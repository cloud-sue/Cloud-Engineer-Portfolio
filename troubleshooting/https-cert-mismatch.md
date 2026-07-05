# HTTPS 접속 실패 — App Gateway ↔ Key Vault 인증서 버전 참조 불일치

> 인증서 자동 재발급 과정에서 Application Gateway가 이미 삭제된 Key Vault secret version을 계속 참조해 HTTPS 접속이 실패한 문제를, 진단·조치·재발 방지까지 추적한 기록입니다.

| 항목 | 내용 |
|------|------|
| 프로젝트 | Multi-Cloud DR 기반 K-Beauty Commerce Platform |
| 영역 | Azure · HTTPS 인증서 자동화 (App Gateway, Key Vault, Terraform, GitHub Actions) |
| 대상 도메인 | `www.sue019522.shop` |
| 한 줄 요약 | 인증서 재발급 후 App Gateway가 삭제된 secret version을 참조해 TLS handshake가 실패한 문제 해결 |

---

## 1. 증상 (Symptom)

`https://www.sue019522.shop/` 접속 시 브라우저에서 페이지가 열리지 않았습니다. Windows `curl`에서는 다음 오류가 발생했습니다.

```
curl: (35) schannel: next InitializeSecurityContext failed:
SEC_E_ILLEGAL_MESSAGE (0x80090326)
```

WSL/Linux에서 확인하면 **TLS handshake 단계에서 실패**했습니다.

```
openssl s_client -connect www.sue019522.shop:443 -servername www.sue019522.shop -brief
```

```
tlsv1 unrecognized name
SSL alert number 112
```

반면 **HTTP는 App Gateway까지 정상 도달**했고 HTTPS로 redirect되고 있었습니다. 즉, 라우팅·리다이렉트는 정상이고 TLS 계층만 깨진 상태임을 먼저 분리했습니다.

```
curl -I http://www.sue019522.shop/
```

```
HTTP/1.1 301 Moved Permanently
Location: https://www.sue019522.shop/
```

---

## 2. 원인 (Root Cause)

Terraform/GitHub Actions로 인증서를 재발급하는 과정에서 Key Vault에는 새 인증서 secret version이 생성되었지만, **이후 Application Gateway 업데이트가 중간에 실패**했습니다. 그 결과 App Gateway는 **이미 삭제된 이전 Key Vault secret version을 계속 참조**하고 있었습니다.

App Gateway가 참조 중이던 secret:

```
https://kv-agw-azsis-kbeauty-dev.vault.azure.net/secrets/www-sue019522-shop/06ea5ae2988644c3aaedfce5abd76894
```

하지만 해당 version은 Key Vault에 존재하지 않았습니다.

```
SecretNotFound
www-sue019522-shop/06ea5ae2988644c3aaedfce5abd76894 was not found
```

Key Vault에 존재하는 최신 secret version은 다음이었습니다.

```
https://kv-agw-azsis-kbeauty-dev.vault.azure.net/secrets/www-sue019522-shop/eecf1b6b1f36440bb665fdd271fef45e
```

### 장애 흐름

```
1. Terraform/GitHub Actions가 새 인증서 버전 생성
2. 예전 인증서 버전(06ea...)이 삭제됨
3. App Gateway 업데이트는 중간 실패
4. App Gateway는 여전히 삭제된 06ea... secret을 참조
5. HTTPS listener가 인증서를 로드하지 못함
6. TLS handshake에서 unrecognized name / schannel 오류 발생
```

---

## 3. 진단 (Diagnosis)

증상을 추측하지 않고, App Gateway가 **참조 중인** version과 Key Vault에 **실제 존재하는** version을 명령어로 대조해 불일치를 증명했습니다.

App Gateway가 참조 중인 인증서 확인:

```bash
az network application-gateway ssl-cert list \
  -g rg-azsis-kbeauty-dev \
  --gateway-name agw-azsis-kbeauty-dev \
  -o table
```

Key Vault 최신 인증서 확인:

```bash
az keyvault certificate show \
  --vault-name kv-agw-azsis-kbeauty-dev \
  --name www-sue019522-shop \
  --query "{id:id,sid:sid,enabled:attributes.enabled,expires:attributes.expires}" \
  -o json
```

secret version 목록 확인:

```bash
az keyvault secret list-versions \
  --vault-name kv-agw-azsis-kbeauty-dev \
  --name www-sue019522-shop \
  -o table
```

---

## 4. 조치 (Action)

App Gateway의 SSL certificate 참조를 **최신 Key Vault secret version으로 갱신**했습니다.

```bash
az network application-gateway ssl-cert update \
  -g rg-azsis-kbeauty-dev \
  --gateway-name agw-azsis-kbeauty-dev \
  -n www-sue019522-shop \
  --key-vault-secret-id "https://kv-agw-azsis-kbeauty-dev.vault.azure.net/secrets/www-sue019522-shop/eecf1b6b1f36440bb665fdd271fef45e"
```

---

## 5. 검증 (Verification)

TLS 인증서가 정상 로드되는지 확인:

```bash
openssl s_client -connect www.sue019522.shop:443 -servername www.sue019522.shop </dev/null 2>/dev/null \
  | openssl x509 -noout -issuer -subject -dates
```

HTTPS 응답 확인:

```bash
curl -I https://www.sue019522.shop/
```

| 구분 | Before | After |
|------|--------|-------|
| HTTPS 접속 | TLS handshake 실패 | 정상 응답 |
| App Gateway 참조 secret | 삭제된 `06ea...` | 최신 `eecf...` |

---

## 6. 재발 방지 (Prevention)

근본 원인은 **실행 주체에 따라 Key Vault access policy가 교체되면서 Terraform apply가 중간 실패**한 것이었습니다. GitHub Actions와 로컬 실행자가 서로 다른 Azure AD object ID를 사용하는데, AppGW Key Vault access policy가 단일 실행자 기준으로 관리되고 있어 실행 주체가 바뀔 때마다 policy가 교체된 것입니다.

따라서 AppGW 전용 Key Vault access policy를 단일 실행자가 아니라 **고정 object ID 목록** 기준으로 관리하도록 변경했습니다.

```hcl
resource "azurerm_key_vault_access_policy" "terraform" {
  for_each = local.https.enabled ? toset(var.certificate_admin_object_ids) : toset([])

  key_vault_id = azurerm_key_vault.appgw[0].id
  tenant_id    = var.tenant_id
  object_id    = each.value

  certificate_permissions = local.access_policies.terraform_certificate_permissions
  secret_permissions      = local.access_policies.terraform_secret_permissions
}
```

이후 기존 Azure policy는 Terraform state에 import하여 **state와 실제 Azure 리소스 상태를 일치**시켰습니다.

---

## 7. 배운 점

- HTTP는 정상인데 HTTPS만 실패하는 경우, 라우팅이 아니라 **TLS 계층(인증서 로드)** 을 먼저 의심해야 합니다.
- 자동화(IaC/CI)가 중간 실패하면 **리소스가 존재하지 않는 참조를 남긴 채 배포가 끝날 수 있다**는 점을 체감했습니다. 자동화가 만든 장애는 다시 자동화의 신뢰성(멱등성·상태 일관성)으로 막아야 합니다.
- "참조 중인 값"과 "실제 존재하는 값"을 명령어로 대조하는 것이 인증서·상태 관련 장애 진단의 핵심입니다.

---

## Security Notice

본 문서의 subscription id, object id, secret version 등은 예시 값이며, 실제 계정·키·비밀번호 등 민감 정보는 포함하지 않습니다.

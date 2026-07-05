# 멀티클라우드 DR 기반 K-뷰티 커머스 플랫폼 서비스 운영

> Azure 메인 운영 · AWS 보조 DR — 무중단 배포와 데이터 무손실을 보장하는 멀티클라우드 아키텍처
> 단일 클라우드 장애점(SPOF)을 해소하고 IaC·CI/CD로 자동화하는 DevOps 환경 구축 (팀 프로젝트)

<p>
  <a href="https://github.com/cloud-sue/pj3_team_kbeauty_dr-azure-.git">
    <img src="https://img.shields.io/badge/GitHub-Azure%20Repo-121011?style=for-the-badge&logo=github&logoColor=white">
  </a>
  <a href="https://github.com/cloud-sue/pj3_team_kbeauty_dr-aws-.git">
    <img src="https://img.shields.io/badge/GitHub-AWS%20Repo-121011?style=for-the-badge&logo=github&logoColor=white">
  </a>
  <!-- <a href="https://www.sue019522.shop">
    <img src="https://img.shields.io/badge/Live-www.sue019522.shop-024AD8?style=for-the-badge&logo=googlechrome&logoColor=white">
  </a> -->
</p>

---

## 📌 프로젝트 개요

Azure를 메인 운영 환경으로, AWS를 보조 DR 환경으로 구성한 **멀티클라우드 기반 K-뷰티 커머스 서비스**입니다. <br>
단일 클라우드의 장애점으로 인한 서비스 전체 중단 리스크를 해소하기 위해, IaC로 인프라를 코드화하고 CI/CD로 빌드·배포를 자동화했으며, Pilot Light DR 전략으로 비용과 복구 속도의 균형을 맞췄습니다.

- **주제**: 멀티클라우드(Azure/AWS) DR 기반 커머스 서비스 운영
- **목표**: 서비스 연속성 · 데이터 보호 · 빠른 복구를 검증하는 재해 복구 환경 구축
- **트래픽 흐름**: `Client → Azure DNS → Traffic Manager → App Gateway(AGIC) → AKS(WEB→WAS) → Azure DB for MySQL`
- **DR 흐름**: `장애 감지 → Traffic Manager Failover → CloudFront/S3 → EKS 배포 → RDS(DMS CDC 복제)`

| 항목 | 내용 |
|------|------|
| 팀명 | Azuresis (애저시스터즈), 3인 |
| 기간 | 2026.06.01 ~ 2026.07.01 (4주) |
| 멘토 | 전*진 (Bespin Global) |


---

## 🛠 기술 스택

<table>
  <tr>
    <td>클라우드<br>(Main)</td>
    <td>
      <img src = "https://img.shields.io/badge/Microsoft%20Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/Azure%20AKS-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white">
      <img src = "https://img.shields.io/badge/App%20Gateway-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/Azure%20DB%20for%20MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>클라우드<br>(DR)</td>
    <td>
      <img src = "https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white">
      <img src = "https://img.shields.io/badge/Amazon%20EKS-FF9900?style=for-the-badge&logo=amazoneks&logoColor=white">
      <img src = "https://img.shields.io/badge/CloudFront-8C4FFF?style=for-the-badge&logo=amazoncloudfront&logoColor=white">
      <img src = "https://img.shields.io/badge/Amazon%20RDS-527FFF?style=for-the-badge&logo=amazonrds&logoColor=white">
      <img src = "https://img.shields.io/badge/AWS%20DMS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>IaC</td>
    <td>
      <img src = "https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white">
      <img src = "https://img.shields.io/badge/Azure%20Blob%20Backend-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>컨테이너</td>
    <td>
      <img src = "https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white">
      <img src = "https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white">
      <img src = "https://img.shields.io/badge/Azure%20ACR-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/Amazon%20ECR-FF9900?style=for-the-badge&logo=amazonecs&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>CI/CD</td>
    <td>
      <img src = "https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white">
      <img src = "https://img.shields.io/badge/Argo%20CD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>서버환경</td>
    <td>
      <img src = "https://img.shields.io/badge/NGINX-009639?style=for-the-badge&logo=nginx&logoColor=white">
      <img src = "https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>보안</td>
    <td>
      <img src = "https://img.shields.io/badge/Azure%20Key%20Vault-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/External%20Secrets-5D3FD3?style=for-the-badge&logo=&logoColor=white">
      <img src = "https://img.shields.io/badge/Let's%20Encrypt-003A70?style=for-the-badge&logo=letsencrypt&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>모니터링& 비용</td>
    <td>
      <img src = "https://img.shields.io/badge/WhaTap-00C7B7?style=for-the-badge&logo=&logoColor=white">
      <img src = "https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white">
      <img src = "https://img.shields.io/badge/OpsNow-232F3E?style=for-the-badge&logo=&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>데이터베이스</td>
    <td>
      <img src = "https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
    </td>
  </tr>
</table>

---

## 🏗 아키텍처

<p align="center">
  <img src="./images/pj3_multicloud-dr-architecture.png" alt="멀티클라우드 DR 전체 아키텍처" width="100%">
</p>

> Azure Main CSP를 메인 운영으로, AWS DR CSP를 보조 DR로 구성하고 VPN(Private)으로 연결한 멀티클라우드 구조. Traffic Manager 헬스체크 기반으로 장애 시 AWS로 Failover되며, DB는 DMS CDC로 상시 복제됩니다.

### 구성 요소

| 계층 | Azure (Main) | AWS (DR) |
|------|--------------|----------|
| 진입/DNS | Azure DNS · Traffic Manager | CloudFront (Failover Endpoint) → S3 |
| L7 라우팅 | Application Gateway (WAF · AGIC) | ALB Ingress |
| WEB/WAS | AKS (Blue/Green) | EKS Cluster |
| 데이터 | Azure Database for MySQL | Amazon RDS MySQL (DR Target) |
| 세션/보안 | Redis · Key Vault · ACR | ECR (DR) |
| 연결 | — VPN (Private) · DMS CDC 복제 — | |

---

## 👥 팀 구성 & 역할

| 팀원 | 담당 (CSP · 영역) | 주요 작업 |
|------|-------------------|-----------|
| 박수현 | Azure · 인프라/운영/배포 | K-beauty 홈페이지 설계·구현, Terraform 인프라, k8s Blue/Green + Canary, Redis 세션 외부화, CI/CD(GitHub Actions·ArgoCD), HTTPS 인증서·만료 알림 |
| 이상일 | Azure/AWS · 운영/DR | Azure AKS(WAS) 구성, DR 운영 문서, Azure↔AWS VPN 구축, AWS DR 인프라 구축, Pilot Light DR 아키텍처 설계 |
| 박가영 | AWS · 모니터링/비용 관리 | AWS k8s(WEB/WAS) 구성, AWS Terraform 인프라, WhaTap 모니터링, 로그 모니터링, Slack 알람 연동, OpsNow 비용 관리 |

---

## ⚙️ 핵심 구현

### 1. Terraform 인프라 (IaC)

역할별 **11개 모듈**(`network · aks · acr · agw · db · redis · keyvault · rbac · traffic_manager · dns · vpn`) + root 조합으로 책임을 분리하고, 의존성(암묵적·명시적)을 부여했습니다.

- **Remote State**: tfstate를 Azure Blob Storage 백엔드(`dev/` 경로 분리)에 저장 — 팀 상태 일관성 유지 및 동시 apply 충돌 방지, prod 환경 상태 분리 확장성 확보
- **Secret 분리**: 환경 설정값은 `terraform.tfvars`, 민감 정보(subscription id, DB 계정 등)는 `.env`(`TF_VAR_*`)로 분리 후 `.gitignore`, 실제 값은 GitHub Secrets로 주입

```hcl
module "agw" {
  source     = "./modules/azure/agw"
  subnet_id  = module.network.appgw_subnet_id
  depends_on = [module.network]
}

backend "azurerm" {
  resource_group_name  = "rg-azsis-kbeauty-blob"
  storage_account_name = "azsiskbeautytfstate"
  container_name       = "tfstate"
  key                  = "dev/terraform.tfstate"   # 환경별 경로 분리
}
```

### 2. Kubernetes — Blue/Green + Canary 무중단 배포

Service의 `selector`를 `blue ↔ green`으로 전환하는 트래픽 스위치 방식으로 배포 중 다운타임을 0으로 유지하고, 문제 발생 시 재배포 없이 직전 color로 되돌려 즉시 롤백합니다.

- **Canary 검증**: AGIC가 가중치 라우팅을 지원하지 않아 `/canary` **경로 기반 라우팅**으로 신버전 검증
- **자가 치유**: `readinessProbe`(준비된 Pod에만 트래픽), `livenessProbe`(비정상 컨테이너 재시작), `HPA`(CPU 60% 기준 replicas 2~20 자동 확장)

```yaml
# ingress.yaml
spec:
  rules:
  - host: www.sue019522.shop
    http:
      paths:
      - path: /canary                                  # 검증용 경로
        backend: { service: { name: web-green } }
      - path: /                                        # 일반 사용자
        backend: { service: { name: web-active } }
```

### 3. Redis 세션 외부화

HttpSession을 Redis로 분리해 Pod가 바뀌어도 로그인 세션을 유지합니다. `/api/auth/me`를 12회 반복 호출하는 검증에서 pod 메모리 세션(blue)은 일부만 성공하는 반면, Redis 세션(green)은 12회 모두 동일한 JSESSIONID로 성공합니다. Redis 접속 정보는 **External Secrets Operator**로 Key Vault에서 자동으로 가져와 K8s Secret으로 생성 후 파드에 주입합니다(`refreshInterval: 1h`).

### 4. CI/CD 자동화 (GitHub Actions + ArgoCD)

관련 파일 변경 + 커밋 메시지에 `deploy` 포함 시에만 워크플로우가 동작합니다.

| 단계 | 트리거 | 동작 |
|------|--------|------|
| CI (PR 시) | main 브랜치 PR | quality-gate(format·validate·lint·security scan), build test(matrix로 blue/green 병렬), plan 결과 댓글 |
| CD (merge 시) | 관리자 승인 후 merge | OIDC 키리스 인증으로 apply, ACR/ECR push, determine-target(운영 color 자동 판단), GitOps 이미지 태그 갱신 |

- **OIDC 키리스 인증**: 단기 토큰 발급으로 비밀키 미보관, Environment 승인 단계 추가
- **ArgoCD**: Git manifest 변경 감지 후 새 이미지로 AKS/EKS 자동 동기화

### 5. HTTPS 인증서 자동화

Let's Encrypt 공인 인증서를 **DNS-01** 방식으로 자동 발급 → Key Vault → App Gateway 443 리스너 바인딩. 만료 **30일 전 Slack 알람** 및 자동 재발급으로 만료 사고를 방지하며, 전 구간 HTTPS(`ssl-redirect: true`)를 적용했습니다.

```
인증서 요청(Terraform) → DNS-01 검증(Azure DNS _acme-challenge TXT)
→ Key Vault 저장(PFX) → AppGW 443 바인딩 → HTTP→443 리다이렉트
```

---

## 🔁 DR 전략 및 구현

### Pilot Light를 선택한 이유

데이터는 상시(RDS 복제), 컴퓨팅은 온디맨드로 두어 RTO와 비용의 균형을 맞췄습니다.

| 전략 | 컴퓨팅 | 비용 | RTO |
|------|--------|------|-----|
| Backup & Restore | 없음 (cold) | 최저 | 수 시간 (너무 느림) |
| **Pilot Light ✅** | **데이터(RDS)만 상시** | **중간** | **실측 33분** |
| Warm Standby | 최소사양 상시 | 높음 | 수 분 (상시 비용 과다) |
| Active-Active | 전부 상시 (hot) | 최고 (2배) | 거의 0 (과투자) |

### 장애 감지 → DR 발동

**자동 감지 → 수동 판정 → 수동 트리거** 흐름으로 오발동을 방지합니다.

1. **Lambda HC**: EventBridge가 1분 주기로 Azure AGW HTTPS 헬스체크
2. **알람 발동**: CloudWatch Alarm → Slack 알림
3. **담당자 판정**: `curl` / `kubectl` / WhaTap 직접 확인 (CrashLoopBackOff·Pending, 임계값 초과)
4. **DR 트리거**: `terraform apply`

> **감지 임계값 15분** — 0~5분(네트워크 장애) → 5~10분(담당자 검증) → 10~15분(오발동 최종 배제). 사용자는 약 3분 시점부터 정적 웹페이지로 안내됩니다.

### Failover 배포 순서

```
① NAT Gateway 생성      (프라이빗 서브넷 인터넷 경로 확보)
② ECR 접근 활성화       (이미지 저장소 Pull 가능)
③ EKS NodeGroup 배포    (depends_on: NAT GW 완료 후)
```

### Failback (AWS DR → Azure Primary 복귀)

DMS 역방향 복제 → 데이터 정합성 확인(row count·checksum) → Azure 인프라 복구(Pod Running·AGW HC 200) → Traffic Manager 자동 복귀 → AWS DR 리소스 정리(RDS만 상시 유지).

> ⚠️ 트래픽이 Azure로 완전히 전환된 것을 확인한 후 DR 인프라를 destroy

### DR 데이터 정합성 (DMS CDC)

| DMS 복제 구성 | 값 |
|---------------|-----|
| 복제 유형 | Full-Load-and-CDC |
| CDC 방식 | Binary Log 기반 |
| 복제 단위 | Committed 트랜잭션 |
| 통신 경로 | VPN (Private) |
| 소스 → 타깃 | Azure MySQL → Amazon RDS MySQL |

- **Row Count 비교**: `SELECT COUNT(*)` 주요 테이블 건수 일치 (Azure↔AWS 16건 일치)
- **Checksum 검증**: `SUM(CRC32(...))` 해시값 비교로 값 변조 감지 (양측 일치)
- **CDC 지연**: 실측 Max 2.4s + 2.4s ≈ 약 5초 (분 단위 0분)

---

## 📊 RTO / RPO 테스트 결과

**총 5회 훈련 · 목표 달성 4/5회 · 최단 RTO 30분(5회차)**

| 회차 | 일자 | 단계 | RTO 목표 | RTO 실측 | RPO 실측 | 달성 | 비고 |
|------|------|------|----------|----------|----------|------|------|
| 1 | 06-19 | 1단계 | 10분 | 3분 | 0 | ✅ | — |
| 1 | 06-19 | 2단계 | 60분 | 40분 | 약 5초 | ✅ | NAT 생성 문제 |
| 2 | 06-23 | 2단계 | 60분 | 120분 | 약 5초 | ❌ | Pod 이미지 빌드 오류 (예외) |
| 3 | 06-23 | 2단계 | 60분 | 31분 | 약 5초 | ✅ | 정상 |
| 4 | 06-24 | 2단계 | 60분 | 35분 | 약 5초 | ✅ | 정상 |
| 5 | 06-25 | 2단계 | 60분 | 30분 | 약 5초 | ✅ | 정상 |

- **RTO**: 목표 60분 대비 **평균 33분** (목표 대비 -45%)
- **RPO**: 목표 1분 대비 **0분** (DMS CDC 실시간 복제)

---

## 📡 모니터링 및 비용 관리

- **WhaTap 통합 모니터링**: Azure 운영·AWS DR 환경의 Node/Pod 상태, CPU/Memory, Restart Count, TPS/응답시간, Apdex, Heap Memory 관측
- **APM 성공률**: HTTP 상태코드 대신 트랜잭션 에러 여부 기준 `(Total TX − Error TX) / Total TX × 100`
- **로그 분석**: AppLog(WARN/ERROR, HikariPool 경고)로 원인 추적, Access Log 기반 성공률 지표로 확장 예정
- **경고 & Slack 알림**: 운영/DR 환경을 분리해 Web/WAS별 조건(`tx_error > 10`, `RestartCount > 5`, ALB UnHealthy 등)을 Warning/Critical 이벤트로 설정, 발생 시 whatap-alarm 채널로 자동 전송
- **OpsNow 비용 관리**: Azure/AWS 월별 비용 통합 조회, 서비스별 비교, DR 테스트 후 미사용 리소스 점검

---

## 🚀 향후 개선 방안

| 구분 | 현재 | 개선안 |
|------|------|--------|
| 자동화 | Azure 중심 CI/CD 자동화 | AWS까지 CI/CD 자동화 확장 |
| DR 훈련 | 프로젝트 기간 내 5회 훈련 | 분기별 장애 주입 테스트로 RTO/RPO 지속 검증·절차 개선 |
| 비용 최적화 | Pilot Light 기본 구성 | OpsNow 분석 기반 자원 규모 재조정으로 평시 비용 추가 절감 |
| 성공률 지표 | 트랜잭션 에러 기준 산출 | Access Log 기반 2xx/4xx/5xx 비율로 성공률·오류 원인 분석 |

---

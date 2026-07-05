# Redis 세션 외부화 — 세션 유지 실패부터 502·OOMKilled까지

> Blue/Green 무중단 배포 환경에서 Pod가 바뀌면 로그인 세션이 풀리던 문제를 Redis 세션 외부화로 해결하고, 그 과정에서 이어진 Redis 연결 502와 Green Pod OOMKilled까지 연쇄적으로 추적한 기록입니다.

| 항목 | 내용 |
|------|------|
| 프로젝트 | Multi-Cloud DR 기반 K-Beauty Commerce Platform |
| 영역 | Azure · Kubernetes(AKS) · Spring Session · Redis |
| 검증 방식 | `/canary` 경로에서 `/api/auth/me` 12회 반복 호출로 세션 유지 확인 |
| 한 줄 요약 | HttpSession을 Redis로 외부화해 Pod 교체·스케일링 환경에서 로그인 세션 유지 |

---

## 문제 1. Green WAS 세션 유지 실패

### 증상

`/canary` 환경에서 로그인 후 세션 확인 시 일부 요청만 성공했습니다. 같은 `JSESSIONID`로 요청했는데도 일부 WAS Pod에서는 로그인 상태를 인식하지 못했습니다.

```
세션 끊김 감지 (8/12 성공, 실패 4)
```

### 원인

- 기존에는 WAS Pod마다 세션을 **로컬 메모리**에 저장하고 있었습니다.
- Load Balancer/Service가 요청을 다른 WAS Pod로 보내면 해당 Pod에는 세션 정보가 없습니다.
- 따라서 같은 사용자의 요청이어도 **Pod가 바뀌면 로그인 상태가 풀린 것처럼** 보였습니다.

### 해결

`was-green`에 Spring Session Redis를 적용하고, Azure Managed Redis를 세션 저장소로 사용했습니다. `was-green` Pod들이 같은 Redis namespace를 바라보도록 설정했습니다.

```properties
spring.session.store-type=redis
spring.session.redis.namespace=kbeauty:session
spring.data.redis.ssl.enabled=true
```

Redis 접속 정보는 Kubernetes Secret으로 주입했습니다.

```
SPRING_DATA_REDIS_HOST
SPRING_DATA_REDIS_PORT
SPRING_DATA_REDIS_PASSWORD
```

### 결과

- Pod가 바뀌어도 Redis에서 같은 세션을 조회 → `JSESSIONID` 기준으로 로그인 상태 유지
- Blue는 기존 로컬 세션, Green은 Redis 세션 구조로 **직접 비교 가능**

---

## 문제 2. Redis 연결 후 로그인 502 발생

### 증상

`/canary/api/auth/login` 요청 시 `502 Bad Gateway`가 발생했습니다. WAS 로그에서 Redis 연결 실패를 확인했습니다.

```
Unable to connect to redis-azsis-kbeauty-dev.koreacentral.redis.azure.net
connection timed out
```

### 원인

- Azure Managed Redis는 **public access가 닫혀** 있었습니다.
- 그런데 AKS Pod에서 Redis hostname을 조회하면 private IP가 아니라 **public IP로 해석**되었습니다. Private DNS Zone 설정이 Managed Redis hostname과 맞지 않았습니다.
- 또한 Managed Redis 포트는 `10000`인데, **NSG는 기존 Redis 포트인 `6379` 기준**으로 열려 있었습니다.

### 해결

Terraform Redis 모듈에 Managed Redis용 Private DNS Zone을 설정하고, Redis hostname이 VNet 내부에서 private endpoint IP로 해석되도록 A record를 추가했습니다.

```hcl
private_dns_zone_name = "${var.location}.redis.azure.net"

resource "azurerm_private_dns_a_record" "redis" {
  name    = local.redis_config.name
  records = [azurerm_private_endpoint.redis.private_service_connection[0].private_ip_address]
}
```

NSG Redis 허용 포트를 `6379`에서 `10000`으로 변경했습니다.

```hcl
destination_port_range = "10000"
```

### 결과

- AKS WAS Pod에서 Redis hostname이 private IP로 해석됨
- Redis Session 저장 정상 동작 → 로그인 요청 502 해결

---

## 문제 3. Green WAS가 Blue보다 느리고 세션 확인이 간헐적으로 실패

### 증상

Blue는 빠른데 Green은 상품 목록·server-info·로그인 확인이 느리고, 세션 확인이 간헐적으로 실패했습니다.

```
세션 끊김 감지 (8/12 성공, 실패 4)
```

web-green nginx 로그에서 upstream 연결 실패가 발생했습니다.

```
connect() failed (111: Connection refused) while connecting to upstream
```

was-green Pod에서 재시작이 발생했습니다.

```
Reason: OOMKilled
Exit Code: 137
```

### 원인

- `was-green`의 CPU/Memory request·limit이 `was-blue`보다 훨씬 낮았습니다. Green은 Redis Session까지 사용하므로 Blue보다 메모리 사용량이 더 큽니다.

  ```yaml
  requests: { cpu: "100m", memory: "128Mi" }
  limits:   { cpu: "250m", memory: "256Mi" }
  ```

- Spring Boot 기동 시간이 긴데 **readinessProbe가 없어**, WAS가 완전히 준비되기 전에 Service endpoint에 붙을 수 있었습니다. 이 상태에서 web-green nginx가 요청을 보내면 connection refused가 발생했습니다.

### 해결

`was-green` 리소스를 `was-blue`와 동일하게 상향했습니다.

```yaml
resources:
  requests: { cpu: "300m", memory: "512Mi" }
  limits:   { cpu: "1000m", memory: "1Gi" }
```

가벼운 health check API(`GET /api/healthz`)를 추가하고, Deployment에 `startupProbe`·`readinessProbe`를 추가했습니다.

```yaml
startupProbe:
  httpGet: { path: /api/healthz, port: 8080 }
  periodSeconds: 5
  failureThreshold: 24
readinessProbe:
  httpGet: { path: /api/healthz, port: 8080 }
  periodSeconds: 5
  timeoutSeconds: 2
  failureThreshold: 3
```

### 결과

- WAS가 완전히 기동된 뒤에만 Service endpoint에 등록됨
- OOMKilled 방지, web-green nginx upstream connection refused 감소
- 세션 확인 실패가 **실제 세션 문제인지 Pod 불안정 문제인지 구분 가능**해짐

---

## 전체 흐름 정리

```
세션 유지 실패 (Pod 로컬 메모리 세션)
   ↓ Spring Session Redis 외부화
Redis 연결 502 (Private DNS / NSG 포트 불일치)
   ↓ Private DNS A record + NSG 10000 포트 개방
Green Pod OOMKilled / connection refused (리소스 부족 + Probe 부재)
   ↓ 리소스 상향 + startup/readiness Probe 추가
Pod 교체·스케일링 환경에서도 로그인 세션 안정 유지
```

---

## 배운 점

- 세션 유지 문제는 애플리케이션(Spring Session)만이 아니라 **네트워크(Private DNS·NSG)와 워크로드 리소스(Probe·requests/limits)** 까지 함께 봐야 완결됩니다.
- "세션 확인 실패"라는 같은 증상이라도 원인은 로컬 세션·Redis 연결·Pod 불안정으로 각각 달랐고, 계층을 분리해야 진짜 원인에 도달할 수 있었습니다.
- Managed 서비스는 기존 서비스와 **포트·접근 방식이 다를 수 있다**는 점(Redis 6379 → 10000)을 확인하는 습관을 얻었습니다.

---

## Security Notice

본 문서에는 실제 Redis 접속 정보, 계정, 비밀번호 등 민감 정보를 포함하지 않습니다.

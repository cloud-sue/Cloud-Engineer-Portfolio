# Azure 기반 고가용성 3-Tier 웹 서비스 인프라 구축

> [베스핀글로벌] 멀티클라우드 취업실무과정 — Azure 1팀 (Azure씨들)
> Auto Scaling 및 Multi-AZ 기반 무중단 고가용성 웹 서비스 인프라

---

## 📌 프로젝트 개요

전국 20여 개 지점을 운영하는 대형 동물병원 예약/조회 플랫폼(**PetClinic**)을 대상으로, 매월 초 정기 검진 할인 이벤트 시 접속자가 3배 급증하는 트래픽을 무중단으로 처리하는 **엔터프라이즈급 3-Tier 인프라**를 Azure 기반으로 구축했습니다.

- **주제**: 트래픽에 유연하게 대응하는 중단 없는 서비스를 위한 Auto Scaling · Multi-AZ 기반 고가용성 웹 인프라
- **내용**: Azure 기반 3-Tier(Web/WAS/DB) 웹 서비스 환경 구축
- **기대 효과**: 운용 비용 절감 및 서비스 연속성 보장
- **트래픽 흐름**: `Client → DNS → Public AGW → Web VMSS → Internal AGW → WAS VMSS → Azure MySQL`

---

## 📅 프로젝트 기간

`2025.03.30 ~ 2025.04.10` (총 2주)
---

## 🛠 기술 스택

<table>
  <tr>
    <td>운영체제</td>
    <td>
      <img src = "https://img.shields.io/badge/Rocky%20Linux-10B981?style=for-the-badge&logo=rockylinux&logoColor=white">
      <img src = "https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black">
    </td>
  </tr>
  <tr>
    <td>클라우드</td>
    <td>
      <img src = "https://img.shields.io/badge/Microsoft%20Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/VMSS-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/Application%20Gateway-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/Traffic%20Manager-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>언어</td>
    <td>
      <img src = "https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white">
      <img src = "https://img.shields.io/badge/Groovy-4298B8?style=for-the-badge&logo=apachegroovy&logoColor=white">
      <img src = "https://img.shields.io/badge/Shell%20Script-121011?style=for-the-badge&logo=gnubash&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>서버환경</td>
    <td>
      <img src = "https://img.shields.io/badge/Apache%20Tomcat%209.0-D22128?style=for-the-badge&logo=Apache%20Tomcat&logoColor=white">
      <img src = "https://img.shields.io/badge/Apache-D22128?style=for-the-badge&logo=apache&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>프레임워크</td>
    <td>
      <img src = "https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>데이터베이스</td>
    <td>
      <img src = "https://img.shields.io/badge/Azure%20Database%20for%20MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>모니터링</td>
    <td>
      <img src = "https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white">
      <img src = "https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>테스트</td>
    <td>
      <img src = "https://img.shields.io/badge/nGrinder-00A98F?style=for-the-badge&logo=naver&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>도구</td>
    <td>
      <img src = "https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white">
      <img src = "https://img.shields.io/badge/DBeaver-372923?style=for-the-badge&logo=dbeaver&logoColor=white">
      <img src = "https://img.shields.io/badge/Visual%20Studio%20Code-0078d7.svg?style=for-the-badge&logo=visual-studio-code&logoColor=white">
    </td>
  </tr>
</table>

---

## 👥 팀 구성 및 역할

계층별 전담제(Web·WAS·DB)를 통한 전문적 3-Tier 인프라 구축

| 담당 | 역할 | 주요 업무 |
|------|------|-----------|
| 이\*일 (팀장) | WEB | AGW 설정, VMSS 구현, DNS 설정, Apache Proxy 설정, 모니터링/경보 체계 구축, 부하테스트 |
| 박수현 (팀원) | WAS | AGW 설정, VMSS 구현, 코드 리팩토링, Tomcat 설정, 모니터링/경보 체계 구축, 부하테스트 |
| 박\*영 (팀원) | DB | 고가용성 DB 설계, 조회 성능 최적화, DB Failover 테스트, 백업/복구 정책 수립 |
| 전\*진 (멘토-BespinGlobal) | — | 아키텍처 리뷰 및 기술 지도 |

<br>

### 🙋‍♂️ My Part — 박수현 (WAS 계층 전담)

> **본 프로젝트에서 저는 WAS 계층을 전담했습니다.**

```
Role  :  WAS (Web Application Server) Tier
Stack :  Application Gateway · VMSS · Tomcat 9.0 · Spring PetClinic · Azure MySQL
```

- ⚙️ **Internal Application Gateway 설정** — L7 기반 경로 라우팅(`/petclinic`) 및 Health Check 구성
- 📈 **WAS VMSS 구현** — Auto Scaling(Min 2 / Max 20) 및 Pre-warm 정책 적용
- 🐱 **Tomcat 9.0 서버 구축** — Systemd 서비스 등록, 데이터 디스크 마운트, 골든 이미지 제작
- 🔧 **PetClinic 코드 리팩토링** — 환경 변수 기반 Azure MySQL 접속 정보 주입(보안 처리), 시스템 시각화(Zone/Host/DB) 기능 추가
- 📊 **모니터링/경보 체계 구축 & 부하테스트** — Grafana·Slack 연동, nGrinder 성능 검증(단일 VM → VMSS Scale-out으로 TPS 3배 향상)

---

## 🏗 아키텍처
ㅇㅇ

README 파일 만들겠습니다. 먼저 관련 스킬을 확인하겠습니다.


Read the markdown skill before creating the README file
Read the markdown skill before creating the README file
md 스킬은 없으니 바로 파일을 생성하겠습니다.


파일 생성됨, 파일 읽음
파일 생성됨, 파일 읽음
기술 스택 섹션까지 합쳐서 전체 README를 완성했습니다. GitHub에 올리면 뱃지와 표가 그대로 렌더링됩니다. 아키텍처 다이어그램 이미지를 삽입하거나 데모 링크를 추가하고 싶으면 말씀해 주세요.


Readme
문서 · MD 
## 👥 팀 구성 및 역할
계층별 전담제(Web·WAS·DB)를 통한 전문적 3-Tier 인프라 구축
| 담당 | 역할 | 주요 업무 |
|------|------|-----------|
| 이*일 (팀장) | WEB | AGW 설정, VMSS 구현, DNS 설정, Apache Proxy 설정, 모니터링/경보 체계 구축, 부하테스트 |
| 박수현 (팀원) | WAS | AGW 설정, VMSS 구현, 코드 리팩토링, Tomcat 설정, 모니터링/경보 체계 구축, 부하테스트 |
| 박*영 (팀원) | DB | 고가용성 DB 설계, 조회 성능 최적화, DB Failover 테스트, 백업/복구 정책 수립 |
| 전*진 (멘토-BespinGlobal) | — | 아키텍처 리뷰 및 기술 지도 |
---

여기 역할에서 내껏만 강조하고 싶어 하이라이팅 등으로

더 보기
README의 팀 구성 표를 박수현(WAS) 행만 강조하도록 수정하겠습니다.


파일 수정됨, 파일 읽음
파일 수정됨, 파일 읽음
박수현(WAS) 행만 강조되도록 수정했습니다.

적용한 강조 방식은 세 가지입니다. 본인 행 전체를 볼드 처리하고, 이름 앞에 👉 표시를 넣었으며, 역할(WAS)은 코드 하이라이트로 눈에 띄게 했습니다. 표 아래에는 담당 내용을 요약한 인용 블록도 추가했습니다.

참고로 GitHub 마크다운 표에서는 행 배경색 하이라이팅은 지원되지 않아 볼드·이모지·코드블록 조합으로 구현했습니다. 다른 팀원 이름은 요청대로 마스킹(이*일, 박*영, 전*진)하고 멘토는 소속(BespinGlobal)을 표기했습니다.

더 강하게 표현하고 싶으면 본인 행만 별도 카드(별도 섹션)로 빼는 방법도 있는데, 그렇게 바꿔드릴까요?


Readme
문서 · MD 
ㅇㅇ

본인 담당 부분을 별도 카드 섹션으로 분리하겠습니다.


파일 조회함, 파일 수정됨, 파일 읽음
파일 조회함, 파일 수정됨, 파일 읽음
본인 담당 부분을 별도 카드 섹션(🙋‍♂️ My Part — 박수현)으로 분리했습니다.

전체 팀 표는 담백하게 유지하고, 그 아래에 본인 기여만 집중적으로 보여주는 카드를 새로 만들었습니다. 코드블록으로 Role·Stack을 요약하고, 실제 발표자료의 WAS 관련 세부 작업(Internal AGW, VMSS, Tomcat 골든 이미지, 환경변수 기반 DB 접속 보안 처리, nGrinder 부하테스트)을 이모지 불릿으로 정리했습니다.

포트폴리오 관점에서 채용담당자가 "이 사람이 뭘 했는지"가 한눈에 들어오도록 구성한 형태입니다. 카드 톤을 더 담백하게 하거나, 반대로 성과 수치(TPS 3배, 응답시간 45% 단축 등)를 더 부각하고 싶으면 조정해 드리겠습니다.


Readme
문서 · MD 
1783235577568_image.png
이렇게 되어있는데 아키텍처단 맨 위에 이미지 추가해줘.

리포지토리 구조를 보니 아키텍처 이미지가 images/azure-ha-architecture.png에 있네요. 아키텍처 섹션 맨 위에 이미지를 추가하겠습니다.


Find the architecture section heading to insert image after it
Find the architecture section heading to insert image after it
파일 구조를 보면 이 README는 projects/pj1_azure-ha-infra.md가 될 것 같은데요. 이미지 경로는 projects/에서 images/로 올라가야 하므로 상대 경로로 넣겠습니다.


파일 수정됨, 파일 읽음
파일 수정됨, 파일 읽음

Add architecture image at the top of the architecture section

README.md
+9
-3

Presented file
완료
아키텍처 섹션 맨 위에 이미지를 추가했습니다.

경로는 이 파일이 projects/pj1_azure-ha-infra.md 위치에 있다고 보고 ../images/azure-ha-architecture.png로 지정했습니다. 가운데 정렬에 폭 100%로 넣었고, 아래에 트래픽 흐름 캡션도 달았습니다.

한 가지 확인이 필요한 부분이 있습니다. 만약 이 내용을 최상위 README.md에 넣으실 거라면 경로에서 ../를 빼고 images/azure-ha-architecture.png로 바꿔야 이미지가 정상 표시됩니다. 어느 파일에 넣으실 건가요?


Readme
문서 · MD 

Claude가 응답할 때 알림을 받으시겠습니까?





Claude는 AI이며 실수할 수 있습니다. 응답을 다시 한번 확인해 주세요.


Readme · MD
# Azure 기반 고가용성 3-Tier 웹 서비스 인프라 구축
 
> [베스핀글로벌] 멀티클라우드 취업실무과정 — Azure 1팀 (Azure씨들)
> Auto Scaling 및 Multi-AZ 기반 무중단 고가용성 웹 서비스 인프라
 
---
 
## 📌 프로젝트 개요
 
전국 20여 개 지점을 운영하는 대형 동물병원 예약/조회 플랫폼(**PetClinic**)을 대상으로, 매월 초 정기 검진 할인 이벤트 시 접속자가 3배 급증하는 트래픽을 무중단으로 처리하는 **엔터프라이즈급 3-Tier 인프라**를 Azure 기반으로 구축했습니다.
 
- **주제**: 트래픽에 유연하게 대응하는 중단 없는 서비스를 위한 Auto Scaling · Multi-AZ 기반 고가용성 웹 인프라
- **내용**: Azure 기반 3-Tier(Web/WAS/DB) 웹 서비스 환경 구축
- **기대 효과**: 운용 비용 절감 및 서비스 연속성 보장
- **트래픽 흐름**: `Client → DNS → Public AGW → Web VMSS → Internal AGW → WAS VMSS → Azure MySQL`
---
 
## 🛠 기술 스택
 
<table>
  <tr>
    <td>운영<br>체제</td>
    <td>
      <img src = "https://img.shields.io/badge/Rocky%20Linux-10B981?style=for-the-badge&logo=rockylinux&logoColor=white">
      <img src = "https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black">
    </td>
  </tr>
  <tr>
    <td>클라<br>우드</td>
    <td>
      <img src = "https://img.shields.io/badge/Microsoft%20Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/VMSS-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/Application%20Gateway-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
      <img src = "https://img.shields.io/badge/Traffic%20Manager-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>언어</td>
    <td>
      <img src = "https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white">
      <img src = "https://img.shields.io/badge/Groovy-4298B8?style=for-the-badge&logo=apachegroovy&logoColor=white">
      <img src = "https://img.shields.io/badge/Shell%20Script-121011?style=for-the-badge&logo=gnubash&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>서버<br>환경</td>
    <td>
      <img src = "https://img.shields.io/badge/Apache%20Tomcat%209.0-D22128?style=for-the-badge&logo=Apache%20Tomcat&logoColor=white">
      <img src = "https://img.shields.io/badge/Apache-D22128?style=for-the-badge&logo=apache&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>프레임<br>워크</td>
    <td>
      <img src = "https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>데이터<br>베이스</td>
    <td>
      <img src = "https://img.shields.io/badge/Azure%20Database%20for%20MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>모니<br>터링</td>
    <td>
      <img src = "https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white">
      <img src = "https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>테스트</td>
    <td>
      <img src = "https://img.shields.io/badge/nGrinder-00A98F?style=for-the-badge&logo=naver&logoColor=white">
    </td>
  </tr>
  <tr>
    <td>도구</td>
    <td>
      <img src = "https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white">
      <img src = "https://img.shields.io/badge/DBeaver-372923?style=for-the-badge&logo=dbeaver&logoColor=white">
      <img src = "https://img.shields.io/badge/Visual%20Studio%20Code-0078d7.svg?style=for-the-badge&logo=visual-studio-code&logoColor=white">
    </td>
  </tr>
</table>
---
 
## 👥 팀 구성 및 역할
 
계층별 전담제(Web·WAS·DB)를 통한 전문적 3-Tier 인프라 구축
 
| 담당 | 역할 | 주요 업무 |
|------|------|-----------|
| 이\*일 (팀장) | WEB | AGW 설정, VMSS 구현, DNS 설정, Apache Proxy 설정, 모니터링/경보 체계 구축, 부하테스트 |
| 박수현 (팀원) | WAS | AGW 설정, VMSS 구현, 코드 리팩토링, Tomcat 설정, 모니터링/경보 체계 구축, 부하테스트 |
| 박\*영 (팀원) | DB | 고가용성 DB 설계, 조회 성능 최적화, DB Failover 테스트, 백업/복구 정책 수립 |
| 전\*진 (멘토-BespinGlobal) | — | 아키텍처 리뷰 및 기술 지도 |
 
<br>
### 🙋‍♂️ My Part — 박수현 (WAS 계층 전담)
 
> **본 프로젝트에서 저는 WAS 계층을 전담했습니다.**
 
```
Role  :  WAS (Web Application Server) Tier
Stack :  Application Gateway · VMSS · Tomcat 9.0 · Spring PetClinic · Azure MySQL
```
 
- ⚙️ **Internal Application Gateway 설정** — L7 기반 경로 라우팅(`/petclinic`) 및 Health Check 구성
- 📈 **WAS VMSS 구현** — Auto Scaling(Min 2 / Max 20) 및 Pre-warm 정책 적용
- 🐱 **Tomcat 9.0 서버 구축** — Systemd 서비스 등록, 데이터 디스크 마운트, 골든 이미지 제작
- 🔧 **PetClinic 코드 리팩토링** — 환경 변수 기반 Azure MySQL 접속 정보 주입(보안 처리), 시스템 시각화(Zone/Host/DB) 기능 추가
- 📊 **모니터링/경보 체계 구축 & 부하테스트** — Grafana·Slack 연동, nGrinder 성능 검증(단일 VM → VMSS Scale-out으로 TPS 3배 향상)
---
 
## 🏗 아키텍처
 
<p align="center">
  <img src="../images/azure-ha-architecture.png" alt="Azure 고가용성 3-Tier 아키텍처" width="100%">
</p>

### 네트워크 설계 (Vnet: 10.0.0.0/16)

| 서브넷 | 용도 | 대역 | 공인 IP |
|--------|------|------|:------:|
| snet-agw-external | Application Gateway | 10.0.50.0/24 | O |
| snet-web | WEB Tier (VMSS) | 10.0.1.0/24 | |
| snet-agw-internal | Application Gateway | 10.0.60.0/24 | |
| snet-was | WAS Tier (VMSS + LB) | 10.0.2.0/24 | |
| snet-db | DB Tier | 10.0.3.0/24 | |
| snet-bastion | Bastion Server | 10.0.10.0/24 | O |

### 보안 그룹(NSG) 설계

- **NSG-web**: WEB의 AGW를 통해서만 접속 허용 (AzureLoadBalancer 소스)
- **NSG-agw-was-internal**: WEB 서브넷(10.0.1.0/24)에서 오는 8080 포트만 허용
- **NSG-db**: WAS 서브넷(10.0.2.0/24)에서 오는 3306 포트만 허용
- DB는 공용 액세스(Public IP) 완전 차단, 프라이빗 액세스(VNet 통합) 구성

---

## ⚙️ 핵심 구현

### 1. 고가용성(HA) 전략

- **Multi-AZ 구성**: Web/WAS/DB 모두 Zone 분산 배치 (Web·WAS: Zone 1,2 / DB: Zone 1,3)
- **VMSS Auto Scaling**
  - WEB: Min 2 / Max 10 / 확장 CPU>60%, 축소 CPU<30%
  - WAS: Min 2 / Max 20 / 확장 CPU>60%(2대씩), 축소 CPU<30%(2대씩)
  - **Pre-warm 정책**: 매월 1일 이벤트 대비 오전 8시 사전 확장 (2대 → 4대)
- **L7 Application Gateway**: 상세 Health Check, 경로 기반 라우팅(`/petclinic`), SSL/TLS 종단 처리

### 2. 데이터 안정성

- **자동 Failover**: 강제 Failover 테스트 시 약 30초 내 보조 영역(Zone 3) 전환, 복제 지연 0초 유지
- **백업 정책**: 12시간 주기 자동 백업(RPO 12h), 7일간 백업본 보관
- **복구 목표**: RTO 2시간 이내, PITR(시점 복구) 활용 신규 서버 인스턴스 즉시 생성

### 3. 모니터링 및 알림

- Grafana 대시보드로 VMSS/DB CPU, DB Connection, Threads 실시간 시각화
- Slack 연동 알림: Evaluation Interval 30s, Pending Period 최소화로 임계치 즉시 반응(Scale-out)

---

## 📊 부하 테스트 결과 (nGrinder)

### 단일 VM 테스트

| 계층 | Vuser | 평균 TPS | 평균 응답시간 | 결과 |
|------|:-----:|:-------:|:------------:|------|
| WEB | 600명 | 3,240.40/s | 101.43 ms | 안정적 (성공률 98.75%) |
| WAS | 300명 | 181.8 | 1,619.01 ms | CPU 96~98% 병목 → Scale-out 필요 |

### VMSS 테스트 (Auto-Scaling 적용)

| 항목 | 수치 | 단일 VM 대비 |
|------|:----:|-------------|
| Vuser | 500명 | ▲ 200명 증가 |
| 평균 TPS | 549.5 | ▲ 약 3배 향상 |
| 평균 응답시간 | 883.48 ms | ▼ 45% 단축 |
| WAS CPU 부하 | 66~80% | 부하 감소 (Scale-out 효과) |

**결론**: 단일 VM 환경의 물리적 한계를 VMSS Auto-Scaling으로 해소, 성능 3배 향상 및 응답시간 45% 단축을 검증

---

## 🚀 향후 개선 방안

**보완점 (보안 고도화)**

- HTTPS 보안 적용 / WAF 도입 / Azure Key Vault 활용

**개선 방안**

- 글로벌 사용자를 위한 CDN 적용
- DR 시스템 고도화
- Read-Replica를 활용한 DB 읽기 성능 개선
- 자동 장애 복구 스크립트 도입



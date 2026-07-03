# 박수현 | Cloud Engineer Portfolio

> **애플리케이션 구조를 이해하고, 인프라 운영 관점에서 문제를 해결하는 클라우드 엔지니어 지원자**

Java/Spring 기반 웹 개발 교육과 프로젝트 운영 경험을 바탕으로 클라우드 인프라·DevOps 영역으로 역량을 확장하고 있습니다.  
단순히 인프라를 구축하는 것에 그치지 않고, **애플리케이션 동작 방식·데이터 흐름·배포 구조**를 함께 고려하여 안정적인 서비스 운영 환경을 설계하는 데 강점이 있습니다.

---

## Core Competency

| 역량 | 설명 |
|---|---|
| **Cloud Architecture** | Azure/AWS 기반 3-Tier, 고가용성, 멀티클라우드 DR 아키텍처 설계 및 구현 |
| **Kubernetes Operation** | AKS/EKS 환경에서 Web/WAS 컨테이너 배포, Service, Ingress, Probe, HPA 구성 경험 |
| **IaC** | Terraform 모듈화, Remote State, 환경 변수·Secret 분리 기반 인프라 코드화 경험 |
| **CI/CD & GitOps** | GitHub Actions와 ArgoCD를 활용한 이미지 빌드·레지스트리 Push·GitOps 배포 흐름 구성 |
| **Troubleshooting** | DB Failover, 세션 유지, Secret 주입, 배포/인증 오류 등 운영 이슈 원인 분석 및 해결 |
| **Application Understanding** | Java/Spring, DB, WAS, 배포 흐름 이해를 기반으로 애플리케이션과 인프라 사이의 문제 분석 |

---

## Tech Stack

| Category | Skills | Experience |
|---|---|---|
| **Cloud** | Azure, AWS | Azure 메인 운영 환경, AWS 보조 DR 환경 구성 |
| **Compute / Network** | VMSS, Application Gateway, Traffic Manager, VNet, VPC, Subnet, NSG | 3-Tier 네트워크, L7 라우팅, 장애 전환 구조 설계 |
| **Container** | Docker, Kubernetes, AKS, EKS | Web/WAS 컨테이너 배포, Service/Ingress 구성 |
| **IaC** | Terraform | Azure 인프라 모듈화, Remote State, Secret 분리 |
| **CI/CD** | GitHub Actions, ArgoCD | Docker Image Build, ACR/ECR Push, GitOps 배포 |
| **DB / Cache** | MySQL, Azure Database for MySQL, AWS RDS, Redis | DB Failover 검증, Redis 세션 외부화 |
| **Monitoring** | Grafana, WhaTap, Slack Alert | 부하 테스트, 주요 지표 모니터링, 알림 연동 |
| **Language / Framework** | Java, Spring Boot, JSP/Servlet, JavaScript, Python | 웹 애플리케이션 구조 및 백엔드 흐름 이해 |

---

## Project Summary

| No | Project | Type | Key Point |
|---|---|---|---|
| 01 | [Multi-Cloud DR 기반 K-Beauty Commerce Platform](./projects/multi-cloud-dr.md) | Team | Azure 메인 + AWS DR, Terraform, AKS/EKS, CI/CD, Redis, HTTPS |
| 02 | [AWS EKS 기반 3-Tier Container Service](./projects/aws-eks-3tier.md) | Personal | EKS, ECR, RDS, Bastion, Secret, Deployment/Service/Ingress |
| 03 | [Azure 기반 고가용성 Web Infrastructure](./projects/azure-ha-infra.md) | Team | VMSS, Application Gateway, Auto Scaling, Multi-AZ, DB Failover |

---

## Main Architecture

![Portfolio Architecture](./images/architecture.png)

---

## Troubleshooting Archive

| Issue | Summary | Link |
|---|---|---|
| DB Failover Connection 갱신 문제 | DB DNS는 변경되었지만 애플리케이션 Connection 객체가 기존 연결을 유지한 문제 해결 | [db-failover.md](./troubleshooting/db-failover.md) |
| Redis Session 유지 문제 | Pod 변경 시 로그인 세션 유지를 위해 Redis 세션 외부화 적용 | [redis-session.md](./troubleshooting/redis-session.md) |

---

## Education & Certification

- **AI MSP 베스핀글로벌 멀티클라우드 엔지니어 부트캠프**  
  AWS, Azure, Docker, Kubernetes, Terraform, CI/CD, DR Architecture

- **빅데이터 분석서비스 개발자 과정**  
  Java, Python, JSP/Servlet, Spring, Database, Linux, AWS EC2 배포

- **정보처리기사**

---

## Career Background

5년간 IT 교육기관에서 Java, Spring, Database, Web, Git/GitHub, Linux, AWS EC2 배포 등을 강의하고 프로젝트를 지도했습니다.  
이전 경력은 클라우드 엔지니어에게 필요한 다음 역량으로 연결됩니다.

- 애플리케이션 구조 이해
- 문제를 설명하고 문서화하는 능력
- 팀 프로젝트 관리 및 협업 경험
- DB, WAS, 배포 흐름에 대한 이해
- 장애 상황을 단계적으로 분석하는 습관

---

## Security Notice

본 포트폴리오에는 실제 계정 ID, Access Key, Secret Key, DB Password, 개인 연락처, 주소, 생년월일을 포함하지 않습니다.

<div align="center">

# Cloud Engineer Portfolio

### 애플리케이션 구조를 이해하고, 인프라 운영 관점에서 문제를 해결하는 클라우드 엔지니어 지원자

Java/Spring 기반 웹 개발 교육과 프로젝트 운영 경험을 바탕으로  
Kubernetes, Terraform, CI/CD, Multi-Cloud DR 환경을 설계·구현하며 클라우드 엔지니어 역량을 확장하고 있습니다.

<br/>

<a href="https://cloud-sue.github.io/cloud-engineer-portfolio/"><img src="https://img.shields.io/badge/Portfolio-111111?style=for-the-badge&logo=githubpages&logoColor=white" /></a>
<a href="https://github.com/cloud-sue"><img src="https://img.shields.io/badge/GitHub-f5f1ec?style=for-the-badge&logo=github&logoColor=111111" /></a>

</div>

---

## Tech Stack

<p>
  <img src="https://img.shields.io/badge/Azure-111111?style=for-the-badge&logo=microsoftazure&logoColor=white" />
  <img src="https://img.shields.io/badge/AWS-111111?style=for-the-badge&logo=amazonaws&logoColor=white" />
  <img src="https://img.shields.io/badge/Docker-111111?style=for-the-badge&logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/Kubernetes-111111?style=for-the-badge&logo=kubernetes&logoColor=white" />
  <img src="https://img.shields.io/badge/Terraform-111111?style=for-the-badge&logo=terraform&logoColor=white" />
  <img src="https://img.shields.io/badge/GitHub_Actions-111111?style=for-the-badge&logo=githubactions&logoColor=white" />
  <img src="https://img.shields.io/badge/ArgoCD-111111?style=for-the-badge&logo=argo&logoColor=white" />
  <img src="https://img.shields.io/badge/Java-111111?style=for-the-badge&logo=openjdk&logoColor=white" />
  <img src="https://img.shields.io/badge/Spring_Boot-111111?style=for-the-badge&logo=springboot&logoColor=white" />
  <img src="https://img.shields.io/badge/MySQL-111111?style=for-the-badge&logo=mysql&logoColor=white" />
  <img src="https://img.shields.io/badge/Redis-111111?style=for-the-badge&logo=redis&logoColor=white" />
  <img src="https://img.shields.io/badge/Linux-111111?style=for-the-badge&logo=linux&logoColor=white" />
</p>

| Category | Experience |
|---|---|
| **Cloud** | Azure 메인 운영 환경, AWS 보조 DR 환경 구성 |
| **Container** | AKS/EKS 기반 Web/WAS 컨테이너 배포, Service/Ingress 구성 |
| **IaC** | Terraform 모듈화, Remote State, 환경 변수·Secret 분리 |
| **CI/CD** | GitHub Actions 기반 Build/Push, ArgoCD 기반 GitOps 배포 |
| **Network** | VNet/VPC, Subnet, NSG, Application Gateway, Traffic Manager 설계 |
| **DB/Cache** | MySQL, Azure Database for MySQL, AWS RDS, Redis 세션 외부화 |
| **Monitoring** | Grafana, WhaTap, Slack Alert 기반 모니터링 및 알림 구성 |
| **Backend** | Java/Spring, JSP/Servlet, DB 구조 이해 기반 인프라 문제 분석 |

---

## Core Competency

<table>
  <tr>
    <td width="33%">
      <h3>Cloud Architecture</h3>
      <p>Azure/AWS 기반 3-Tier, 고가용성, 멀티클라우드 DR 아키텍처 설계 및 구현</p>
    </td>
    <td width="33%">
      <h3>Kubernetes Operation</h3>
      <p>AKS/EKS 환경에서 Web/WAS 컨테이너 배포, Service, Ingress, Probe, HPA 구성</p>
    </td>
    <td width="33%">
      <h3>IaC & Automation</h3>
      <p>Terraform 모듈화, GitHub Actions, ArgoCD를 활용한 인프라/배포 자동화</p>
    </td>
  </tr>
  <tr>
    <td width="33%">
      <h3>Troubleshooting</h3>
      <p>DB Failover, Redis Session, Secret 주입, 배포/인증 오류 원인 분석 및 해결</p>
    </td>
    <td width="33%">
      <h3>Application Understanding</h3>
      <p>Java/Spring, DB, WAS, 배포 흐름 이해를 기반으로 인프라-워크로드 문제 연결</p>
    </td>
    <td width="33%">
      <h3>Documentation</h3>
      <p>설계 이유, 장애 원인, 해결 과정, 회고를 문서화하여 설명 가능한 포트폴리오 구성</p>
    </td>
  </tr>
</table>

---

## Project Summary

| No | Project | Type | Key Point |
|---|---|---|---|
| 01 | [Multi-Cloud DR 기반 K-Beauty Commerce Platform](./projects/pj3_multi-cloud-dr.md) | Team | Azure 메인 + AWS DR, Terraform, AKS/EKS, CI/CD, Redis, HTTPS |
| 02 | [AWS EKS 기반 3-Tier Container Service](./projects/pj2_aws-eks-3tier.md) | Personal | EKS, ECR, RDS, Bastion, Secret, Deployment/Service/Ingress |
| 03 | [Azure 기반 고가용성 Web Infrastructure](./projects/pj1_azure-ha-infra.md) | Team | VMSS, Application Gateway, Auto Scaling, Multi-AZ, DB Failover |

---

## Main Project

### Multi-Cloud DR 기반 K-Beauty Commerce Platform

> Azure를 메인 운영 환경으로, AWS를 보조 DR 환경으로 구성한 멀티클라우드 기반 커머스 서비스 운영 프로젝트입니다.

![Multi-Cloud DR Architecture](./images/architecture.png)

**Key Results**

| RTO (평균) | RPO | DR 훈련 달성 | Terraform 모듈 |
|:---:|:---:|:---:|:---:|
| **33분** (목표 대비 -45%) | **0분** (DMS CDC 실시간 복제) | **4/5** 회차 | **11개** |

**My Role**

- K-Beauty 홈페이지 설계 및 구현
- Terraform 기반 Azure 인프라 구현
- Kubernetes Blue/Green + Canary 배포 구성
- Redis 기반 세션 외부화 적용
- GitHub Actions + ArgoCD 기반 CI/CD 구성
- HTTPS 인증서 적용 및 만료 알림 구현

**Why this project matters**

단일 클라우드 장애 시 서비스 전체가 중단되는 문제를 줄이기 위해 Azure-AWS 이중 구조를 설계했습니다.  
Terraform, Kubernetes, CI/CD, Redis, HTTPS를 개별 기술이 아니라 **운영 흐름**으로 연결한 것이 핵심입니다.

[프로젝트 상세 보기](./projects/pj3_multi-cloud-dr.md)

---

## Troubleshooting Archive

| Issue | Summary | Link |
|---|---|---|
| HTTPS 접속 실패 (인증서 버전 참조 불일치) | App Gateway가 삭제된 Key Vault secret version을 참조해 TLS handshake가 실패한 문제 진단·조치·재발 방지 | [https-cert-mismatch.md](./troubleshooting/https-cert-mismatch.md) |
| Redis Session 유지 문제 | Pod 변경 시 로그인 세션 유지를 위한 Redis 외부화, 이어진 502·OOMKilled까지 연쇄 해결 | [redis-session.md](./troubleshooting/redis-session.md) |
| DB Failover Connection 갱신 문제 | DB DNS는 변경되었지만 애플리케이션 Connection 객체가 기존 연결을 유지한 문제 해결 | [db-failover.md](./troubleshooting/db-failover.md) |

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
이 경험은 클라우드 엔지니어에게 필요한 다음 역량으로 연결됩니다.

- 애플리케이션 구조 이해
- 문제를 설명하고 문서화하는 능력
- 팀 프로젝트 관리 및 협업 경험
- DB, WAS, 배포 흐름에 대한 이해
- 장애 상황을 단계적으로 분석하는 습관

---

## Security Notice

본 포트폴리오에는 실제 계정 ID, Access Key, Secret Key, DB Password, 개인 연락처, 주소, 생년월일을 포함하지 않습니다.

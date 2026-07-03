---
title: Cloud Engineer Portfolio
---

<link rel="stylesheet" href="./assets/style.css">

<div class="shell top-nav">
  <div class="logo">Cloud Engineer Portfolio</div>
  <div class="nav-links">
    <a href="#skills">Skills</a>
    <a href="#projects">Projects</a>
    <a href="#troubleshooting">Troubleshooting</a>
  </div>
</div>

<div class="marquee">
  <span>AZURE · AWS · KUBERNETES · TERRAFORM · GITHUB ACTIONS · ARGOCD · REDIS · MYSQL · DEVOPS</span>
  <span>AZURE · AWS · KUBERNETES · TERRAFORM · GITHUB ACTIONS · ARGOCD · REDIS · MYSQL · DEVOPS</span>
</div>

<main class="shell">
  <section class="hero">
    <div class="eyebrow">CLOUD ENGINEER / DEVOPS PORTFOLIO</div>
    <h1>Application을 이해하는<br/>Cloud Engineer</h1>
    <p class="lead">
      Java/Spring 기반 웹 개발 교육과 프로젝트 운영 경험을 바탕으로, Kubernetes · Terraform · CI/CD · Multi-Cloud DR 환경을 설계하고 운영하는 클라우드 엔지니어 포트폴리오입니다.
    </p>
    <div class="btn-row" style="margin-top:32px;">
      <a class="btn btn-primary" href="./projects/multi-cloud-dr.html">대표 프로젝트 보기</a>
      <a class="btn btn-secondary" href="https://github.com/your-github-id">GitHub</a>
    </div>
  </section>

  <section class="color-block lime" id="skills">
    <div class="eyebrow">SKILL ICON BOARD</div>
    <h2 class="section-title">기술을 나열하지 않고,<br/>운영 경험으로 증명합니다.</h2>
    <p class="lead">
      클라우드, 컨테이너, IaC, CI/CD, DB/Cache, 모니터링, 백엔드 이해를 하나의 운영 흐름으로 연결했습니다.
    </p>
    <div class="skill-board">
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/microsoftazure/000000" alt="Azure">Azure</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/amazonaws/000000" alt="AWS">AWS</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/docker/000000" alt="Docker">Docker</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/kubernetes/000000" alt="Kubernetes">Kubernetes</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/terraform/000000" alt="Terraform">Terraform</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/githubactions/000000" alt="GitHub Actions">GitHub Actions</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/argo/000000" alt="ArgoCD">ArgoCD</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/openjdk/000000" alt="Java">Java</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/springboot/000000" alt="Spring Boot">Spring Boot</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/mysql/000000" alt="MySQL">MySQL</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/redis/000000" alt="Redis">Redis</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/grafana/000000" alt="Grafana">Grafana</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/linux/000000" alt="Linux">Linux</span>
      <span class="skill-pill"><img src="https://cdn.simpleicons.org/git/000000" alt="Git">Git</span>
    </div>
  </section>

  <section class="section">
    <h2 class="section-title">Core Competency</h2>
    <div class="grid grid-3">
      <div class="card soft-card">
        <h3>Cloud Architecture</h3>
        <p>Azure/AWS 기반 3-Tier, 고가용성, 멀티클라우드 DR 아키텍처 설계 및 구현</p>
      </div>
      <div class="card soft-card">
        <h3>Kubernetes Operation</h3>
        <p>AKS/EKS 환경에서 Web/WAS 컨테이너 배포, Service, Ingress, Probe, HPA 구성</p>
      </div>
      <div class="card soft-card">
        <h3>IaC & Automation</h3>
        <p>Terraform 모듈화, Remote State, GitHub Actions, ArgoCD 기반 자동화 경험</p>
      </div>
      <div class="card soft-card">
        <h3>Troubleshooting</h3>
        <p>DB Failover, Redis Session, Secret 주입, 배포/인증 오류 원인 분석 및 해결</p>
      </div>
      <div class="card soft-card">
        <h3>Application Understanding</h3>
        <p>Java/Spring, DB, WAS, 배포 흐름 이해를 기반으로 인프라-워크로드 문제 연결</p>
      </div>
      <div class="card soft-card">
        <h3>Documentation</h3>
        <p>설계 이유, 장애 원인, 해결 과정, 회고를 문서화하여 설명 가능한 포트폴리오 구성</p>
      </div>
    </div>
  </section>

  <section class="color-block lilac" id="projects">
    <div class="eyebrow">MAIN PROJECT</div>
    <h2 class="section-title">Multi-Cloud DR 기반<br/>K-Beauty Commerce Platform</h2>
    <p class="lead">
      Azure를 메인 운영 환경으로, AWS를 보조 DR 환경으로 구성한 멀티클라우드 커머스 서비스 운영 프로젝트입니다.
    </p>
    <div class="arch-frame" style="margin-top:32px;">
      <img src="./images/architecture.png" alt="Multi-Cloud DR Architecture">
    </div>
    <div class="btn-row" style="margin-top:28px;">
      <a class="btn btn-primary" href="./projects/multi-cloud-dr.html">상세 보기</a>
      <a class="btn btn-secondary" href="./troubleshooting/redis-session.html">Redis Session TroubleShooting</a>
    </div>
  </section>

  <section class="section">
    <h2 class="section-title">Project Cards</h2>
    <div class="grid grid-3">
      <div class="card">
        <div class="project-number">Project 01 · Team</div>
        <h3>Multi-Cloud DR</h3>
        <p>Azure 메인 + AWS DR, Terraform, AKS/EKS, CI/CD, Redis, HTTPS</p>
        <a class="btn btn-primary" href="./projects/multi-cloud-dr.html">Read More</a>
      </div>
      <div class="card">
        <div class="project-number">Project 02 · Personal</div>
        <h3>AWS EKS 3-Tier</h3>
        <p>EKS, ECR, RDS, Bastion, Secret, Deployment/Service/Ingress 기반 컨테이너 운영</p>
        <a class="btn btn-primary" href="./projects/aws-eks-3tier.html">Read More</a>
      </div>
      <div class="card">
        <div class="project-number">Project 03 · Team</div>
        <h3>Azure HA Infra</h3>
        <p>VMSS, Application Gateway, Auto Scaling, Multi-AZ, DB Failover 검증</p>
        <a class="btn btn-primary" href="./projects/azure-ha-infra.html">Read More</a>
      </div>
    </div>
  </section>

  <section class="color-block navy" id="troubleshooting">
    <div class="eyebrow">TROUBLESHOOTING</div>
    <h2 class="section-title">장애를 숨기지 않고,<br/>원인과 해결 과정을 설명합니다.</h2>
    <div class="grid grid-2">
      <div class="card">
        <h3>DB Failover Connection 갱신 문제</h3>
        <p>DB DNS는 변경되었지만 애플리케이션 Connection 객체가 기존 연결을 유지한 문제를 DataSource 설정으로 해결했습니다.</p>
        <a class="btn btn-secondary" href="./troubleshooting/db-failover.html">문서 보기</a>
      </div>
      <div class="card">
        <h3>Redis Session 유지 문제</h3>
        <p>Pod 변경 시 로그인 세션이 끊길 수 있는 문제를 Redis 세션 외부화와 Key Vault Secret 주입으로 해결했습니다.</p>
        <a class="btn btn-secondary" href="./troubleshooting/redis-session.html">문서 보기</a>
      </div>
    </div>
  </section>

  <section class="color-block coral">
    <div class="eyebrow">CAREER BACKGROUND</div>
    <h2 class="section-title">웹 개발 교육 5년의 경험을<br/>클라우드 운영 역량으로 연결합니다.</h2>
    <p class="lead">
      Java, Spring, Database, Git/GitHub, Linux, AWS EC2 배포를 강의하고 프로젝트를 지도하며 애플리케이션 구조와 배포 흐름을 설명해왔습니다. 이 경험을 바탕으로 인프라 문제를 워크로드 관점까지 함께 분석합니다.
    </p>
  </section>

  <footer class="footer">
    PUBLIC PORTFOLIO · NO SECRET · NO ACCESS KEY · NO PASSWORD · NO PERSONAL CONTACT INFO
  </footer>
</main>

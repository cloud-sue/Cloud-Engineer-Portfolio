---
title: Multi-Cloud DR Project
---

<link rel="stylesheet" href="../assets/style.css">

<div class="shell top-nav">
  <div class="logo">Project 01</div>
  <div class="nav-links"><a href="../index.html">Home</a><a href="../README.md">README</a></div>
</div>

<main class="shell">

<section class="hero">
  <div class="eyebrow">TEAM PROJECT · MULTI-CLOUD DR</div>
  <h1>Multi-Cloud DR 기반<br/>K-Beauty Commerce Platform</h1>
  <p class="lead">Azure를 메인 운영 환경으로, AWS를 보조 DR 환경으로 구성한 멀티클라우드 기반 커머스 서비스 운영 프로젝트입니다.</p>
</section>

<section class="color-block lilac">
  <div class="eyebrow">PROJECT OVERVIEW</div>
  <div class="grid grid-2">
    <div>
      <h2 class="section-title">Azure Main<br/>AWS DR</h2>
      <p>단일 클라우드 장애 시 서비스 전체가 중단되는 SPOF 문제를 줄이기 위해 Azure 장애 발생 시 AWS 보조 환경으로 전환 가능한 DR 구조를 설계했습니다.</p>
    </div>
    <div class="card">
      <h3>Project Info</h3>
      <ul>
        <li><strong>기간</strong>: 2026.06.01 ~ 2026.07.01</li>
        <li><strong>팀 규모</strong>: 3인</li>
        <li><strong>담당 역할</strong>: Azure CSP · 인프라/운영/배포</li>
        <li><strong>키워드</strong>: Azure, AWS, Terraform, AKS, EKS, ArgoCD, Redis, HTTPS</li>
      </ul>
    </div>
  </div>
</section>

<section class="section">
  <h2 class="section-title">Architecture</h2>
  <div class="arch-frame"><img src="../images/architecture.png" alt="Multi-Cloud DR Architecture"></div>
</section>

<section class="section">
  <h2 class="section-title">My Role</h2>
  <div class="grid grid-3">
    <div class="card soft-card"><h3>Terraform</h3><p>역할별 11개 모듈 구조로 Azure 인프라를 코드화하고 Remote State로 팀 상태를 공유했습니다.</p></div>
    <div class="card soft-card"><h3>Kubernetes</h3><p>Blue/Green + /canary 경로 검증 방식으로 무중단 배포와 빠른 롤백이 가능한 구조를 구성했습니다.</p></div>
    <div class="card soft-card"><h3>Redis Session</h3><p>Pod 변경 이후에도 로그인 세션이 유지되도록 Redis 기반 세션 외부화를 적용했습니다.</p></div>
    <div class="card soft-card"><h3>CI/CD</h3><p>GitHub Actions로 이미지 빌드 및 ACR/ECR Push, ArgoCD로 GitOps 배포 흐름을 구성했습니다.</p></div>
    <div class="card soft-card"><h3>HTTPS</h3><p>인증서 적용과 만료 알림 구조를 구성해 운영 안정성을 높였습니다.</p></div>
    <div class="card soft-card"><h3>Application</h3><p>K-Beauty 홈페이지를 설계·구현하고 인프라와 애플리케이션 흐름을 연결했습니다.</p></div>
  </div>
</section>

<section class="color-block cream">
  <div class="eyebrow">DESIGN DECISION</div>
  <h2 class="section-title">왜 이 기술을 선택했는가</h2>
  <div class="grid grid-2">
    <div class="card"><h3>Multi-Cloud DR</h3><p>커머스 서비스는 주문·결제 흐름이 중요하기 때문에 Azure 장애 시 AWS로 전환해 서비스 연속성과 데이터 보호를 확보하는 구조를 선택했습니다.</p></div>
    <div class="card"><h3>Terraform</h3><p>수동 구성의 환경 차이를 줄이고, 보조 환경에도 동일한 인프라를 재현하기 위해 IaC를 선택했습니다.</p></div>
    <div class="card"><h3>Blue/Green + Canary</h3><p>운영 중 배포 리스크를 줄이기 위해 신규 버전을 /canary 경로로 검증한 뒤 selector 전환 방식으로 운영 트래픽을 전환했습니다.</p></div>
    <div class="card"><h3>Redis Session</h3><p>Pod 재시작이나 스케일링 이후에도 사용자의 로그인 상태가 유지되도록 세션을 외부화했습니다.</p></div>
  </div>
</section>

<section class="section">
  <h2 class="section-title">CI/CD Flow</h2>
  <div class="code-like">Code Push / PR → GitHub Actions → Build & Test → Docker Image Build → Security Scan → ACR/ECR Push → GitOps Repo Image Tag Update → ArgoCD Sync → AKS/EKS Deploy</div>
</section>

<section class="color-block navy">
  <div class="eyebrow">TROUBLESHOOTING</div>
  <h2 class="section-title">Redis 세션 유지 검증</h2>
  <div class="grid grid-2">
    <div class="card"><h3>Problem</h3><p>기본 Pod 메모리 세션 사용 시 요청이 다른 Pod로 분산되면 로그인 세션이 유지되지 않을 수 있었습니다.</p></div>
    <div class="card"><h3>Solution</h3><p>Spring Session 설정을 Redis로 변경하고, Redis 접속 정보는 Key Vault와 External Secrets Operator를 통해 Kubernetes Secret으로 주입했습니다.</p></div>
  </div>
  <div class="btn-row" style="margin-top:28px;"><a class="btn btn-secondary" href="../troubleshooting/redis-session.html">Redis 문서 보기</a></div>
</section>

<footer class="footer">BACK TO <a href="../index.html">PORTFOLIO HOME</a></footer>

</main>

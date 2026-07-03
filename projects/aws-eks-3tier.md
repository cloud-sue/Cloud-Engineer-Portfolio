---
title: AWS EKS 3-Tier Project
---

<link rel="stylesheet" href="../assets/style.css">

<div class="shell top-nav"><div class="logo">Project 02</div><div class="nav-links"><a href="../index.html">Home</a></div></div>

<main class="shell">
<section class="hero">
  <div class="eyebrow">PERSONAL PROJECT · AWS EKS</div>
  <h1>AWS EKS 기반<br/>3-Tier Container Service</h1>
  <p class="lead">EKS, ECR, RDS, Bastion, Kubernetes Secret, Deployment, Service, Ingress를 직접 구성하며 컨테이너 기반 3-Tier 운영 흐름을 학습한 개인 프로젝트입니다.</p>
</section>

<section class="color-block coral">
  <div class="eyebrow">PROJECT POINT</div>
  <h2 class="section-title">컨테이너 이미지 빌드부터<br/>EKS 배포까지 직접 구성</h2>
  <div class="grid grid-3">
    <div class="card"><h3>RDS</h3><p>MySQL Multi-AZ 구성, 퍼블릭 접근 비활성화, EKS/Bastion 접근 보안그룹 구성</p></div>
    <div class="card"><h3>ECR</h3><p>Frontend/Backend 이미지를 분리하고 Private ECR Repository에 Push</p></div>
    <div class="card"><h3>EKS</h3><p>Private Subnet 기반 EKS 클러스터, Deployment/Service/Ingress 배포</p></div>
  </div>
</section>

<section class="section"><h2 class="section-title">Architecture</h2><div class="arch-frame"><img src="../images/aws-eks-3tier-architecture.png" alt="AWS EKS 3-Tier Architecture"></div></section>

<section class="section">
  <h2 class="section-title">Implementation</h2>
  <div class="grid grid-2">
    <div class="card soft-card"><h3>Bastion Access</h3><p>AWS CLI, kubectl, EKS Access Entry를 구성해 Bastion에서 클러스터에 접근할 수 있도록 구성했습니다.</p></div>
    <div class="card soft-card"><h3>Kubernetes Secret</h3><p>DB 접속 정보를 애플리케이션 코드에 직접 넣지 않고 Secret으로 분리해 Pod에 주입했습니다.</p></div>
    <div class="card soft-card"><h3>Multi-stage Dockerfile</h3><p>빌드 단계와 런타임 단계를 분리해 최종 이미지에 불필요한 빌드 도구가 포함되지 않도록 구성했습니다.</p></div>
    <div class="card soft-card"><h3>Ingress</h3><p>Nginx Ingress Controller를 활용해 WEB/WAS 요청 흐름을 구성했습니다.</p></div>
  </div>
</section>

<footer class="footer">BACK TO <a href="../index.html">PORTFOLIO HOME</a></footer>
</main>

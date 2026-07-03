---
title: Redis Session Troubleshooting
---

<link rel="stylesheet" href="../assets/style.css">

<div class="shell top-nav"><div class="logo">Troubleshooting 02</div><div class="nav-links"><a href="../index.html">Home</a></div></div>

<main class="shell">
<section class="hero">
  <div class="eyebrow">SESSION EXTERNALIZATION</div>
  <h1>Redis 기반<br/>Session 외부화</h1>
  <p class="lead">Pod가 변경되거나 스케일링되어도 로그인 세션이 유지되도록 Redis 기반 세션 저장 구조를 적용한 경험입니다.</p>
</section>

<section class="color-block pink">
  <div class="grid grid-2">
    <div class="card"><h3>Problem</h3><p>기본 Pod 메모리 세션을 사용할 경우 요청이 다른 Pod로 분산되면 로그인 세션이 유지되지 않을 수 있었습니다.</p></div>
    <div class="card"><h3>Cause</h3><p>세션 정보가 각 WAS Pod의 메모리에 저장되어 Pod 간 공유되지 않았습니다. 무중단 배포와 스케일링 환경에서는 세션 저장소를 외부화해야 했습니다.</p></div>
    <div class="card"><h3>Action</h3><p>Spring Session Store Type을 Redis로 설정하고, Redis 접속 정보는 Azure Key Vault와 External Secrets Operator를 통해 Kubernetes Secret으로 주입했습니다.</p></div>
    <div class="card"><h3>Result</h3><p>여러 번 요청이 들어가도 동일한 세션 상태가 유지되는 것을 검증했습니다. Pod 변경 이후에도 로그인 세션이 유지되는 운영 구조를 구성했습니다.</p></div>
  </div>
</section>

<section class="section">
  <h2 class="section-title">Security Injection</h2>
  <div class="code-like">Azure Key Vault → External Secrets Operator → Kubernetes Secret → WAS Pod Environment</div>
</section>

<footer class="footer">BACK TO <a href="../index.html">PORTFOLIO HOME</a></footer>
</main>

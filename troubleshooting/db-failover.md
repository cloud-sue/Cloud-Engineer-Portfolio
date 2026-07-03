---
title: DB Failover Troubleshooting
---

<link rel="stylesheet" href="../assets/style.css">

<div class="shell top-nav"><div class="logo">Troubleshooting 01</div><div class="nav-links"><a href="../index.html">Home</a></div></div>

<main class="shell">
<section class="hero">
  <div class="eyebrow">STAR TROUBLESHOOTING</div>
  <h1>DB Failover 후<br/>Connection 갱신 문제 해결</h1>
  <p class="lead">인프라 장애가 아닌 애플리케이션 워크로드 관점까지 함께 분석해 해결한 트러블슈팅 경험입니다.</p>
</section>

<section class="color-block cream">
  <div class="grid grid-2">
    <div class="card"><h3>Situation</h3><p>Azure 기반 고가용성 웹 인프라 프로젝트에서 WAS Tier를 담당했습니다. DB Failover 테스트 중 DB Zone이 변경되었지만 화면에 표시되는 DB Host 정보가 갱신되지 않았습니다.</p></div>
    <div class="card"><h3>Task</h3><p>DB 장애가 발생해 다른 Zone의 DB로 전환되더라도 애플리케이션이 정상적으로 새 DB 연결을 사용하도록 해야 했습니다.</p></div>
    <div class="card"><h3>Action</h3><p>nslookup으로 DB DNS 변경은 확인했지만, 애플리케이션의 Connection 객체가 기존 연결을 유지하고 있다는 점을 파악했습니다. DataSource 설정을 수정해 연결 객체가 문제 상황에서 갱신되도록 개선했습니다.</p></div>
    <div class="card"><h3>Result</h3><p>DB Host 정보가 정상적으로 출력되었고, DB Failover 이후에도 애플리케이션이 안정적으로 서비스될 수 있는 구조를 검증했습니다.</p></div>
  </div>
</section>

<section class="section">
  <h2 class="section-title">Why it matters</h2>
  <div class="color-block lime">
    <p class="lead">이 경험의 핵심은 인프라가 정상적으로 Failover되더라도 애플리케이션 연결 객체가 갱신되지 않으면 서비스 장애가 계속될 수 있다는 점을 확인한 것입니다. 클라우드 운영에서는 인프라와 워크로드를 분리해서 보지 않고 함께 분석해야 합니다.</p>
  </div>
</section>

<footer class="footer">BACK TO <a href="../index.html">PORTFOLIO HOME</a></footer>
</main>

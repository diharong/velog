<h1 id="🏗️-hahigh-availability-고가용성이란">🏗️ HA(High Availability) 고가용성이란?</h1>
<h2 id="📌-hahigh-availability란">📌 HA(High Availability)란?</h2>
<p>HA(High Availability), 즉 &quot;고가용성&quot;은 <strong>시스템이나 서비스가 장애 없이 계속 운영될 수 있도록 하는 개념</strong>이다. 
서버 장애나 네트워크 문제가 생겨도 서비스가 멈추지 않게 만드는 것이 목표이다.</p>
<h3 id="11-가용성이란-🤔">1.1 가용성이란? 🤔</h3>
<p><strong>가용성(Availability)</strong>은 시스템이나 서비스가 정상적으로 작동하는 시간을 의미한다. 
쉽게 말하면, 1년 365일 중에서 <strong>몇 퍼센트의 시간 동안 서비스가 멀쩡한지</strong>를 나타내는 개념이다.</p>
<p>📊 <strong>가용성 수준 예시</strong></p>
<ul>
<li><strong>99% 가용성</strong> → 1년에 약 <strong>3.65일</strong> 동안 장애 발생 가능</li>
<li><strong>99.9% (Three Nines)</strong> → 1년에 약 <strong>8.76시간</strong> 장애 가능</li>
<li><strong>99.99% (Four Nines)</strong> → 1년에 약 <strong>52.56분</strong> 장애 가능</li>
<li><strong>99.999% (Five Nines, 고가용성 수준)</strong> → 1년에 약 <strong>5.26분</strong> 장애 가능</li>
</ul>
<p>💡 <strong>고가용성(HA)</strong>이란? 99.999%에 가까운 가용성을 유지하는 것을 목표로 한다.</p>
<hr />
<h2 id="️-ha가-왜-중요할까">⁉️ HA가 왜 중요할까?</h2>
<p>서비스가 중단되면 어떤 일이 생길까?</p>
<ul>
<li><strong>은행 앱이 멈춘다면?</strong> → 송금, 결제 불가 ❌</li>
<li><strong>온라인 쇼핑몰이 다운된다면?</strong> → 주문 불가, 매출 손실 📉</li>
<li><strong>게임 서버가 꺼진다면?</strong> → 유저 이탈 🚶‍♂️</li>
</ul>
<p>서비스가 <strong>멈추지 않도록 설계하는 것</strong>이 바로 HA다! </p>
<hr />
<h2 id="☀️-ha를-위한-핵심-기술">☀️ HA를 위한 핵심 기술</h2>
<h3 id="1-이중화redundancy">1) 이중화(Redundancy)</h3>
<p>하나의 서버만 운영하면 <strong>고장 나면 끝</strong>이다. 그래서 <strong>여러 개의 서버를 운영</strong>해 하나가 망가져도 다른 서버가 역할을 대신하도록 만든다.</p>
<ul>
<li>✅ ex. 로드 밸런서를 사용해 트래픽을 여러 서버로 분산하기</li>
</ul>
<h3 id="2-페일오버failover">2) 페일오버(Failover)</h3>
<p>서버가 죽으면 자동으로 다른 서버로 전환하는 기술이다.</p>
<ul>
<li>✅ ex. DB에서 Master-Slave 구조를 사용해 마스터 DB가 죽으면 자동으로 슬레이브 DB가 운영되도록 설정</li>
</ul>
<h3 id="3-로드-밸런싱load-balancing">3) 로드 밸런싱(Load Balancing)</h3>
<p>트래픽을 여러 서버로 분산해 한 서버에 과부하가 걸리지 않도록 하는 기술이다.</p>
<ul>
<li>✅ ex. AWS의 ELB(Elastic Load Balancer), Nginx 사용</li>
</ul>
<h3 id="4-자동-복구self-healing">4) 자동 복구(Self-Healing)</h3>
<p>시스템이 장애를 감지하면 자동으로 문제를 해결하는 기능이다.</p>
<ul>
<li>✅ ex. Kubernetes에서 컨테이너가 비정상적으로 종료되면 자동으로 새로운 컨테이너 실행</li>
</ul>
<h3 id="5-액티브-스탠바이active-standby">5) 액티브-스탠바이(Active-Standby)</h3>
<p>한 서버가 <strong>운영(Active)</strong> 상태이고, 다른 서버는 <strong>대기(Standby)</strong> 상태다. 
만약 운영 서버가 죽으면 대기 서버가 자동으로 활성화된다.</p>
<ul>
<li>✅ ex. 금융 시스템에서 <strong>메인 서버(Active)가 다운되면 백업 서버(Standby)가 자동으로 활성화되어 운영</strong></li>
</ul>
<h3 id="6-액티브-액티브active-active">6) 액티브-액티브(Active-Active)</h3>
<p>모든 서버가 동시에 운영된다. 서버 하나가 죽어도 다른 서버가 계속해서 역할을 수행한다.</p>
<ul>
<li>✅ ex. AWS에서 <strong>Multi-AZ 배포(여러 데이터센터에서 서비스 실행)</strong></li>
</ul>
<hr />
<h2 id="🦾-ha-아키텍쳐-예제">🦾 HA 아키텍쳐 예제</h2>
<p>💡 <strong>일반적인 고가용성 웹 서비스 구조</strong>
1️⃣ <strong>로드 밸런서(Nginx, HAProxy)</strong> → 요청을 여러 개의 웹 서버로 분산 
2️⃣ <strong>웹 서버(Nginx, Apache)</strong> → 여러 개의 웹 서버 운영 
3️⃣ <strong>애플리케이션 서버(Spring, Django, Node.js)</strong> → 여러 서버에서 같은 앱 실행 
4️⃣ <strong>데이터베이스 이중화(MySQL Master-Slave, PostgreSQL Replication)</strong> → DB 장애 시 자동 전환 
5️⃣ <strong>모니터링 및 장애 감지(Prometheus, Grafana, ELK 스택)</strong> → 장애 발생 시 자동 알림 
6️⃣ <strong>Active-Standby 적용</strong> → 주요 서버가 다운될 경우 Standby 서버가 운영 
7️⃣ <strong>Active-Active 적용</strong> → 여러 서버가 동시에 트래픽을 처리해 성능과 가용성 극대화 </p>
<hr />
<h2 id="⚖️-ha의-장점과-단점">⚖️ HA의 장점과 단점</h2>
<table>
<thead>
<tr>
<th>✅ <strong>장점</strong></th>
<th>❌ <strong>단점</strong></th>
</tr>
</thead>
<tbody><tr>
<td>서비스 중단 최소화</td>
<td>구축 비용 증가</td>
</tr>
<tr>
<td>고객 신뢰도 상승</td>
<td>시스템 관리 복잡도 증가</td>
</tr>
<tr>
<td>장애 발생 시 자동 복구</td>
<td>설정 및 운영 부담 증가</td>
</tr>
</tbody></table>
<hr />
<h2 id="💡-결론">💡 결론</h2>
<p><strong>고가용성(HA)이란 장애 없이 서비스를 지속적으로 운영할 수 있도록 만드는 것</strong>이다. 
기업들은 <strong>이중화, 페일오버, 로드 밸런싱, 자동 복구, Active-Standby, Active-Active</strong> 같은 기술을 활용해 안정적인 서비스를 제공한다.</p>
<p>🔥 <strong>HA를 적용하면?</strong>
✅ <strong>서비스 연속성 유지</strong> → 고객이 불편 없이 사용 가능
✅ <strong>장애 발생 시 신속한 복구</strong> → 다운타임 최소화
✅ <strong>비즈니스 신뢰도 상승</strong> → 매출 감소 방지</p>
<p>👉<strong>결론:</strong> 금융, 전자상거래, 클라우드 같은 중요한 서비스에서는 HA가 필수다</p>
<p>👉 HA를 제대로 이해하고 적용하면, 시스템이 <strong>언제나 안정적으로 운영되는 환경을 만들 수 있음‼️</strong></p>
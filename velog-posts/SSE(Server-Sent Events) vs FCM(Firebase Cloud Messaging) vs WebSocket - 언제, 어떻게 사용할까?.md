<h2 id="실시간-데이터-전송-무엇을-선택해야-할까-️">실시간 데이터 전송, 무엇을 선택해야 할까 ⁉️</h2>
<p>앱이나 웹을 개발할 때 <strong>실시간 데이터 전송</strong>이 필요한 경우가 많다. </p>
<ul>
<li>실시간 스포츠 경기 점수 업데이트 </li>
<li>채팅 서비스 </li>
<li>모바일 푸시 알림 </li>
<li>금융 데이터 실시간 업데이트 </li>
</ul>
<p>이때 사용할 수 있는 대표적인 기술이 <strong>SSE(Server-Sent Events)</strong>, <strong>FCM(Firebase Cloud Messaging)</strong>, 그리고 <strong>WebSocket</strong>이 있다. </p>
<p>✅ <strong>SSE</strong>는 서버에서 클라이언트로 데이터를 지속적으로 보내는 방식이며, 주로 <strong>실시간 웹 업데이트</strong>에 사용.
✅ <strong>FCM</strong>은 Firebase를 이용한 <strong>푸시 알림 서비스</strong>로, 웹과 모바일 모두에서 사용 능.
✅ <strong>WebSocket</strong>은 서버와 클라이언트가 <strong>양방향으로 데이터를 주고받을 수 있는</strong> 실시간 통신 기술.</p>
<p>이제 세 가지 기술을 비교해보자.</p>
<hr />
<p>그 전에 Firebase 의 개념부터 알고가자.</p>
<h2 id="🔥-firebase란">🔥 Firebase란?</h2>
<h3 id="✅-firebase-개념">✅ Firebase 개념</h3>
<blockquote>
<p><strong>Firebase(파이어베이스)</strong>는 Google에서 제공하는 <strong>클라우드 기반 백엔드 서비스 플랫폼</strong>. </p>
</blockquote>
<p>쉽게 말하면, <strong>앱 개발에 필요한 서버 기능을 쉽게 사용할 수 있도록 도와주는 서비스</strong>이다.</p>
<p>보통 앱을 개발할 때 <strong>데이터베이스, 사용자 인증, 푸시 알림, 파일 저장</strong> 같은 기능이 필요한데,<br />이런 기능들을 직접 개발하지 않고 <strong>Firebase를 이용하면 간편하게 구현</strong>할 수 있다.</p>
<h3 id="✅-firebase의-주요-기능">✅ Firebase의 주요 기능</h3>
<table>
<thead>
<tr>
<th>기능</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Authentication (인증)</strong></td>
<td>이메일, 구글, 페이스북, 애플 로그인 같은 <strong>사용자 로그인 기능</strong> 제공</td>
</tr>
<tr>
<td><strong>Firestore / Realtime Database</strong></td>
<td><strong>클라우드 데이터베이스</strong> (NoSQL 기반)</td>
</tr>
<tr>
<td><strong>Firebase Cloud Messaging (FCM)</strong></td>
<td><strong>푸시 알림 전송</strong> 기능</td>
</tr>
<tr>
<td><strong>Cloud Storage</strong></td>
<td>사진, 동영상 등 <strong>파일 저장</strong></td>
</tr>
<tr>
<td><strong>Hosting</strong></td>
<td>웹사이트를 Firebase 서버에서 <strong>배포 가능</strong></td>
</tr>
<tr>
<td><strong>Analytics</strong></td>
<td>앱 사용 통계를 자동으로 수집</td>
</tr>
</tbody></table>
<p>Firebase를 이용하면 <strong>백엔드 서버를 직접 구축하지 않고도 다양한 기능을 활용할 수 있기 때문에</strong>,  
특히 <strong>모바일 앱이나 웹 개발</strong>에서 아주 유용하다!</p>
<hr />
<h2 id="🔄-sseserver-sent-events란">🔄 SSE(Server-Sent Events)란?</h2>
<h3 id="✅-sse-개념">✅ SSE 개념</h3>
<blockquote>
<p><strong>SSE(Server-Sent Events)</strong>는 <strong>서버가 클라이언트(브라우저)로 지속적으로 데이터를 전송하는 단방향 통신 기술</strong>. </p>
</blockquote>
<p>HTTP 연결을 유지하면서 <strong>서버가 필요할 때마다 데이터를 푸시</strong>한다.</p>
<h3 id="✅-sse-동작-방식">✅ SSE 동작 방식</h3>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/54a4d570-2737-47d3-a2b3-1e3feb8430a7/image.png" /></p>
<ol>
<li>클라이언트(브라우저)가 서버에 연결 (<code>EventSource</code> 객체 사용)</li>
<li>서버는 HTTP 연결을 유지하며 데이터를 전송</li>
<li>클라이언트가 데이터를 받아 화면을 업데이트</li>
<li>연결이 끊기면 자동으로 재연결 </li>
</ol>
<h3 id="✅-sse의-장점--단점">✅ SSE의 장점 &amp; 단점</h3>
<p>✔ <strong>장점</strong></p>
<ul>
<li>단순한 HTTP 기반으로 구현이 쉬움</li>
<li>브라우저에서 기본 지원 (별도 라이브러리 불필요)</li>
<li>자동 재연결 기능 제공</li>
</ul>
<p>❌ <strong>단점</strong></p>
<ul>
<li>서버에서 클라이언트로 <strong>단방향 통신</strong>만 가능</li>
<li>다수의 연결이 발생하면 서버 부담 증가</li>
<li>모바일 앱에서 사용하기 어려움 (브라우저 전용)</li>
</ul>
<hr />
<h2 id="📩-fcmfirebase-cloud-messaging이란">📩 FCM(Firebase Cloud Messaging)이란?</h2>
<h3 id="✅-fcm-개념">✅ FCM 개념</h3>
<blockquote>
<p><strong>FCM(Firebase Cloud Messaging)</strong>은 Google Firebase에서 제공하는 <strong>모바일 및 웹 푸시 알림 서비스</strong>. </p>
</blockquote>
<h3 id="✅-fcm-동작-방식">✅ FCM 동작 방식</h3>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/fe595c22-bc29-4dd5-91e5-96dc70e36f13/image.png" /></p>
<ol>
<li>클라이언트(앱, 웹)가 Firebase 서버에서 <strong>FCM 토큰</strong>을 발급받음</li>
<li>서버에서 Firebase에 &quot;이 사용자에게 메시지를 보내라&quot; 요청</li>
<li>Firebase가 사용자의 기기로 <strong>푸시 메시지 전송</strong></li>
<li>사용자는 앱이 꺼져 있어도 알림을 받을 수 있음</li>
</ol>
<h3 id="✅-fcm의-장점--단점">✅ FCM의 장점 &amp; 단점</h3>
<p>✔ <strong>장점</strong></p>
<ul>
<li><strong>웹, 모바일 모두 지원</strong> </li>
<li><strong>백그라운드에서도 작동 가능</strong> (앱이 꺼져도 알림 수신 가능)</li>
<li>양방향 통신 가능 (클라이언트 → 서버도 가능)</li>
</ul>
<p>❌ <strong>단점</strong></p>
<ul>
<li>Google Firebase에 종속됨 </li>
<li>네트워크 상태가 안 좋으면 푸시 알림이 늦게 도착할 수 있음</li>
</ul>
<hr />
<h2 id="🌐-websocket이란">🌐 WebSocket이란?</h2>
<h3 id="✅-websocket-개념">✅ WebSocket 개념</h3>
<blockquote>
<p><strong>WebSocket</strong>은 <strong>클라이언트와 서버가 실시간으로 양방향 통신을 할 수 있도록 지원하는 프로토콜</strong>.  </p>
</blockquote>
<p>HTTP 기반이 아니라, <strong>한 번 연결이 맺어지면 지속적으로 데이터를 주고받을 수 있는 방식</strong>이다.</p>
<h3 id="✅-websocket-동작-방식">✅ WebSocket 동작 방식</h3>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/4d2f94a7-c1fc-48a9-95c6-7eab19b85bf5/image.png" /></p>
<ol>
<li>클라이언트가 서버와 WebSocket 연결을 수립</li>
<li>연결이 유지된 상태에서 서버와 클라이언트가 <strong>자유롭게 데이터를 주고받을 수 있음</strong></li>
<li>연결을 유지하면서 채팅, 알림, 실시간 데이터 업데이트 가능</li>
</ol>
<h3 id="✅-websocket-코드-예제">✅ WebSocket 코드 예제</h3>
<h4 id="📌-서버nodejs--websocket">📌 서버(Node.js + WebSocket)</h4>
<pre><code class="language-javascript">const WebSocket = require('ws');
const server = new WebSocket.Server({ port: 8080 });

server.on('connection', ws =&gt; {
    console.log('새로운 클라이언트 연결됨');
    ws.send('서버에서 클라이언트로 메시지 전송');
    ws.on('message', message =&gt; {
        console.log(`클라이언트 메시지: ${message}`);
    });
});</code></pre>
<h4 id="📌-클라이언트javascript">📌 클라이언트(JavaScript)</h4>
<pre><code class="language-javascript">const socket = new WebSocket('ws://localhost:8080');

socket.onmessage = (event) =&gt; {
    console.log('서버 메시지:', event.data);
};

socket.onopen = () =&gt; {
    socket.send('클라이언트에서 서버로 메시지 전송');
};</code></pre>
<h3 id="✅-websocket의-장점--단점">✅ WebSocket의 장점 &amp; 단점</h3>
<p>✔ <strong>장점</strong></p>
<ul>
<li><strong>양방향 통신 가능</strong> (서버 ↔ 클라이언트)</li>
<li><strong>빠른 데이터 전송</strong> (HTTP보다 가벼운 프로토콜)</li>
<li>실시간 채팅, 주식 거래, 게임 등 <strong>빠른 응답이 필요한 서비스에 적합</strong></li>
</ul>
<p>❌ <strong>단점</strong></p>
<ul>
<li><strong>브라우저 지원 필요</strong> (일부 환경에서 제한될 수 있음)</li>
<li>연결이 많아지면 서버 부하 증가 가능</li>
</ul>
<hr />
<h2 id="sse-🆚-fcm-🆚--websocket">SSE 🆚 FCM 🆚  WebSocket</h2>
<table>
<thead>
<tr>
<th>비교 항목</th>
<th>SSE (Server-Sent Events)</th>
<th>FCM (Firebase Cloud Messaging)</th>
<th>WebSocket</th>
</tr>
</thead>
<tbody><tr>
<td><strong>통신 방식</strong></td>
<td><strong>단방향</strong> (서버 → 클라이언트)</td>
<td><strong>단방향</strong> (서버 → 클라이언트)</td>
<td><strong>양방향</strong> (서버 ↔ 클라이언트)</td>
</tr>
<tr>
<td><strong>사용 목적</strong></td>
<td>실시간 데이터 스트리밍</td>
<td>푸시 알림, 메시지 전송</td>
<td>채팅, 게임, 실시간 데이터 공유</td>
</tr>
<tr>
<td><strong>웹 지원</strong></td>
<td>브라우저에서 가능</td>
<td>웹, 모바일 지원</td>
<td>웹, 모바일 지원</td>
</tr>
<tr>
<td><strong>앱 지원</strong></td>
<td>❌ (웹 전용)</td>
<td>✅ (모바일, 웹 지원)</td>
<td>✅ (모바일, 웹 지원)</td>
</tr>
<tr>
<td><strong>백그라운드 작동</strong></td>
<td>❌ (탭을 닫으면 끊김)</td>
<td>✅ (앱이 꺼져도 알림 가능)</td>
<td>❌ (백그라운드에서 유지 어려움)</td>
</tr>
<tr>
<td><strong>Google 종속 여부</strong></td>
<td>❌ (독립적)</td>
<td>✅ (Google Firebase 사용)</td>
<td>❌ (독립적)</td>
</tr>
</tbody></table>
<hr />
<h2 id="🤷-언제-sse-fcm-websocket을-사용해야-할까">🤷‍ 언제 SSE, FCM, WebSocket을 사용해야 할까?</h2>
<h3 id="✅-sse를-사용해야-하는-경우">✅ <strong>SSE를 사용해야 하는 경우</strong></h3>
<ul>
<li>실시간 데이터 스트리밍이 필요한 경우 (주식, 스포츠 경기 점수 등) </li>
<li>브라우저에서 서버 데이터를 지속적으로 받아야 할 때 </li>
<li>외부 서비스(Firebase) 없이 자체 서버를 운영하고 싶을 때</li>
</ul>
<h3 id="✅-fcm을-사용해야-하는-경우">✅ <strong>FCM을 사용해야 하는 경우</strong></h3>
<ul>
<li><strong>모바일 푸시 알림</strong>이 필요한 경우 </li>
<li>앱이 꺼져 있어도 <strong>알림을 보내야 할 때</strong></li>
<li>웹과 모바일을 모두 지원해야 할 때 </li>
</ul>
<h3 id="✅-websocket을-사용해야-하는-경우">✅ <strong>WebSocket을 사용해야 하는 경우</strong></h3>
<ul>
<li><strong>실시간 채팅</strong> 기능이 필요할 때 💬</li>
<li><strong>게임, 주식 거래 시스템</strong>과 같이 빠른 응답이 필요한 경우 </li>
<li>서버와 클라이언트가 <strong>양방향으로 데이터를 주고받아야 할 때</strong></li>
</ul>
<hr />
<h2 id="💡결론">💡결론</h2>
<ul>
<li><strong>SSE는 실시간 데이터 스트리밍</strong>에 적합하지만, 브라우저에서만 동작하고 단방향 통신만 가능</li>
<li><strong>FCM은 푸시 알림을 위한 서비스</strong>로, 모바일과 웹에서 모두 사용 가능하며 백그라운드에서도 작동</li>
<li><strong>WebSocket은 실시간 양방향 통신</strong>이 필요한 경우에 적합하며, 채팅, 주식 거래, 게임 등에 많이 사용됨</li>
<li><strong>사용 목적에 따라 적절한 기술을 선택하는 것이 중요!</strong> </li>
</ul>
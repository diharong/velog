<p>웹 애플리케이션을 개발하면서 인증 방식을 고민했던 적이 많다. 처음에는 단순히 &quot;JWT가 트렌드니까 써야지!&quot;라고 생각했지만, 막상 프로젝트를 진행하면서 쿠키, 세션, 토큰 각각의 장단점을 직접 체감하게 됐다. 그리고 이 모든 것의 시작은 바로 <strong>HTTP의 특징</strong>에서 비롯된다는 걸 알게 되었다.</p>
<h2 id="📌http의-특징과-인증이-필요한-이유">📌HTTP의 특징과 인증이 필요한 이유</h2>
<p>HTTP는 <strong>Stateless(무상태성) 프로토콜</strong>이다. 즉, <strong>서버는 이전 요청을 기억하지 않는다.</strong></p>
<p>이게 무슨 의미냐면, 사용자가 로그인했다고 해서 다음 요청에서도 사용자를 인식할 수 있는 것이 아니라는 것이다. 따라서 <strong>사용자의 상태를 유지하기 위해 쿠키, 세션, 토큰 같은 인증 방식이 필요</strong>하다.</p>
<p>이제 각각의 방식이 HTTP와 어떻게 연관되는지 살펴보자.</p>
<hr />
<h2 id="1️⃣-쿠키cookie---클라이언트에-저장되는-작은-정보">1️⃣ 쿠키(Cookie) - 클라이언트에 저장되는 작은 정보</h2>
<p>쿠키는 <strong>클라이언트(브라우저)에 저장되는 작은 데이터</strong>다. HTTP는 기본적으로 상태를 유지하지 않지만, <strong>쿠키를 이용하면 서버가 사용자의 로그인 상태를 기억할 수 있다.</strong></p>
<p>✅ <strong>쿠키의 HTTP 연관성</strong></p>
<ul>
<li>서버는 <code>Set-Cookie</code> 응답 헤더를 통해 클라이언트에게 쿠키를 저장하도록 요청함.</li>
<li>이후 클라이언트가 요청을 보낼 때 <code>Cookie</code> 헤더에 자동으로 쿠키를 포함하여 전송함.</li>
</ul>
<p>✅ <strong>쿠키가 유용했던 경우</strong></p>
<ul>
<li>자동 로그인 기능을 추가할 때</li>
<li>클라이언트에서 작은 설정값 (예: 다크 모드, 언어 설정)을 저장할 때</li>
</ul>
<p>❌ <strong>BUT ❌ 이런 문제가 있었다!</strong></p>
<ul>
<li>쿠키는 클라이언트에서 직접 수정이 가능해서 보안이 걱정됐다.</li>
<li>모든 요청에 쿠키가 포함되다 보니, 트래픽이 쌓일수록 부담이 될 수도 있었다.</li>
<li>CSRF(크로스 사이트 요청 위조) 공격에 취약할 수 있어서 <code>HttpOnly</code>, <code>Secure</code>, <code>SameSite</code> 설정이 필요했다.</li>
</ul>
<hr />
<h2 id="2️⃣-세션session---서버에서-사용자-상태-관리">2️⃣ 세션(Session) - 서버에서 사용자 상태 관리</h2>
<p>세션은 <strong>사용자의 로그인 정보를 서버에서 직접 관리하는 방식</strong>이다. 
쿠키와 차이점은, <strong>클라이언트에는 오직 세션 ID만 저장되고, 실제 사용자 정보는 서버에서 관리한다는 점</strong>이다.</p>
<p>✅ <strong>세션의 HTTP 연관성</strong></p>
<ul>
<li>사용자가 로그인하면 서버는 세션을 생성하고, <strong>세션 ID를 쿠키에 저장</strong>함 (<code>Set-Cookie: sessionId=xyz</code>).</li>
<li>이후 클라이언트가 요청을 보낼 때 <code>Cookie</code> 헤더를 이용하여 세션 ID를 함께 전송함.</li>
<li>서버는 해당 세션 ID를 조회하여 사용자 정보를 가져옴.</li>
</ul>
<p>✅ <strong>세션이 좋았던 점</strong></p>
<ul>
<li>로그인한 사용자의 데이터를 서버에서 직접 관리할 수 있어서 보안성이 높음.</li>
<li>클라이언트가 직접 값을 수정할 수 없으므로 데이터 조작 위험이 줄어듦.</li>
</ul>
<p>❌ <strong>BUT ❌ 이런 단점이 있었음</strong></p>
<ul>
<li>서버에서 사용자별 데이터를 저장해야 하므로 유저가 많아지면 메모리 부담이 커질 수 있음.</li>
<li>분산 서버 환경에서는 세션을 공유하는 처리가 필요함 (예: Redis 활용).</li>
<li>서버가 재시작되면 기존 세션이 초기화될 수 있음.</li>
</ul>
<hr />
<h2 id="3️⃣-토큰token---jwt로-인증하기">3️⃣ 토큰(Token) - JWT로 인증하기</h2>
<p>API 기반 인증이 필요할 때, 그리고 모바일, 웹 등 여러 환경에서 인증을 유지할 때 <strong>JWT(JSON Web Token)</strong>을 사용했다. 
토큰 기반 인증의 핵심은 <strong>서버가 사용자의 상태를 기억하지 않아도 된다는 것</strong>이다.</p>
<p>✅ <strong>토큰의 HTTP 연관성</strong></p>
<ul>
<li>JWT는 <code>Authorization</code> 헤더(<code>Authorization: Bearer &lt;토큰&gt;</code> 사용)를 통해 서버에 전송됨.</li>
<li>세션과 달리 서버는 별도의 저장소 없이, 토큰만으로 사용자를 검증할 수 있음.</li>
</ul>
<p>✅ <strong>JWT가 유용했던 경우</strong></p>
<ul>
<li>REST API 기반 서비스에서 로그인 인증을 구현할 때</li>
<li>모바일, 웹, 데스크톱 등 여러 환경에서 공통으로 사용할 때</li>
<li>마이크로서비스 아키텍처를 구축할 때</li>
</ul>
<p>❌ <strong>BUT ❌ 이런 문제가?</strong></p>
<ul>
<li>JWT가 탈취되면 만료될 때까지 계속 사용할 수 있어서 보안에 주의해야 함.</li>
<li>페이로드(payload)가 Base64로 인코딩되므로, 디코딩하면 내부 정보를 볼 수 있음 (중요한 정보 저장 금지!).</li>
<li>토큰이 길어지면 네트워크 트래픽 부담이 증가할 수 있음.</li>
</ul>
<p>그래서 JWT를 사용할 때는 만료 시간(expiration time)을 짧게 설정하고, <strong>리프레시 토큰(Refresh Token)</strong>을 활용하는 것이 중요했다.</p>
<hr />
<h2 id="💡-결국-어떤-방식이-좋을까">💡 결국 어떤 방식이 좋을까?</h2>
<table>
<thead>
<tr>
<th>비교 항목</th>
<th>쿠키 (Cookie)</th>
<th>세션 (Session)</th>
<th>토큰 (JWT)</th>
</tr>
</thead>
<tbody><tr>
<td>저장 위치</td>
<td>클라이언트 (브라우저)</td>
<td>서버</td>
<td>클라이언트</td>
</tr>
<tr>
<td>보안</td>
<td>취약 (조작 가능)</td>
<td>보안성 높음</td>
<td>보안 위험 존재 (탈취 시 문제)</td>
</tr>
<tr>
<td>상태 유지</td>
<td>O</td>
<td>O (서버 관리)</td>
<td>X (Stateless)</td>
</tr>
<tr>
<td>서버 부담</td>
<td>없음</td>
<td>높음 (세션 저장 필요)</td>
<td>없음</td>
</tr>
<tr>
<td>확장성</td>
<td>낮음 (동일 도메인에서만 사용 가능)</td>
<td>낮음 (서버 부하 증가)</td>
<td>높음 (마이크로서비스 및 모바일 지원)</td>
</tr>
<tr>
<td>인증 방식</td>
<td>클라이언트 측 인증</td>
<td>서버 측 인증</td>
<td>자체 검증 가능</td>
</tr>
<tr>
<td>유효 기간</td>
<td>브라우저 설정에 따라 다름</td>
<td>세션 만료 시 삭제됨</td>
<td>명시적으로 설정 가능 (Access Token + Refresh Token)</td>
</tr>
</tbody></table>
<hr />
<h2 id="️-결론">‼️ 결론</h2>
<p>웹 애플리케이션의 인증 방식은 <strong>HTTP가 상태를 기억하지 않기 때문에 필요하다.</strong></p>
<ul>
<li><strong>쿠키는 클라이언트가 직접 관리하는 인증 방식으로, 자동 로그인 등에 적합하다.</strong></li>
<li><strong>세션은 서버에서 인증 정보를 관리하며, 보안이 중요한 경우 적절하다.</strong></li>
<li><strong>JWT는 서버에서 상태를 저장하지 않는 방식으로, API 인증에 적합하다.</strong></li>
</ul>
<p>결국, <strong>쿠키, 세션, JWT를 적절히 조합하여 사용하는 것이 가장 현실적인 해결책</strong>이 될 수도 있다. 인증 방식에 대해 고민하는 사람이 있다면, 이 글이 도움이 되었으면 좋겠다!</p>
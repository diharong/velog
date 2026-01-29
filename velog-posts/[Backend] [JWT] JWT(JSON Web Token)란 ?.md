<h2 id="✏️-jwt란">✏️ JWT란?</h2>
<p>JWT는 &quot;JSON Web Token&quot;의 약자로, JSON 기반의 <strong>토큰(Token) 방식 인증</strong>을 의미한다. 주로 <strong>웹 및 모바일 애플리케이션의 인증(Authentication)과 정보 교환</strong>을 위해 사용됨. 기존 <strong>세션(Session)이나 쿠키(Cookie) 기반 인증보다 간편하고 확장성이 뛰어난 방식</strong>이다!</p>
<h3 id="✅-jwt가-필요한-이유">✅ JWT가 필요한 이유</h3>
<ul>
<li><strong>HTTP는 상태를 저장하지 않는(stateless) 프로토콜</strong>이기 때문에 사용자의 로그인 상태를 유지하려면 추가적인 인증 방식이 필요하다.</li>
<li>기존 <strong>세션 기반 인증</strong>은 서버가 사용자의 정보를 직접 저장해야 하므로 확장성에 한계가 있음.</li>
<li>JWT를 사용하면 <strong>서버가 상태를 유지할 필요 없이 클라이언트가 인증 정보를 직접 보관할 수 있다.</strong></li>
</ul>
<h2 id="🔎-jwt의-구조">🔎 JWT의 구조</h2>
<p>JWT는 세 부분으로 구성되며, 각각 점(<code>.</code>)으로 구분된다.
<img alt="" src="https://velog.velcdn.com/images/diha01/post/2cd1d8c8-77a4-498a-a3e4-07298cafca85/image.png" /></p>
<h3 id="1️⃣-header-헤더">1️⃣ Header (헤더)</h3>
<p>헤더는 JWT의 유형과 서명에 사용할 알고리즘을 지정함.</p>
<pre><code class="language-json">{
  &quot;alg&quot;: &quot;HS256&quot;,
  &quot;typ&quot;: &quot;JWT&quot;
}</code></pre>
<ul>
<li><code>alg</code>: 서명에 사용된 암호화 알고리즘 (예: <strong>HS256, RS256</strong> 등)</li>
<li><code>typ</code>: 토큰 타입 (항상 &quot;JWT&quot;로 설정됨)</li>
</ul>
<h3 id="2️⃣-payload-페이로드">2️⃣ Payload (페이로드)</h3>
<p>페이로드는 <strong>사용자 정보 및 토큰의 추가적인 데이터</strong>를 포함하는 부분임.</p>
<pre><code class="language-json">{
  &quot;sub&quot;: &quot;1234567890&quot;,
  &quot;name&quot;: &quot;John Doe&quot;,
  &quot;admin&quot;: true,
  &quot;iat&quot;: 1516239022,
  &quot;exp&quot;: 1516249022
}</code></pre>
<ul>
<li><code>sub</code> (Subject): 사용자의 고유 ID</li>
<li><code>name</code>: 사용자의 이름</li>
<li><code>admin</code>: 관리자 여부</li>
<li><code>iat</code> (Issued At): 토큰이 발행된 시간 (Unix Timestamp)</li>
<li><code>exp</code> (Expiration): 토큰의 만료 시간</li>
</ul>
<p>🚨 <strong>주의:</strong> 페이로드는 <strong>Base64로 인코딩되어 있지만 암호화되지 않으므로</strong> <del>중요한 정보</del>를 저장하면 안됨‼️!</p>
<h3 id="3️⃣-signature-서명">3️⃣ Signature (서명)</h3>
<p>서명은 <strong>토큰이 변조되지 않았음을 검증</strong>하는 역할.</p>
<pre><code>HMACSHA256(
  base64UrlEncode(header) + &quot;.&quot; + base64UrlEncode(payload),
  secretKey
)</code></pre><h2 id="🦾-jwt의-작동-원리">🦾 JWT의 작동 원리</h2>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/d700d63c-e084-43fa-9fc1-cb985049f5c9/image.png" /></p>
<p>1️⃣ <strong>사용자가 로그인 요청을 보냄</strong>
👉 클라이언트(사용자)는 아이디와 비밀번호를 입력하여 서버에 로그인 요청을 함.
2️⃣ <strong>서버가 사용자 정보를 확인</strong>
👉 서버는 요청을 받아서 DB에서 해당 사용자가 존재하는지 조회.
3️⃣ <strong>서버가 JWT 토큰을 생성</strong>
👉사용자가 유효한 계정이라면, 서버는 Secret Key를 사용하여 JWT 토큰을 생성한다.
생성된 JWT는 사용자의 정보를 포함하며, 서버에서 관리할 필요 없이 클라이언트가 보관함.
4️⃣ <strong>서버가 클라이언트에게 JWT 토큰 전달</strong>
👉서버는 JWT를 클라이언트(사용자)에게 반환.
이후부터 클라이언트는 이 JWT를 사용하여 API 요청을 보낼 수 있음.
5️⃣** 클라이언트가 API 요청 시 JWT를 포함하여 보냄**
👉클라이언트는 API 요청을 보낼 때 JWT를 <code>Authorization: Bearer &lt;토큰&gt;</code> 헤더에 포함합니다.
JWT는 쿠키를 사용할 필요 없이 HTTP 요청 헤더를 통해 전달됨.
6️⃣ <strong>서버가 JWT를 검증하여 사용자 인증 수행</strong>
👉서버는 JWT의 서명을 확인하여 변조되지 않았음을 검증한다.
JWT가 유효하면 사용자가 신뢰할 수 있는 사용자임을 확인하고 요청을 처리.
7️⃣** 서버가 API 응답 반환**
👉검증이 완료되면, 서버는 요청에 대한 응답을 클라이언트에게 반환.</p>
<h2 id="🥨-jwt-사용의-장점과-단점">🥨 JWT 사용의 장점과 단점</h2>
<h3 id="✅-장점">✅ <strong>장점</strong></h3>
<ul>
<li><strong>무상태성(Stateless)</strong>: 서버가 세션을 저장하지 않아 확장성이 뛰어남.</li>
<li><strong>빠른 인증</strong>: 서버가 세션을 조회할 필요 없이 토큰만 검증하면 됨.</li>
<li><strong>보안성</strong>: 서명을 통해 변조 여부를 검증할 수 있음.</li>
<li><strong>모바일 &amp; API 친화적</strong>: 다양한 클라이언트(웹, 모바일, IoT)에서 쉽게 사용할 수 있음.</li>
</ul>
<h3 id="❌-단점">❌ <strong>단점</strong></h3>
<ul>
<li><strong>보안 위험</strong>: 토큰이 탈취되면 만료될 때까지 사용할 수 있음.</li>
<li><strong>페이로드 노출</strong>: Base64로 인코딩되어 있어 민감한 정보를 저장하면 안 됨.</li>
<li><strong>토큰 크기 문제</strong>: JWT는 쿠키나 세션보다 크기가 커질 수 있음.</li>
</ul>
<h2 id="⚠️-jwt-사용-시-주의점">⚠️ JWT 사용 시 주의점</h2>
<ul>
<li>🔒 <strong>민감한 정보(비밀번호, 카드 정보 등)는 절대 페이로드에 포함하면 안 됨.</strong></li>
<li>🔑 <strong>비밀 키(secret key)를 안전하게 관리해야 함.</strong></li>
<li>🔗 <strong>HTTPS를 사용하여 토큰이 노출되지 않도록 해야 함.</strong></li>
<li>⏳ <strong>토큰의 유효기간(<code>exp</code>)을 적절히 설정하여 보안을 강화해야 함.</strong></li>
<li>🔄 <strong>Refresh Token을 사용하여 액세스 토큰을 갱신하는 방식을 고려해야 함.</strong></li>
</ul>
<h2 id="🆚-jwt-vs-oauth-20-비교">🆚 JWT vs. OAuth 2.0 비교</h2>
<table>
<thead>
<tr>
<th>기능</th>
<th>JWT</th>
<th>OAuth 2.0</th>
</tr>
</thead>
<tbody><tr>
<td>인증 방식</td>
<td>자체 검증</td>
<td>토큰 발급 및 검증 서버 필요</td>
</tr>
<tr>
<td>보안 수준</td>
<td>취약(탈취 가능)</td>
<td>보안 강화(Access Token + Refresh Token)</td>
</tr>
<tr>
<td>사용 용도</td>
<td>API 인증, 서버 간 통신</td>
<td>SSO, API 접근 제어</td>
</tr>
<tr>
<td>유효 기간</td>
<td>유효 시간 설정 필요</td>
<td>자동 갱신 가능</td>
</tr>
</tbody></table>
<h2 id="📌-jwt-실제-사용-사례">📌 JWT 실제 사용 사례</h2>
<ul>
<li>🔑 <strong>사용자 로그인 및 인증</strong> (예: REST API, GraphQL 인증)</li>
<li>🔓 <strong>싱글사인온(SSO, Single Sign-On) 시스템</strong></li>
<li>📡 <strong>서버 간 데이터 교환</strong> (API Gateway, 마이크로서비스)</li>
<li>🔒 <strong>모바일 및 IoT 장치 인증</strong></li>
</ul>
<h2 id="💡-결론">💡 결론</h2>
<p>JWT는 <strong>간단하고 확장성이 뛰어난 인증 방식</strong>으로, 특히 API 및 마이크로서비스 환경에서 많이 사용된다. 하지만 보안 취약점이 있을 수 있으므로, <strong>토큰 만료 시간 설정, HTTPS 사용, Refresh Token 활용</strong> 등의 보안 조치를 병행함을 잊지 말자.</p>
<blockquote>
<p>참고 및 이미지 출처: <a href="https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-JWTjson-web-token-%EB%9E%80-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC#jwt_json_web_token_%EC%9D%B4%EB%9E%80">https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-JWTjson-web-token-%EB%9E%80-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC#jwt_json_web_token_%EC%9D%B4%EB%9E%80</a>
<a href="https://velog.io/@chuu1019/%EC%95%8C%EA%B3%A0-%EC%93%B0%EC%9E%90-JWTJson-Web-Token">https://velog.io/@chuu1019/%EC%95%8C%EA%B3%A0-%EC%93%B0%EC%9E%90-JWTJson-Web-Token</a></p>
</blockquote>
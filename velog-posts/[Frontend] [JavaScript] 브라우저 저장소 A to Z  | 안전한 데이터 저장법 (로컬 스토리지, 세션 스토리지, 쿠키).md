<h1 id="🌐-브라우저-저장소에-대해-알아보자️">🌐 브라우저 저장소에 대해 알아보자‼️</h1>
<p>웹 서비스 개발 시 알아야하는 <strong>브라우저 저장소</strong>에 대한 포스팅이다!  
브라우저는 <em>데이터를 저장하는</em> 여러 가지 방법을 제공하는데, 대표적으로 <strong>로컬 스토리지(Local Storage)</strong>, <strong>세션 스토리지(Session Storage)</strong>, <strong>쿠키(Cookie)</strong>가 있다.</p>
<p>이번 포스팅에서는 각각의 저장소가 어떤 <strong>역할</strong>을 하는지, <strong>어떤 상황</strong>에서 사용해야 하는지, 그리고 <strong>차이점</strong>은 무엇인지 알아보자.</p>
<hr />
<h2 id="1-🗂️-로컬-스토리지local-storage">1. 🗂️ 로컬 스토리지(Local Storage)</h2>
<h3 id="📌-로컬-스토리지란">📌 로컬 스토리지란?</h3>
<p>로컬 스토리지는 <strong>브라우저에 데이터를 영구적으로 저장할 수 있는 저장소</strong>이다. 사용자가 데이터를 직접 삭제하지 않는 한 계속 남아 있음.</p>
<h3 id="📌-로컬-스토리지의-특징">📌 로컬 스토리지의 특징</h3>
<ul>
<li><strong>데이터가 영구적으로 저장됨</strong> → 사용자가 직접 삭제하지 않는 한 유지됨.</li>
<li><strong>도메인(Origin) 단위로 저장됨</strong> → 같은 웹사이트(도메인) 내에서만 데이터를 사용할 수 있음.</li>
<li><strong>서버와 자동으로 데이터를 주고받지 않음</strong> → 보안성이 높고, 불필요한 네트워크 트래픽을 줄일 수 있음.</li>
<li><strong>저장 용량이 크다</strong> → 보통 5MB까지 저장할 수 있으며, 브라우저에 따라 차이가 있다.</li>
</ul>
<h3 id="📌-언제-로컬-스토리지를-사용해야-할까">📌 언제 로컬 스토리지를 사용해야 할까?</h3>
<p>✅ <strong>사용자가 설정한 정보 유지</strong> → 다크 모드 설정, 언어 설정 등
✅ <strong>자동 로그인 여부 저장</strong> → 사용자가 매번 로그인 여부를 설정하지 않도록 저장
✅ <strong>장바구니 정보 저장</strong> → 로그인하지 않은 사용자도 장바구니 정보를 유지 가능</p>
<h3 id="📌-js-예시-코드">📌 JS 예시 코드</h3>
<pre><code class="language-javascript">// 데이터 저장하기
localStorage.setItem(&quot;theme&quot;, &quot;dark&quot;);</code></pre>
<p>👉 <code>setItem</code> 메서드를 사용하여 <strong>&quot;theme&quot;</strong> 키에 <strong>&quot;dark&quot;</strong> 값을 저장</p>
<pre><code class="language-javascript">// 데이터 가져오기
const theme = localStorage.getItem(&quot;theme&quot;);
console.log(theme); // &quot;dark&quot;</code></pre>
<p>👉 <code>getItem</code> 메서드를 사용하여 <strong>&quot;theme&quot;</strong> 키에 저장된 데이터를 가져옴. 콘솔에 <strong>&quot;dark&quot;</strong> 값이 출력된다.</p>
<pre><code class="language-javascript">// 데이터 삭제하기
localStorage.removeItem(&quot;theme&quot;);</code></pre>
<p>👉 <code>removeItem</code>을 사용하면 특정 키의 데이터를 삭제할 수 있다.</p>
<pre><code class="language-javascript">// 모든 데이터 삭제하기
localStorage.clear();</code></pre>
<p>👉 <code>clear</code> 메서드는 저장된 모든 데이터를 삭제한다.</p>
<hr />
<h2 id="2-🕒-세션-스토리지session-storage">2. 🕒 세션 스토리지(Session Storage)</h2>
<h3 id="📌-세션-스토리지란">📌 세션 스토리지란?</h3>
<p>세션 스토리지는 <strong>브라우저 탭(세션)이 열려 있는 동안만 데이터를 저장</strong>하는 저장소이다. 즉, <strong>브라우저 탭을 닫으면 데이터가 사라짐!</strong></p>
<h3 id="📌-세션-스토리지의-특징">📌 세션 스토리지의 특징</h3>
<ul>
<li><strong>브라우저 탭(세션)이 닫힐 때 데이터가 삭제됨</strong> → 일시적인 데이터 저장에 적합</li>
<li><strong>도메인(Origin) 단위로 저장됨</strong> → 같은 웹사이트 내에서만 데이터 공유 가능</li>
<li><strong>서버와 자동으로 데이터를 주고받지 않음</strong> → 네트워크 부담이 없음</li>
<li><strong>로컬 스토리지와 사용법이 거의 동일함</strong></li>
</ul>
<h3 id="📌-언제-세션-스토리지를-사용해야-할까">📌 언제 세션 스토리지를 사용해야 할까?</h3>
<p>✅ <strong>일회성 로그인 정보 저장</strong> → 페이지를 새로고침해도 유지되지만, 탭을 닫으면 사라짐
✅ <strong>특정 페이지에서만 필요한 데이터 저장</strong> → 검색 필터, 일시적인 폼 입력값 저장
✅ <strong>입력 폼 데이터 임시 저장</strong> → 사용자가 실수로 페이지를 이동해도 값 유지</p>
<h3 id="📌-js-예시-코드-1">📌 JS 예시 코드</h3>
<pre><code class="language-javascript">// 데이터 저장하기
sessionStorage.setItem(&quot;sessionData&quot;, &quot;temporaryValue&quot;);</code></pre>
<p>👉 <code>setItem</code> 메서드를 사용하여 <strong>&quot;sessionData&quot;</strong> 키에 <strong>&quot;temporaryValue&quot;</strong> 값을 저장.</p>
<pre><code class="language-javascript">// 데이터 가져오기
const data = sessionStorage.getItem(&quot;sessionData&quot;);
console.log(data); // &quot;temporaryValue&quot;</code></pre>
<p>👉 <code>getItem</code>을 사용하여 저장된 데이터를 가져오고, 콘솔에 <strong>&quot;temporaryValue&quot;</strong> 값이 출력됨.</p>
<pre><code class="language-javascript">// 데이터 삭제하기
sessionStorage.removeItem(&quot;sessionData&quot;);</code></pre>
<p>👉 특정 키의 데이터를 삭제하려면 <code>removeItem</code>을 사용한다.</p>
<pre><code class="language-javascript">// 모든 데이터 삭제하기
sessionStorage.clear();</code></pre>
<p>👉 <code>clear</code> 메서드를 사용하면 세션 스토리지에 저장된 모든 데이터를 삭제할 수 있다.</p>
<hr />
<h2 id="3-🍪-쿠키cookie">3. 🍪 쿠키(Cookie)</h2>
<h3 id="📌-쿠키란">📌 쿠키란?</h3>
<p>쿠키는 <strong>클라이언트와 서버가 데이터를 주고받을 수 있도록 저장하는 작은 데이터 조각</strong>. 쿠키는 일정한 기간 동안 저장할 수 있으며, 만료 날짜를 지정할 수도 있음.</p>
<h3 id="📌-쿠키의-특징">📌 쿠키의 특징</h3>
<ul>
<li><strong>클라이언트와 서버 간 자동으로 데이터를 주고받을 수 있음</strong> → 로그인 유지 등에 활용</li>
<li><strong>만료 기한을 설정할 수 있음</strong> → 브라우저를 껐다 켜도 유지 가능</li>
<li><strong>4KB 정도의 작은 저장 용량</strong> → 너무 큰 데이터를 저장하기에는 부적절</li>
<li><strong>보안 옵션을 설정할 수 있음</strong> → <code>HttpOnly</code>, <code>Secure</code> 등 설정 가능</li>
</ul>
<h3 id="📌-언제-쿠키를-사용해야-할까">📌 언제 쿠키를 사용해야 할까?</h3>
<p>✅ <strong>로그인 정보 유지</strong> → 로그인 세션 유지, 자동 로그인 설정
✅ <strong>사용자 맞춤형 광고 설정</strong> → 사용자의 관심사를 기반으로 광고 표시
✅ <strong>웹사이트 방문 기록 및 추적</strong> → 방문 기록 분석 및 맞춤형 콘텐츠 제공</p>
<h3 id="📌-js-예시-코드-2">📌 JS 예시 코드</h3>
<pre><code class="language-javascript">// 쿠키 저장하기
document.cookie = &quot;username=John; expires=Fri, 31 Dec 2025 23:59:59 GMT; path=/&quot;;</code></pre>
<p>👉 <code>document.cookie</code>를 사용하여 <strong>&quot;username&quot;</strong> 키에 <strong>&quot;John&quot;</strong> 값을 저장하고, <strong>만료 기한을 2025년 12월 31일</strong>로 설정한다.</p>
<pre><code class="language-javascript">// 쿠키 가져오기
console.log(document.cookie);</code></pre>
<p>👉 저장된 쿠키를 가져오면 <strong>&quot;username=John&quot;</strong> 값이 출력됨.</p>
<hr />
<h2 id="4-로컬-스토리지-🆚-쿠키-차이점">4. 로컬 스토리지 🆚 쿠키 차이점</h2>
<table>
<thead>
<tr>
<th>구분</th>
<th>로컬 스토리지</th>
<th>쿠키</th>
</tr>
</thead>
<tbody><tr>
<td><strong>데이터 크기</strong></td>
<td>최대 5MB</td>
<td>최대 4KB</td>
</tr>
<tr>
<td><strong>서버와의 관계</strong></td>
<td>서버와 자동으로 주고받지 않음</td>
<td>서버와 자동으로 주고받음</td>
</tr>
<tr>
<td><strong>데이터 만료</strong></td>
<td>사용자가 직접 삭제해야 함</td>
<td>만료 날짜 설정 가능</td>
</tr>
<tr>
<td><strong>보안성</strong></td>
<td>XSS 공격에 취약</td>
<td>HttpOnly 옵션을 설정하면 보안 강화</td>
</tr>
<tr>
<td><strong>사용 목적</strong></td>
<td>클라이언트 측 데이터 저장</td>
<td>세션 관리, 인증 정보 저장</td>
</tr>
</tbody></table>
<hr />
<h2 id="5-어떤-저장소를-사용해야-할까️">5. 어떤 저장소를 사용해야 할까⁉️</h2>
<p>✅ <strong>로컬 스토리지</strong> → 장기적으로 저장해야 할 데이터를 관리할 때
✅ <strong>세션 스토리지</strong> → 특정 페이지에서만 필요한 데이터 저장할 때
✅ <strong>쿠키</strong> → 서버와 데이터를 자동으로 주고받아야 할 때 (로그인 세션, 인증 등)</p>
<h3 id="💡-정리하자면-">💡 정리하자면 ?</h3>
<ul>
<li><strong>로컬 스토리지</strong>: 장기 보관, 브라우저 내 저장, 서버와 통신 없음</li>
<li><strong>세션 스토리지</strong>: 브라우저 탭이 닫히면 삭제, 일시적인 데이터 저장</li>
<li><strong>쿠키</strong>: 서버와 자동으로 데이터 주고받음, 보안 옵션 활용 가능</li>
</ul>
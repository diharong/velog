<h1 id="📌-jsx란-">📌 JSX란 ?</h1>
<blockquote>
<p><strong>JSX(JavaScript XML)</strong>는 리액트에서 UI를 선언적으로 표현하는 문법</p>
</blockquote>
<p><code>JavaScript</code>의 확장 문법으로 <code>HTML</code>과 유사한 구조를 가지면서도, <code>JavaScript</code> 코드 안에서 동작할 수 있다. </p>
<p><strong>JSX 를 사용하면 자바스크립트와 HTML 을 혼용하여 사용할 수 있다.</strong>
(JSX를 사용하면 다음과 같이 HTML과 유사한 구조로 컴포넌트를 작성할 수 있음.)</p>
<pre><code class="language-javascript">const element = &lt;h1&gt;Hello, world!&lt;/h1&gt;;</code></pre>
<p>위 코드는 <code>JavaScript</code> 코드지만, <code>HTML</code> 태그처럼 작성할 수 있다.
하지만 JSX는 <code>JavaScript</code> 문법이므로 브라우저가 직접 해석할 수 없고, <code>Babel</code>이 이를 <code>JavaScript</code> 코드로 변환해야 함.</p>
<p>‼️** 여기서 잠깐**</p>
<h3 id="🖋️-babel-이란-">🖋️ Babel 이란 ?</h3>
<blockquote>
<p>Babel(바벨)은 최신 JavaScript 코드를 구버전 JavaScript로 변환해주는 트랜스파일러(Transpiler)이다. </p>
</blockquote>
<p>🚀 쉽게 말해:</p>
<p><code>최신 JavaScript</code>(ES6+, JSX 등) 문법을 브라우저가 이해할 수 있도록 <strong><code>과거 JavaScript</code> 코드로 변환</strong>해주는 도구이다.
<code>JSX</code>도 <code>JavaScript</code>가 아닌 확장 문법이므로, 브라우저가 직접 실행할 수 없다.
👉 따라서 Babel이 <code>JSX</code>를 일반 <code>JavaScript</code> 코드로 변환해야 함.</p>
<p><del>자세한 내용은 따로 포스팅 예정</del></p>
<h2 id="✏️-jsx의-주요-특징">✏️ JSX의 주요 특징</h2>
<h3 id="1️⃣-태그-안에-javascript-표현식-사용하기">1️⃣ 태그 안에 JavaScript 표현식 사용하기</h3>
<blockquote>
<p><code>JSX</code> 내부에서는 <code>중괄호 {}</code> 를 사용하여 <code>JavaScript</code> 표현식을 삽입할 수 있다.</p>
</blockquote>
<pre><code class="language-jsx">const name = &quot;React&quot;;
const element = &lt;h1&gt;Hello, {name}!&lt;/h1&gt;;</code></pre>
<p>위 코드에서 <code>{name}</code>은 React로 변환되어 
브라우저에서 <code>&lt;h1&gt;Hello, React!&lt;/h1&gt;</code>가 출력된다. </p>
<h3 id="2️⃣-최상위-태그는-반드시-하나여야만-한다">2️⃣ 최상위 태그는 반드시 하나여야만 한다.</h3>
<blockquote>
<p>JSX에서 여러 요소를 반환할 경우 반드시 하나의 부모 요소로 감싸야 함. </p>
</blockquote>
<p>단순히 <code>&lt;&gt;&lt;/&gt;</code>을 사용하면 불필요한 <code>&lt;div&gt;</code> 태그를 줄일 수 있다.</p>
<pre><code class="language-jsx">return (
  &lt;&gt;
    &lt;h1&gt;Title&lt;/h1&gt;
    &lt;p&gt;Description&lt;/p&gt;
  &lt;/&gt;
);</code></pre>
<h3 id="3️⃣-jsx의-속성attribute은-camelcase-사용">3️⃣ JSX의 속성(attribute)은 CamelCase 사용</h3>
<p>HTML에서는 class, for 같은 속성을 사용하지만, </p>
<blockquote>
<p><strong>JSX에서는</strong> className, htmlFor처럼 <strong>CamelCase 형식</strong>을 사용한다. </p>
</blockquote>
<pre><code class="language-jsx">const element = &lt;button className=&quot;btn&quot;&gt;Click me&lt;/button&gt;;</code></pre>
<p>✔️ <code>class</code> 대신 <code>className</code>을 사용해야 함.
✔️ <code>for</code> 대신 <code>htmlFor</code>를 사용해야 함.</p>
<h3 id="4️⃣-style-속성은-객체-형태로-작성">4️⃣ style 속성은 객체 형태로 작성</h3>
<pre><code class="language-jsx">const titleStyle = {
  color: &quot;blue&quot;,
  fontSize: &quot;20px&quot;
};

const element = &lt;h1 style={titleStyle}&gt;Styled Text&lt;/h1&gt;;</code></pre>
<p>✔️ 스타일 속성 이름은 <code>CamelCase</code>로 작성해야 함 (<code>background-color</code> → <code>backgroundColor</code>)</p>
<h3 id="5️⃣--조건부-렌더링">5️⃣  조건부 렌더링</h3>
<blockquote>
<p>삼항 연산자나 &amp;&amp; 연산자를 사용하여 JSX 내부에서 조건부 렌더링이 가능함.</p>
</blockquote>
<pre><code class="language-jsx">const isLogIn = true;
return &lt;&gt;
    {user.isLogin ? &lt;div&gt;로그아웃&lt;/div&gt; : &lt;div&gt;로그인&lt;/div&gt;}  
    &lt;/&gt;</code></pre>
<p>⚠️ *<em>주의 *</em></p>
<blockquote>
<p>JSX에서는 <del>if문을 직접 사용할 수 없으며</del>, 대신 삼항 연산자 또는 &amp;&amp; 연산자를 활용해야 함.</p>
</blockquote>
<ul>
<li>참고 : 한 입 크기로 잘라먹는 리액트</li>
<li>참고 : <a href="https://ko.legacy.reactjs.org/docs/jsx-in-depth.html">react 공식홈페이지</a></li>
</ul>
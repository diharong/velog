<h1 id="📌-자바스크립트의-호이스팅hoisting이란-">📌 자바스크립트의 호이스팅(Hoisting)이란 ?</h1>
<p>자바스크립트에서 <strong>호이스팅(Hoisting)</strong>은 변수와 함수 선언이 코드 실행 전에 <strong>최상위로 끌어올려지는 동작</strong>을 의미하는 개념이다. 이를 이해하면 코드의 실행 흐름을 보다 명확하게 파악할 수 있다.</p>
<h2 id="1️⃣-변수-호이스팅">1️⃣ 변수 호이스팅</h2>
<p>자바스크립트에서 <code>var</code>로 선언된 변수는 <strong>선언만</strong> 코드의 최상위로 끌어올려지고, 할당은 원래 자리에 남아 있다.</p>
<pre><code class="language-javascript">console.log(x); // undefined
var x = 5;
console.log(x); // 5</code></pre>
<p>위 코드는 다음과 같이 해석된다.</p>
<pre><code class="language-javascript">var x;
console.log(x); // undefined
x = 5;
console.log(x); // 5</code></pre>
<p>즉, <code>var</code>로 선언된 변수는 선언만 호이스팅되고 값이 할당되기 전까지 <code>undefined</code> 상태를 유지한다. ⚠️</p>
<h3 id="🔎-let과-const의-호이스팅">🔎 <code>let</code>과 <code>const</code>의 호이스팅</h3>
<p>ES6에서 도입된 <code>let</code>과 <code>const</code>도 호이스팅되지만, <code>var</code>와는 다르게 초기화 전에 접근하면 <strong>에러(<code>ReferenceError</code>)</strong>가 발생한다.</p>
<pre><code class="language-javascript">console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 10;</code></pre>
<p>🔒 이러한 현상은 <strong>TDZ(Temporal Dead Zone, 임시 사각지대)</strong> 때문이며, 변수가 선언되었지만 초기화되지 않은 시점부터 초기화 코드가 실행되기 전까지는 접근할 수 없다. </p>
<h4 id="️-tdztemporal-dead-zone란">⁉️ TDZ(Temporal Dead Zone)란?</h4>
<p>TDZ(임시 사각지대)는 변수가 선언되었지만, 아직 값이 할당되지 않은 상태에서 접근할 수 없는 구간을 의미한다.</p>
<p>쉽게 말해, <code>let</code>과 <code>const</code>로 선언된 변수는 선언은 되어 있지만, 초기화 전까지 사용할 수 없는 시점이 존재한다는 것이다.</p>
<pre><code class="language-javascript">console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 10;</code></pre>
<p>위 코드에서 a는 선언되었지만, 아직 초기화되지 않아서 TDZ 상태에 머물고 있다. 따라서 접근하려고 하면 <code>ReferenceError</code>가 발생한다.</p>
<p>TDZ는 변수의 선언과 초기화가 분리되어 실행되기 때문에 발생하는 개념이며, <code>var</code>에서는 발생하지 않고 <code>let</code>, <code>const</code>, <code>class</code>에서만 발생한다. 🚨</p>
<h2 id="2️⃣-함수-호이스팅">2️⃣ 함수 호이스팅</h2>
<p>함수 선언문(Function Declaration)은 변수와 다르게 <strong>전체 코드 실행 전에 선언과 초기화가 함께 이루어진다.</strong></p>
<pre><code class="language-javascript">greet(); // &quot;Hello, world!&quot;

function greet() {
    console.log(&quot;Hello, world!&quot;);
}</code></pre>
<p>📌 위 코드에서는 <code>greet()</code> 함수를 호출하기 전에 선언했지만 정상적으로 실행된다. 이는 <strong>함수 선언문이 코드 실행 전에 메모리에 미리 할당되기 때문</strong>이다. </p>
<h3 id="🔄-함수-표현식과-호이스팅">🔄 함수 표현식과 호이스팅</h3>
<p>반면, 함수 표현식(Function Expression)은 변수와 마찬가지로 <strong>선언만 호이스팅되므로</strong>, 초기화 전에 호출하면 <code>TypeError</code>가 발생한다.</p>
<pre><code class="language-javascript">hello(); // TypeError: hello is not a function

var hello = function() {
    console.log(&quot;Hello!&quot;);
};</code></pre>
<p>위 코드의 실제 동작 방식은 다음과 같다.</p>
<pre><code class="language-javascript">var hello;
hello(); // TypeError: hello is not a function
hello = function() {
    console.log(&quot;Hello!&quot;);
};</code></pre>
<p> 🛠️ 즉, 함수 표현식에서 사용된 변수 <code>hello</code>는 선언만 호이스팅되고, <strong>함수 할당은 원래 위치에서 실행</strong>된다.</p>
<h2 id="3️⃣-호이스팅을-이해하고-활용하는-방법-💡">3️⃣ 호이스팅을 이해하고 활용하는 방법 💡</h2>
<p>호이스팅은 자바스크립트의 실행 방식에 대한 이해를 돕는 개념이지만, 예기치 않은 오류를 방지하려면 다음과 같은 규칙을 따르는 것이 좋다. </p>
<h3 id="🔹-let과-const-사용하기">🔹 <code>let</code>과 <code>const</code> 사용하기</h3>
<p><code>var</code> 대신 <code>let</code>과 <code>const</code>를 사용하면 <strong>TDZ를 활용하여</strong> 호이스팅으로 인한 혼란을 줄일 수 있다.</p>
<h3 id="🔹-함수-표현식-사용하기">🔹 함수 표현식 사용하기</h3>
<p>함수 선언문보다는 <strong>함수 표현식</strong>을 활용하여 코드의 흐름을 명확하게 만들 수 있다.</p>
<h3 id="🔹-변수를-선언한-후-사용하기">🔹 변수를 선언한 후 사용하기</h3>
<p>가능한 한 변수를 선언한 후에 사용하는 것이 좋으며, 코드 최상단에 변수 선언을 모아두는 것도 좋은 습관이다. </p>
<h2 id="🔎-알고-가면-좋아요-🦾💭">🔎 알고 가면 좋아요 🦾💭</h2>
<h3 id="1-자바스크립트에서-호이스팅이란">1. 자바스크립트에서 호이스팅이란?</h3>
<p>변수와 함수 선언이 코드 실행 전에 최상위로 끌어올려지는 동작을 의미한다. 쉽게 말해, <strong>자바스크립트가 실행되기 전에 변수와 함수가 미리 메모리에 등록되는 개념</strong>이다. </p>
<h3 id="2-var-let-const에-따라-호이스팅이-어떻게-다르게-동작할까">2. <code>var</code>, <code>let</code>, <code>const</code>에 따라 호이스팅이 어떻게 다르게 동작할까?</h3>
<ul>
<li><code>var</code>는 선언만 호이스팅되고 값은 <code>undefined</code>로 초기화된다. </li>
<li><code>let</code>과 <code>const</code>도 호이스팅되지만 <strong>TDZ(임시 사각지대)</strong>가 있어서 선언 전에 접근하면 <code>ReferenceError</code>가 발생한다. </li>
</ul>
<h3 id="3-tdztemporal-dead-zone">3. TDZ(Temporal Dead Zone)?</h3>
<ul>
<li><strong>변수가 선언되었지만 초기화되기 전까지 접근할 수 없는 영역</strong>이다. </li>
<li><code>let</code>과 <code>const</code>는 TDZ가 존재하여, <strong>초기화 코드가 실행되기 전까지 참조할 수 없다.</strong> </li>
</ul>
<h3 id="4-함수-선언문과-함수-표현식의-호이스팅-차이는-무엇인가">4. 함수 선언문과 함수 표현식의 호이스팅 차이는 무엇인가?</h3>
<ul>
<li><strong>함수 선언문</strong>은 코드 실행 전에 미리 메모리에 저장되므로 <strong>어디서든 호출 가능</strong>하다.</li>
<li><strong>함수 표현식</strong>은 변수에 할당되므로 선언 전에 호출하면 <code>TypeError</code>가 발생한다. </li>
</ul>
<h3 id="5-변수를-선언한-후-사용해야-하는-이유는">5. 변수를 선언한 후 사용해야 하는 이유는?</h3>
<p>호이스팅으로 인해 <strong>예기치 않은 버그가 발생할 수 있기 때문</strong>이다. <code>let</code>과 <code>const</code>를 사용하면 <strong>TDZ 덕분에 오류를 빨리 감지할 수 있다.</strong> </p>
<h3 id="6-호이스팅이-코드-실행에-미치는-영향은">6. 호이스팅이 코드 실행에 미치는 영향은?</h3>
<p>변수를 선언 전에 참조하면 <code>undefined</code> 또는 <code>ReferenceError</code>가 발생할 수 있다. <code>let</code>과 <code>const</code>를 사용하면 보다 안전하게 코드를 작성할 수 있다. </p>
<h3 id="7-자바스크립트-엔진은-호이스팅을-어떻게-처리할까">7. 자바스크립트 엔진은 호이스팅을 어떻게 처리할까?</h3>
<ol>
<li><strong>메모리 할당 단계에서 변수와 함수 선언을 미리 등록</strong>한다.</li>
<li>실행 단계에서 코드 흐름을 따라 실행하면서 값을 할당한다. </li>
</ol>
<h3 id="8-즉시-실행-함수iife와-호이스팅의-관계는">8. 즉시 실행 함수(IIFE)와 호이스팅의 관계는?</h3>
<p>IIFE는 <strong>즉시 실행되므로</strong>, 호이스팅된 변수나 함수와 독립적으로 동작하여 <strong>전역 스코프 오염을 방지</strong>하는 데 유용하다.</p>
<h3 id="9-es6-이후-호이스팅-관련-주요-변경-사항은">9. ES6 이후 호이스팅 관련 주요 변경 사항은?</h3>
<ul>
<li><code>let</code>과 <code>const</code>가 도입되어 <strong>TDZ 개념이 추가</strong>되었다.</li>
<li><code>class</code>도 호이스팅되지만 TDZ가 적용되어 <strong>선언 전에 사용하면 오류가 발생</strong>한다❗</li>
</ul>
<h2 id="👉-결론">👉 결론</h2>
<p>자바스크립트의 호이스팅은 <strong>변수와 함수 선언을 코드 최상단으로 끌어올리는 동작</strong>을 의미한다. 이를 이해하면 코드 실행 순서를 명확히 파악할 수 있다. </p>
<p><strong>💡 <code>let</code>, <code>const</code>, 함수 표현식을 적극 활용하여</strong> 보다 예측 가능한 코드를 작성하는 것이 좋다. </p>
<p>콜백 함수(Callback Function)는 쉽게 말하면 &quot;나중에 불러줘!&quot;라고 부탁하는 함수다. 특정 작업이 끝난 후 실행되는 함수로, 자바스크립트의 비동기 작업 처리에서 흔히 사용된다.</p>
<hr />
<h2 id="🔍-콜백-함수가-왜-필요할까">🔍 콜백 함수가 왜 필요할까?</h2>
<p>자바스크립트는 싱글 스레드(Single Thread) 기반으로 실행된다. 즉, 한 번에 하나의 작업만 처리할 수 있다. 하지만 서버 요청, 타이머, 사용자 이벤트와 같은 작업은 즉시 완료되지 않고 일정 시간이 소요된다. 이러한 비동기 작업을 효율적으로 처리하기 위해 콜백 함수를 사용한다.</p>
<hr />
<h2 id="✅-콜백-함수-실행-흐름">✅ 콜백 함수 실행 흐름</h2>
<pre><code class="language-javascript">console.log('A');  // 동기 코드 실행

setTimeout(() =&gt; {
    console.log('B');  // 비동기 코드 (3초 후 실행)
}, 3000);

console.log('C');  // 동기 코드 실행</code></pre>
<p><strong>출력 결과:</strong></p>
<pre><code>A
C
B</code></pre><p>📌 <code>setTimeout()</code>은 비동기 함수이므로, <code>B</code>는 3초 후 실행된다. 즉, 자바스크립트는 <strong>비동기 작업을 백그라운드에서 실행하면서 다음 코드를 계속 진행한다.</strong> 이런 흐름을 조절하는 것이 바로 <strong>콜백 함수의 역할</strong>이다.</p>
<hr />
<h2 id="🎯-콜백-함수-예시">🎯 콜백 함수 예시</h2>
<pre><code class="language-javascript">// 콜백 함수 정의
function greeting(name) {
    console.log(`안녕하세요, ${name}님! 👋`);
}

// 콜백 함수를 실행하는 함수
function processUserInput(callback) {
    const name = &quot;철수&quot;;
    callback(name);
}

// 콜백 함수 전달
processUserInput(greeting);</code></pre>
<p>📌 <code>greeting</code> 함수는 <code>processUserInput</code> 함수가 실행된 후 <strong>나중에 호출되는 함수</strong>이다.</p>
<hr />
<h2 id="🔥-고차-함수higher-order-function와-콜백">🔥 고차 함수(Higher-Order Function)와 콜백</h2>
<p>고차 함수란 <strong>다른 함수를 매개변수로 받거나 반환하는 함수</strong>를 말한다. 콜백 함수는 보통 고차 함수와 함께 사용된다.</p>
<h3 id="✅-고차-함수-예시">✅ 고차 함수 예시</h3>
<pre><code class="language-javascript">function repeat(n, callback) {
    for (let i = 0; i &lt; n; i++) {
        callback(i);
    }
}

// 콜백 함수 전달
repeat(5, function(i) {
    console.log(`반복: ${i}`);
});</code></pre>
<p>📌 <code>repeat(5, callback)</code>을 호출하면, <code>callback(i)</code>이 5번 실행된다.</p>
<hr />
<h2 id="📌-배열-메서드에서-콜백-함수-활용">📌 배열 메서드에서 콜백 함수 활용</h2>
<h3 id="1️⃣-foreach">1️⃣ <code>forEach()</code></h3>
<pre><code class="language-javascript">const numbers = [1, 2, 3, 4, 5];

numbers.forEach(num =&gt; {
    console.log(num * 2);
});</code></pre>
<p>📌 <code>forEach()</code>는 배열의 각 요소에 대해 콜백 함수를 실행한다.</p>
<h3 id="2️⃣-filter">2️⃣ <code>filter()</code></h3>
<pre><code class="language-javascript">const words = [&quot;apple&quot;, &quot;banana&quot;, &quot;cherry&quot;];

const result = words.filter(word =&gt; word.length &gt; 5);
console.log(result);  // ['banana', 'cherry']</code></pre>
<p>📌 <code>filter()</code>는 조건을 만족하는 요소만 <strong>새로운 배열</strong>로 반환한다.</p>
<h3 id="3️⃣-reduce">3️⃣ <code>reduce()</code></h3>
<pre><code class="language-javascript">const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((acc, num) =&gt; acc + num, 0);
console.log(sum);  // 15</code></pre>
<p>📌 <code>reduce()</code>는 <strong>배열 요소를 누적하여 하나의 값</strong>으로 만든다.</p>
<hr />
<h2 id="🚩-콜백-지옥callback-hell과-해결-방법">🚩 콜백 지옥(Callback Hell)과 해결 방법</h2>
<p>콜백 함수가 중첩되어 코드가 복잡하고 가독성이 떨어지는 현상을 <strong>콜백 지옥</strong>이라고 한다.</p>
<pre><code class="language-javascript">setTimeout(() =&gt; {
    console.log(&quot;1초 후 실행 ⏳&quot;);
    setTimeout(() =&gt; {
        console.log(&quot;2초 후 실행 ⏳&quot;);
        setTimeout(() =&gt; {
            console.log(&quot;3초 후 실행 ⏳&quot;);
        }, 1000);
    }, 1000);
}, 1000);</code></pre>
<p>📌 <strong>중첩 구조</strong>로 인해 코드 가독성이 매우 떨어진다. 이를 해결하기 위해 <strong>Promise</strong>나 <strong>async/await</strong>를 사용할 수 있다.</p>
<hr />
<h2 id="🚀-promise와-asyncawait로-콜백-지옥-탈출하기">🚀 Promise와 async/await로 콜백 지옥 탈출하기</h2>
<h3 id="✅-promise-사용">✅ Promise 사용</h3>
<pre><code class="language-javascript">function delay(ms) {
    return new Promise(resolve =&gt; setTimeout(resolve, ms));
}

delay(1000)
    .then(() =&gt; {
        console.log(&quot;1초 후 실행 ⏳&quot;);
        return delay(1000);
    })
    .then(() =&gt; {
        console.log(&quot;2초 후 실행 ⏳&quot;);
        return delay(1000);
    })
    .then(() =&gt; {
        console.log(&quot;3초 후 실행 ⏳&quot;);
    });</code></pre>
<h3 id="✅-asyncawait-사용">✅ async/await 사용</h3>
<pre><code class="language-javascript">async function run() {
    await delay(1000);
    console.log(&quot;1초 후 실행 ⏳&quot;);
    await delay(1000);
    console.log(&quot;2초 후 실행 ⏳&quot;);
    await delay(1000);
    console.log(&quot;3초 후 실행 ⏳&quot;);
}

run();</code></pre>
<p>📌 <code>async/await</code>를 사용하면 동기 코드처럼 <strong>직관적인 코드</strong>를 작성할 수 있다. </p>
<hr />
<h2 id="👉-끝으로">👉 끝으로</h2>
<p>✅ 콜백 함수는 비동기 처리에서 필수적인 개념이다. 하지만 콜백 지옥 문제를 방지하기 위해 Promise나 async/await를 함께 익혀야 한다. 배열 메서드(forEach, filter, reduce)에서도 자주 활용되므로, 다양한 방식으로 연습하면서 익숙해져야겠다. 💪🔥</p>
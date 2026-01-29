<p>오늘은 자바스크립트의 <code>async</code>와 <code>await</code>에 대해 공부하면서 정리한 내용을 공유해보려고 한다. 자바스크립트에서 비동기 처리를 할 때 자주 겪는 콜백 지옥(callback hell)을 해결하고, 코드를 더 명확하게 작성할 수 있는 방법이다.</p>
<h2 id="1-️-비동기-처리란">1. ⁉️ 비동기 처리란?</h2>
<p>자바스크립트는 한 번에 하나의 작업만 처리할 수 있는 <strong>싱글 스레드</strong> 언어이다. 만약 네트워크 요청이나 파일 읽기처럼 시간이 오래 걸리는 작업을 기다리고 있으면 다른 작업을 할 수 없다. 그래서 이런 작업을 기다리지 않고 다른 작업을 계속 진행할 수 있도록 <strong>비동기 처리</strong>를 사용한다.</p>
<p>예전에는 <code>setTimeout</code>, <code>XMLHttpRequest(XHR)</code>, <code>Promise</code> 등을 써서 비동기 작업을 처리했는데, 최근에는 <code>async</code>와 <code>await</code>을 사용하면 마치 동기적인 코드처럼 더 간결하고 이해하기 쉽게 작성할 수 있어서 좋았다.</p>
<hr />
<h2 id="2--✨-async와-await-이해하기">2.  ✨ async와 await 이해하기</h2>
<h3 id="🔹-async-키워드">🔹 async 키워드</h3>
<p><code>async</code>를 함수 앞에 붙이면 그 함수는 항상 <code>Promise</code>를 반환한다.</p>
<pre><code class="language-javascript">async function sayHello() {
    return &quot;Hello, Async!&quot;;
}

sayHello().then(console.log); // &quot;Hello, Async!&quot;</code></pre>
<p>이렇게 쓰면 자동으로 <code>Promise.resolve(&quot;Hello, Async!&quot;)</code> 형태로 반환된다.</p>
<h3 id="🔹-await-키워드">🔹 await 키워드</h3>
<p><code>await</code>는 반드시 <code>async</code> 함수 내부에서만 사용할 수 있고, 비동기 작업(<code>Promise</code>)의 결과가 나올 때까지 기다리게 해준다.</p>
<pre><code class="language-javascript">async function fetchMessage() {
    let response = await new Promise(resolve =&gt; setTimeout(() =&gt; resolve(&quot;비동기 작업 완료!&quot;), 2000));
    console.log(response);
}

fetchMessage();
// 2초 후 &quot;비동기 작업 완료!&quot; 출력</code></pre>
<p>이렇게 하면 코드 흐름이 중간에 멈추는 것처럼 보이지만, 실제로는 비동기로 처리되고 있다.</p>
<hr />
<h2 id="3-📌-asyncawait를-사용하는-이유">3. 📌 async/await를 사용하는 이유</h2>
<p>async/await를 사용하면 다음과 같은 장점이 있다.</p>
<h3 id="1️⃣-코드가-깔끔하고-이해하기-쉽다">1️⃣ 코드가 깔끔하고 이해하기 쉽다</h3>
<p>기존의 <code>Promise</code> 방식은 <code>.then()</code>이 연달아 붙어서 코드를 복잡하게 만든다.</p>
<h4 id="promise-방식">Promise 방식</h4>
<pre><code class="language-javascript">fetch(&quot;https://jsonplaceholder.typicode.com/users/1&quot;)
    .then(res =&gt; res.json())
    .then(user =&gt; fetch(`https://jsonplaceholder.typicode.com/posts?userId=${user.id}`))
    .then(res =&gt; res.json())
    .then(posts =&gt; console.log(posts))
    .catch(err =&gt; console.error(err));</code></pre>
<h4 id="asyncawait-방식">async/await 방식</h4>
<pre><code class="language-javascript">async function fetchUserAndPosts() {
    try {
        let userResponse = await fetch(&quot;https://jsonplaceholder.typicode.com/users/1&quot;);
        let user = await userResponse.json();

        let postsResponse = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${user.id}`);
        let posts = await postsResponse.json();

        console.log(posts);
    } catch (error) {
        console.error(&quot;에러 발생:&quot;, error);
    }
}

fetchUserAndPosts();</code></pre>
<p>코드가 위에서 아래로 순서대로 흘러가서 읽기 쉽다.</p>
<h3 id="2️⃣-에러-처리가-간편하다">2️⃣ 에러 처리가 간편하다</h3>
<p><code>async/await</code>는 일반적인 <code>try...catch</code> 방식으로 에러 처리가 가능해서, 어디서 에러가 발생했는지 쉽게 확인할 수 있다.</p>
<h3 id="3️⃣-디버깅이-쉽다">3️⃣ 디버깅이 쉽다</h3>
<p><code>async/await</code>로 작성된 코드는 일반 동기 코드처럼 디버깅이 간단해진다. <code>Promise</code> 방식에 비해 문제의 원인을 빠르게 찾을 수 있다.</p>
<hr />
<h2 id="4-🔄-여러-작업을-병렬로-처리하기">4. 🔄 여러 작업을 병렬로 처리하기</h2>
<p>비동기 작업이 여러 개라면 <code>Promise.all()</code>을 사용해서 병렬로 처리할 수 있다. 한 번에 여러 요청을 보내고, 더 빠르게 결과를 받을 수 있다.</p>
<pre><code class="language-javascript">async function fetchMultipleData() {
    let [user, posts] = await Promise.all([
        fetch(&quot;https://jsonplaceholder.typicode.com/users/1&quot;).then(res =&gt; res.json()),
        fetch(&quot;https://jsonplaceholder.typicode.com/posts?userId=1&quot;).then(res =&gt; res.json())
    ]);

    console.log(&quot;사용자:&quot;, user);
    console.log(&quot;게시물:&quot;, posts);
}

fetchMultipleData();</code></pre>
<hr />
<h2 id="5-⚠️-주의할-점">5. ⚠️ 주의할 점</h2>
<ul>
<li><code>await</code>은 반드시 <code>async</code> 함수 내부에서만 사용할 수 있다.</li>
<li>비동기 작업을 순차적으로 처리하면 속도가 느려질 수 있다. 이럴 때는 <code>Promise.all()</code>을 활용해서 병렬 처리를 해야 한다.</li>
</ul>
<hr />
<h2 id="6-thencatch와-asyncawait의-성능-비교">6. then/catch와 async/await의 성능 비교</h2>
<p>성능상 두 방식에 큰 차이는 없다. 하지만 <code>async/await</code>이 가독성과 유지보수 측면에서 더 유리하므로, 코드가 복잡해질 때는 적극적으로 사용하는 것이 좋다.</p>
<hr />
<h2 id="7-정리">7. 정리</h2>
<ul>
<li><code>async</code>: 비동기 함수로 만들어 항상 <code>Promise</code>를 반환한다.</li>
<li><code>await</code>: 비동기 작업의 완료를 기다린다.</li>
<li><code>try...catch</code>: 에러 처리가 쉽다.</li>
<li><code>Promise.all()</code>: 여러 작업을 동시에 처리할 수 있다.</li>
</ul>
<p>콜백 지옥을 해결함과 동시에 더 명확하고 유지보수하기 쉬운 비동기 코드를 작성할 때 async/await을 활용하면 큰 도움이 될 것 같다.</p>
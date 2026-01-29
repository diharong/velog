<h1 id="🔄-react의-리렌더링은-언제-어떻게-발생할까">🔄 React의 리렌더링은 언제 어떻게 발생할까?</h1>
<p>React에서 컴포넌트의 리렌더링은 애플리케이션의 상태를 최신으로 유지하기 위한 중요한 과정이다. 하지만 이 리렌더링이 불필요하게 발생하면 성능 문제가 생길 수 있다. 이번 포스팅에서는 React 컴포넌트가 리렌더링되는 주요 원리와 이를 최적화하는 방법에 대해 자세히 알아보자.</p>
<hr />
<h2 id="리렌더링이-발생하는-세-가지-상황">리렌더링이 발생하는 세 가지 상황</h2>
<p>React에서 컴포넌트는 다음의 세 가지 경우에 리렌더링된다.</p>
<h3 id="1️⃣-state의-값이-변경되었을-때">1️⃣ State의 값이 변경되었을 때</h3>
<p>컴포넌트 내부의 State는 컴포넌트가 직접 소유하며, State의 값이 변경되면 해당 컴포넌트가 다시 렌더링된다.<br />예를 들어, 버튼 클릭으로 <code>setState</code>를 호출하면, React는 해당 컴포넌트를 리렌더링해 화면에 최신 값을 보여준다.</p>
<h3 id="2️⃣-부모로부터-전달받은-props가-변경되었을-때">2️⃣ 부모로부터 전달받은 Props가 변경되었을 때</h3>
<p>Props는 부모 → 자식으로 전달되는 데이터이기 때문에, 부모가 새로운 값을 전달하면 자식 컴포넌트는 자동으로 업데이트된다.<br />부모가 Props를 변경하면, React는 자식 컴포넌트를 다시 렌더링하여 최신 데이터를 표시한다.</p>
<h3 id="3️⃣-부모-컴포넌트가-리렌더링되었을-때">3️⃣ 부모 컴포넌트가 리렌더링되었을 때</h3>
<p>부모 컴포넌트가 리렌더링되면, 자식 컴포넌트도 연쇄적으로 리렌더링된다.<br />이 경우 자식 컴포넌트의 Props가 바뀌지 않더라도 리렌더링이 일어나기 때문에, 불필요한 렌더링이 발생할 수 있다.</p>
<hr />
<h2 id="불필요한-리렌더링과-성능-문제">불필요한 리렌더링과 성능 문제</h2>
<p>불필요한 리렌더링은 앱의 성능 저하로 이어질 수 있다.<br />특히, 부모 컴포넌트에서 변경된 State가 자식 컴포넌트와 직접적인 연관이 없는데도 불구하고, 부모가 리렌더링되면서 자식도 덩달아 리렌더링되는 경우가 많다.</p>
<h3 id="예시-bulb-컴포넌트">예시: Bulb 컴포넌트</h3>
<pre><code class="language-jsx">function App() {
  const [light, setLight] = useState(false);
  const [count, setCount] = useState(0);

  return (
    &lt;div&gt;
      &lt;Bulb light={light} /&gt;
      &lt;button onClick={() =&gt; setLight(!light)}&gt;전등 켜기/끄기&lt;/button&gt;
      &lt;button onClick={() =&gt; setCount(count + 1)}&gt;카운트 증가&lt;/button&gt;
    &lt;/div&gt;
  );
}

function Bulb({ light }) {
  console.log(&quot;Bulb 컴포넌트 렌더링: light =&quot;, light);
  return &lt;div&gt;{light ? &quot;💡&quot; : &quot;🔌&quot;}&lt;/div&gt;;
}</code></pre>
<p>위의 코드에서 <code>Bulb</code> 컴포넌트는 <code>light</code> 상태만 Props로 받지만, <code>count</code> 버튼을 눌러도 리렌더링된다.<br />이는 부모 컴포넌트 <code>App</code>이 리렌더링되면서 자식 컴포넌트도 리렌더링되기 때문이다.</p>
<hr />
<h2 id="성능-최적화를-위한-팁">성능 최적화를 위한 팁</h2>
<ul>
<li><p><strong>관련 없는 State 분리</strong><br />전등 상태와 카운트 상태가 서로 관련이 없다면, 이를 별도의 컴포넌트로 분리하면 각각의 상태 변경이 서로 다른 컴포넌트에 영향을 주지 않는다.</p>
</li>
<li><p><strong>React.memo 사용</strong><br /><code>React.memo</code>를 활용하면 Props가 변경되지 않는 경우 자식 컴포넌트의 리렌더링을 방지할 수 있다.</p>
</li>
<li><p><strong>useCallback 및 useMemo 사용</strong><br />함수나 값이 재생성되지 않도록 <code>useCallback</code>과 <code>useMemo</code>를 활용하면 불필요한 렌더링을 줄일 수 있다.</p>
</li>
</ul>
<hr />
<h2 id="결론">결론</h2>
<p>React의 리렌더링 동작을 정확히 이해하고 사용하면 성능 최적화에 도움을 줄 수 있다.</p>
<ol>
<li><strong>State 변경</strong>, 2. <strong>Props 변경</strong>, 3. <strong>부모 리렌더링</strong>이 리렌더링의 주요 트리거라는 점을 기억해보자!
불필요한 리렌더링을 방지하고 효율적으로 컴포넌트를 설계하면 더 빠르고 매끄러운 사용자 경험을 제공할 수 있다💡</li>
</ol>
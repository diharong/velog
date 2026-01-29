<h1 id="📘-props와-state의-차이점">📘 Props와 State의 차이점</h1>
<p>React를 다루면서 알아야 할 개념 중 <strong>Props</strong>와 <strong>State</strong>이 있다. 이 둘은 모두 React 컴포넌트 내에서 데이터를 관리하기 위한 핵심적인 도구로, 각각의 역할과 사용법이 다르지만, 리엑트를 처음 접하는 입장에서는 이 둘의 명확한 차이를 알기 힘들다. 
이번 포스팅에서는 Props와 State가 정확히 무엇인지, 그리고 어떤 상황에서 각각을 사용해야 하는지에 대해 구체적으로 알아보자‼️</p>
<hr />
<h2 id="✏️-props란">✏️ Props란?</h2>
<blockquote>
<p>부모 컴포넌트가 자식 컴포넌트에게 전달하는 <strong>읽기 전용 데이터</strong> </p>
</blockquote>
<p>Props는 컴포넌트 외부에서 주어진 정보를 받아와 렌더링에 활용하며, 
이를 통해 React 컴포넌트를 재사용 가능하게 만들 수 있다.</p>
<h3 id="✔️-props의-주요-특징">✔️ Props의 주요 특징</h3>
<ol>
<li><p><strong>읽기 전용(Read-Only)</strong><br />자식 컴포넌트는 Props를 받을 뿐, 이를 <strong>직접 변경할 수 없다</strong>. 
Props가 변경되려면 부모 컴포넌트에서 새로운 값을 전달해야 한다.</p>
</li>
<li><p><strong>단방향 데이터 흐름</strong><br />데이터는 <strong>항상 부모 → 자식</strong>으로만 전달됨. 
자식은 데이터를 활용하지만, <del>그 데이터를 &quot;소유&quot;하거나 &quot;수정&quot;하지는 않는다</del>.</p>
</li>
<li><p><strong>컴포넌트 재사용성 향상</strong><br />Props를 통해 *<em>컴포넌트를 재사용 *</em>가능. 
같은 컴포넌트를 여러 군데에서 다양한 데이터로 렌더링할 수 있다.</p>
</li>
</ol>
<h3 id="props-예시">Props 예시</h3>
<pre><code class="language-jsx">function ParentComponent() {
  const greeting = &quot;Hello, React!&quot;;
  return &lt;ChildComponent message={greeting} /&gt;;
}

function ChildComponent(props) {
  return &lt;h1&gt;{props.message}&lt;/h1&gt;;
}</code></pre>
<p>위 예시에서 <code>ParentComponent</code>는 문자열 데이터를 <code>ChildComponent</code>로 전달한다. <code>ChildComponent</code>는 <code>props.message</code>를 사용해 데이터를 렌더링하지만, 직접 변경하지는 않는다.</p>
<hr />
<h2 id="✏️-state란">✏️ State란?</h2>
<blockquote>
<p>컴포넌트 내부에서 관리되는 데이터</p>
</blockquote>
<p>State는 동적인 데이터 변화를 관리하며, 변경될 때마다 해당 컴포넌트의 UI를 자동으로 업데이트한다. 이 점이 Props와 가장 큰 차이이다‼️</p>
<h3 id="✔️-state의-주요-특징">✔️ State의 주요 특징</h3>
<ol>
<li><p><strong>컴포넌트 내부에서 관리</strong><br />State는 컴포넌트 자신만이 &quot;소유&quot;하며, 내부적으로 생성 및 관리된다.</p>
</li>
<li><p><strong>변경 가능(Mutable)</strong><br />Props와 달리** State는 변경**할 수 있다. 
<code>setState</code> 또는 <code>useState</code>를 사용하여 값을 업데이트할 수 있으며, 상태가 변경될 때 React는 컴포넌트를 다시 렌더링한다.</p>
</li>
<li><p><strong>동적 UI 업데이트</strong><br />State를 활용하면 사용자 입력, API 응답, 애니메이션 등 다양한 동적인 상황을 처리할 수 있다.</p>
</li>
</ol>
<h3 id="state-예시">State 예시</h3>
<pre><code class="language-jsx">import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const increment = () =&gt; {
    setCount(count + 1);
  };

  return (
    &lt;div&gt;
      &lt;p&gt;Count: {count}&lt;/p&gt;
      &lt;button onClick={increment}&gt;Increment&lt;/button&gt;
    &lt;/div&gt;
  );
}</code></pre>
<p>위의 코드에서 <code>Counter</code> 컴포넌트는 내부 State로 <code>count</code>를 관리한다. 버튼을 클릭할 때마다 <code>setCount</code>를 호출해 State를 업데이트하면, 컴포넌트가 자동으로 재렌더링되어 새로운 상태를 화면에 표시한다.</p>
<hr />
<h2 id="🔎-props와-state의-차이점">🔎 Props와 State의 차이점</h2>
<table>
<thead>
<tr>
<th>구분</th>
<th>Props</th>
<th>State</th>
</tr>
</thead>
<tbody><tr>
<td><strong>데이터 소유권</strong></td>
<td>부모 컴포넌트로부터 전달됨</td>
<td>컴포넌트 내부에서 직접 관리</td>
</tr>
<tr>
<td><strong>변경 가능성</strong></td>
<td>읽기 전용 (변경 불가)</td>
<td>변경 가능 (자유롭게 수정 가능)</td>
</tr>
<tr>
<td><strong>데이터 흐름</strong></td>
<td>부모 → 자식 (단방향)</td>
<td>컴포넌트 내부에서만 관리</td>
</tr>
<tr>
<td><strong>주요 역할</strong></td>
<td>컴포넌트 간 데이터 전달 및 재사용성 향상</td>
<td>동적 데이터 처리, UI 업데이트</td>
</tr>
</tbody></table>
<hr />
<h2 id="️-언제-props를-사용하고-언제-state를-사용할까">⁉️ 언제 Props를 사용하고 언제 State를 사용할까?</h2>
<ul>
<li><p><strong>Props 사용 시점</strong><br />Props는 외부 데이터를 받아 렌더링해야 할 때 사용. 
부모 컴포넌트에서 전달된 데이터로 컴포넌트를 렌더링하고, 이를 통해 컴포넌트를 재사용 가능하게 만든다.<br />예를 들어, 버튼 텍스트나 헤더 제목처럼 외부에서 주어진 데이터만 표시하는 경우 Props가 적합.</p>
</li>
<li><p><strong>State 사용 시점</strong><br />State는 컴포넌트 내부에서 관리하는 데이터가 필요할 때 사용. 
사용자 입력에 따라 값이 바뀌거나, 시간이 지나면서 동적으로 변화하는 UI를 관리하려면 State를 이용해야 한다.<br />예를 들어, 사용자가 클릭한 횟수를 세거나, API 응답 데이터를 저장하여 화면에 표시할 때는 State가 적합.</p>
</li>
</ul>
<hr />
<h2 id="💡-결론">💡 결론</h2>
<p>Props와 State는 React에서 데이터를 관리하는 핵심적인 도구이다.  </p>
<ul>
<li><strong>Props는 읽기 전용으로, 부모 → 자식으로 전달되는 데이터</strong>이다.  </li>
<li><strong>State는 컴포넌트 내부에서 자유롭게 관리되고 변경되는 데이터</strong>이다.</li>
</ul>
<p>👉 이 둘을 적절히 구분하고 사용하는 것은 React 컴포넌트를 설계하고 유지보수하는 데 있어서 매우 중요함 </p>
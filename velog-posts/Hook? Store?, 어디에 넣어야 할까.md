<h1 id="✏️-시작하며-">✏️ 시작하며 ...</h1>
<p>최근에 팀원들과 폴더 구조를 정리하던 중 이런 이야기를 나누게 됐다.</p>
<p>“이건 hook에 넣는 게 맞지 않아? store로 가야 하나?”
“둘 다 상태를 저장하는데 뭐가 다른 거지 ㅠㅠ”</p>
<p>Hook도 상태를 다루고, Store도 상태를 다루니까 비슷해 보여서 헷갈릴 수밖에 없었다.
그래서 이번 기회에 Hook과 Store의 차이를 정리하고,
각 폴더에 어떤 파일을 넣어야 할지 명확하게 기준을 세워두려 한다‼️</p>
<hr />
<h1 id="🔧-hook-❓">🔧 Hook ❓</h1>
<h2 id="컴포넌트-안에서만-쓰는-개인-도구">컴포넌트 안에서만 쓰는 개인 도구</h2>
<p>Hook은 리액트 컴포넌트 내부에서 사용하는 작은 도구다.
대표적으로 <code>useState</code>, <code>useEffect</code>, <code>useRef</code> 같은 것들이 있고,
이 훅들은 컴포넌트 안에서만 작동하며, 컴포넌트가 사라지면 함께 사라진다.</p>
<h3 id="🩵-hook을-쓰는-상황">🩵 Hook을 쓰는 상황</h3>
<ul>
<li><p>입력값 제어</p>
</li>
<li><p>모달 열고 닫기</p>
</li>
<li><p>특정 컴포넌트에서만 필요한 UI 상태 </p>
</li>
</ul>
<p>등등 </p>
<pre><code class="language-javascript">function ProfileCard() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    &lt;div&gt;
      &lt;button onClick={() =&gt; setIsOpen(!isOpen)}&gt;
        {isOpen ? '닫기' : '더 보기'}
      &lt;/button&gt;
      {isOpen &amp;&amp; &lt;p&gt;추가 내용이 여기에!&lt;/p&gt;}
    &lt;/div&gt;
  );
}</code></pre>
<p>👉 이 <code>isOpen</code> 상태는 <code>ProfileCard</code> 안에서만 의미가 있다.
다른 컴포넌트에선 쓸 일도 없고, 알 필요도 없기 때문에 전역으로 뺄 이유가 없다.</p>
<h2 id="🧩-커스텀-훅-❓">🧩 커스텀 훅 ❓</h2>
<h3 id="반복되는-로직을-뽑아내는-나만의-훅">반복되는 로직을 뽑아내는 나만의 훅</h3>
<blockquote>
<p>여러 컴포넌트에서 같은 훅 로직이 반복될 경우, 
커스텀 훅으로 뽑아서 hooks/ 폴더에 따로 저장해두면 재사용이 쉬워진다.</p>
</blockquote>
<pre><code class="language-js">// hooks/useToggle.ts
import { useState } from 'react';

export default function useToggle(initial = false) {
  const [value, setValue] = useState(initial);
  const toggle = () =&gt; setValue((v) =&gt; !v);
  return [value, toggle] as const;
}</code></pre>
<pre><code class="language-js">// 사용하는 쪽
const [isOpen, toggle] = useToggle();</code></pre>
<p>👉 이렇게 하면 같은 토글 로직을 여러 곳에서 편하게 재사용할 수 있다.</p>
<hr />
<hr />
<h1 id="🏢-store❓">🏢 Store❓</h1>
<h2 id="여러-컴포넌트가-공유하는-중앙-상태-창고">여러 컴포넌트가 공유하는 중앙 상태 창고</h2>
<p><code>Store</code>는 앱 전체에서 공유할 수 있는 공용 상태 보관소다.
로그인 상태, 장바구니, 테마 설정 등처럼 여러 컴포넌트에서 접근해야 하는 데이터는 <code>store</code>에 넣는다.
나는 개인적으로 <code>Zustand</code>를 주로 사용하고 있다.</p>
<pre><code class="language-js">// store/userStore.ts
import { create } from 'zustand';

export const useUserStore = create((set) =&gt; ({
  username: '',
  login: (name) =&gt; set({ username: name }),
  logout: () =&gt; set({ username: '' }),
}));</code></pre>
<pre><code class="language-js">const { username, login, logout } = useUserStore();</code></pre>
<p>👉 Store에 저장된 상태는 여러 컴포넌트에서 동시에 접근 가능하고,
심지어 페이지를 이동해도 유지할 수 있다.</p>
<hr />
<hr />
<h1 id="💾-상태-유지성">💾 상태 유지성</h1>
<h2 id="hook은-일시적--store는-지속적">Hook은 일시적 / Store는 지속적</h2>
<p>Hook은 컴포넌트가 사라지면 함께 초기화된다.
반면 Store는 전역 상태이기 때문에 페이지 이동이나 컴포넌트 변경에도 유지된다.
또한 <code>localStorage</code>에 연결하면 브라우저를 껐다 켜도 유지할 수 있다.</p>
<pre><code class="language-js">// Zustand + persist 예시
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

export const useUserStore = create(
  persist(
    (set) =&gt; ({
      username: '',
      setUsername: (name) =&gt; set({ username: name }),
    }),
    {
      name: 'user-storage', // localStorage 키 이름
    }
  )
);</code></pre>
<h2 id="🔍-hook-vs-store">🔍 Hook vs Store</h2>
<table>
<thead>
<tr>
<th>구분</th>
<th>Hook</th>
<th>Store</th>
</tr>
</thead>
<tbody><tr>
<td>사용 범위</td>
<td>해당 컴포넌트 내부</td>
<td>전역 공유 가능</td>
</tr>
<tr>
<td>상태 유지</td>
<td>페이지 이동 시 초기화</td>
<td>유지되거나 localStorage에 저장 가능</td>
</tr>
<tr>
<td>주요 용도</td>
<td>모달, 입력폼 등 UI 조작</td>
<td>로그인, 장바구니, 테마 등 전역 상태</td>
</tr>
<tr>
<td>위치</td>
<td>컴포넌트 안</td>
<td>store 폴더</td>
</tr>
</tbody></table>
<h1 id="❓-그럼-모든-훅을-hooks-폴더에-넣는-건가">❓ 그럼 모든 훅을 hooks 폴더에 넣는 건가?</h1>
<p>처음에는 useState, useEffect 같은 것도 hooks/ 폴더에 넣어야 하나 고민했지만,
결론은,,! </p>
<blockquote>
<p>✅ 커스텀 훅만 hooks 폴더에 넣고, 기본 훅은 컴포넌트 안에서 사용한다.</p>
</blockquote>
<table>
<thead>
<tr>
<th>종류</th>
<th>예시</th>
<th>위치</th>
<th>이유</th>
</tr>
</thead>
<tbody><tr>
<td>기본 훅</td>
<td><code>useState</code>, <code>useEffect</code>, <code>useRef</code> 등</td>
<td>컴포넌트 안</td>
<td>컴포넌트 전용이기 때문</td>
</tr>
<tr>
<td>커스텀 훅</td>
<td><code>useToggle</code>, <code>useChatMessages</code> 등</td>
<td>hooks/ 폴더</td>
<td>재사용 가능한 로직이기 때문</td>
</tr>
</tbody></table>
<h1 id="✏️-커스텀-훅-네이밍-규칙">✏️ 커스텀 훅 네이밍 규칙</h1>
<p>1️⃣ use로 시작해야 한다</p>
<ul>
<li><p>useToggle, useScrollPosition</p>
</li>
<li><p>❌ toggleHook</p>
</li>
</ul>
<p>2️⃣ 기능을 명확히 드러내야 한다</p>
<ul>
<li>useAuth, useProductList, useDebounce</li>
</ul>
<p>3️⃣ 동작 → 대상 순으로 네이밍</p>
<ul>
<li>✅ useFetchUser, useDetectOutsideClick</li>
</ul>
<hr />
<h1 id="️결론">‼️결론</h1>
<p>👉 이 컴포넌트에서만 쓰는 상태면 <code>Hook</code>,
여러 컴포넌트에서 공유해야 한다면 <code>Store</code>.
그리고 재사용 가능하면 커스텀 훅으로 뽑아 <code>hooks/</code> 폴더에 넣는다!!!! </p>
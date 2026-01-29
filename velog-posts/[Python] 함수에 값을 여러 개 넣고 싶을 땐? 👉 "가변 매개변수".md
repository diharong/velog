<h1 id="✏️-파이썬-가변-매개변수">✏️ 파이썬 가변 매개변수</h1>
<h2 id="🔺서론">🔺서론</h2>
<p>정처기를 공부하다가 <code>가변 매개변수</code>라는 개념을 보고 이에 대해 정리해보고자 한다.  </p>
<hr />
<h2 id="❓-가변-매개변수란">❓ 가변 매개변수란?</h2>
<blockquote>
<p>함수를 만들 때 몇 개의 인자가 들어올지 <strong>모를 경우</strong>에 쓰는 매개변수다.</p>
</blockquote>
<p>예시를 보면 👇</p>
<pre><code class="language-python">def fruits(a, b, c):
    print(a, b, c)

fruits(&quot;사과&quot;, &quot;딸기&quot;, &quot;바나나&quot;)   # ✅ OK
fruits(&quot;사과&quot;, &quot;딸기&quot;)           # ❌ 에러
fruits(&quot;사과&quot;, &quot;딸기&quot;, &quot;바나나&quot;, &quot;수박&quot;)  # ❌ 에러</code></pre>
<p>➡️ 이 함수는 반드시 3개만 받을 수 있어서, 그 이상이나 이하를 넣으면 에러 난다.</p>
<p>✅ 이럴 때 가변 매개변수를 사용하면 된다.! </p>
<table>
<thead>
<tr>
<th>문법</th>
<th>설명</th>
<th>자료형</th>
</tr>
</thead>
<tbody><tr>
<td><code>*args</code></td>
<td>여러 개의 <strong>일반 값</strong>을 받을 때 사용</td>
<td>튜플</td>
</tr>
<tr>
<td><code>**kwargs</code></td>
<td>여러 개의 <strong>key=value</strong> 형태를 받을 때 사용</td>
<td>딕셔너리</td>
</tr>
</tbody></table>
<hr />
<p>🍎 <strong><code>*args</code> 예시</strong></p>
<pre><code class="language-python">def show_fruits(*args):
    print(&quot;🍓 받은 과일 목록:&quot;)
    for fruit in args:
        print(fruit)

show_fruits(&quot;딸기&quot;, &quot;바나나&quot;, &quot;수박&quot;)
show_fruits(&quot;포도&quot;, &quot;복숭아&quot;)</code></pre>
<p> ➡️ <strong>결과)</strong></p>
<pre><code>🍓 받은 과일 목록:
딸기
바나나
수박
🍓 받은 과일 목록:
포도
복숭아</code></pre><ul>
<li><code>*args</code>는 는 값을 여러 개 받아서 튜플로 저장</li>
<li>반복문으로 순회 가능</li>
</ul>
<hr />
<p>🔑 <strong><code>kwargs</code> 예시</strong></p>
<pre><code class="language-python">def show_profile(**kwargs):
    print(&quot;🧑‍💼 프로필 정보:&quot;)
    for key, value in kwargs.items():
        print(f&quot;{key}: {value}&quot;)

show_profile(이름=&quot;홍개발&quot;, 나이=20, 취미=&quot;헬스&quot;)</code></pre>
<p> ➡️ <strong>결과)</strong></p>
<pre><code>🧑‍💼 프로필 정보:
이름: 김개발
나이: 20
취미: 헬스</code></pre><ul>
<li><code>**kwargs</code>는 <code>key=value</code> 형식으로 값을 받아서 딕셔너리로 처리</li>
<li>어떤 정보든 자유롭게 넘길 수 있고, 개수 제한도 없음</li>
</ul>
<hr />
<hr />
<h2 id="🤔-그냥-def-sola-b-c-하면-안-돼">🤔 그냥 def sol(a, b, c) 하면 안 돼?</h2>
<blockquote>
<p>처음에는 그냥 매개변수를 정해두면 되는 거 아닌가 ? 생각했다. </p>
</blockquote>
<p>근데 아래처럼 하면 입력값의 개수가 딱 맞지 않으면 무조건 에러가 난다.</p>
<pre><code class="language-python">def fruits(a, b, c):
    print(a, b, c)

fruits(&quot;사과&quot;, &quot;딸기&quot;)  # ❌ 오류 (3개 필요)
fruits(&quot;사과&quot;, &quot;딸기&quot;, &quot;수박&quot;, &quot;참외&quot;)  # ❌ 오류 (3개만 받아야 함)</code></pre>
<p>➡️ 즉, 매개변수 개수가 고정되어 있는 함수는 유연하지 않다.</p>
<hr />
<h2 id="🧠-그럼-언제-써야-할까">🧠 그럼 언제 써야 할까?</h2>
<p><strong>1. 입력값 개수가 유동적일 때 → <code>*args</code></strong></p>
<pre><code class="language-python">def mix_juice(*fruits):
    print(&quot;🥤 과일 주스 재료들:&quot;)
    for fruit in fruits:
        print(fruit)

mix_juice(&quot;사과&quot;, &quot;딸기&quot;, &quot;바나나&quot;)
mix_juice(&quot;포도&quot;, &quot;자몽&quot;)</code></pre>
<ul>
<li>인자 개수가 정해져 있지 않을 때 편함</li>
<li>과일 몇 개 넣든 OK</li>
</ul>
<p><strong>2. 옵션 값이 다양할 때 → <code>kwargs</code></strong></p>
<pre><code class="language-python">def make_smoothie(**kwargs):
    print(&quot;🍹 스무디 옵션:&quot;)
    for k, v in kwargs.items():
        print(f&quot;{k}: {v}&quot;)

make_smoothie(과일=&quot;딸기&quot;, 얼음=&quot;많이&quot;, 당도=&quot;낮게&quot;)</code></pre>
<ul>
<li>옵션 키워드들이 많을 때 유리함</li>
<li>어떤 옵션이 들어올지 몰라도 다 받아서 처리 가능</li>
</ul>
<hr />
<h2 id="✨-args-kwargs-같이-쓰기">✨ <em>args, *</em>kwargs 같이 쓰기</h2>
<pre><code class="language-python">def describe_order(main_fruit, *extra_fruits, **options):
    print(&quot;메인 과일:&quot;, main_fruit)
    print(&quot;추가 과일:&quot;, extra_fruits)
    print(&quot;기타 옵션:&quot;, options)

describe_order(
    &quot;딸기&quot;,
    &quot;바나나&quot;, &quot;수박&quot;,
    당도=&quot;낮게&quot;, 얼음=&quot;보통&quot;
)</code></pre>
<p> ➡️ <strong>결과)</strong></p>
<pre><code class="language-python">메인 과일: 딸기
추가 과일: ('바나나', '수박')
기타 옵션: {'당도': '낮게', '얼음': '보통'}</code></pre>
<ul>
<li>순서: 일반 매개변수 → <code>*args</code> → <code>**kwargs</code></li>
<li>전부 한 번에 쓸 수도 있다!</li>
</ul>
<hr />
<hr />
<h2 id="📝-정리">📝 정리</h2>
<table>
<thead>
<tr>
<th>상황</th>
<th>일반 매개변수</th>
<th>가변 매개변수</th>
</tr>
</thead>
<tbody><tr>
<td>인자 수 고정</td>
<td>적합</td>
<td>❌</td>
</tr>
<tr>
<td>인자 수 유동적</td>
<td>❌ 에러 가능</td>
<td>✅ <code>*args</code></td>
</tr>
<tr>
<td>옵션이 자주 바뀜</td>
<td>❌ 함수 매번 수정</td>
<td>✅ <code>**kwargs</code></td>
</tr>
</tbody></table>
<hr />
<h2 id="💡-느낀-점">💡 느낀 점</h2>
<p>처음엔 단순히 &quot;그냥 여러 개 받는 기능인가 보다&quot; 했는데
직접 써보니까 이게 진짜 함수를 유연하게 만들어주는 무기라는 걸 깨달았다.</p>
<p>특히 앞으로 유틸 함수 만들 때,
<em>args랑 *</em>kwargs를 잘 써두면 엄청 깔끔하게 만들 수 있을 것 같음‼️</p>
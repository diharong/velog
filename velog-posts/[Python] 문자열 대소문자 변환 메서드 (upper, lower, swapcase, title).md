<h1 id="📌-파이썬-문자열-대소문자-변환-메서드-총정리-❗">📌 파이썬 문자열 대소문자 변환 메서드 총정리 ❗</h1>
<p>문자열의 대소문자 변환하는 알고리즘 문제를 풀다가 <code>swapcase</code> 라는 녀석을 알게 되어 이참에 파이썬의 문자열 변환 메서드들을 정리해본다!</p>
<hr />
<h2 id="1️⃣-upper--문자열을-모두-대문자로">1️⃣ <code>upper()</code> – 문자열을 모두 대문자로</h2>
<blockquote>
<p>문자열 내 모든 알파벳을 <strong>대문자</strong>로 변환한다.</p>
</blockquote>
<h3 id="✏️-예시">✏️ 예시</h3>
<pre><code class="language-python">text = &quot;hello World&quot;
print(text.upper())  #&quot;HELLO WORLD&quot;</code></pre>
<h3 id="🔥-특징">🔥 특징</h3>
<p>🔺소문자 → 대문자</p>
<p>🔺숫자, 특수문자, 공백은 그대로</p>
<p>🔺원본 문자열은 그대로이고 새 문자열을 반환함</p>
<h2 id="2️⃣-lower--문자열을-모두-소문자로">2️⃣ lower() – 문자열을 모두 소문자로</h2>
<blockquote>
<p>문자열 내 모든 알파벳을 <strong>소문자로 변환</strong>한다.</p>
</blockquote>
<h3 id="✏️-예시-1">✏️ 예시</h3>
<pre><code class="language-python">text = &quot;HeLLo PYTHON&quot;
print(text.lower())  #&quot;hello python&quot;</code></pre>
<h3 id="🔥-특징-1">🔥 특징</h3>
<p>🔺대문자 → 소문자</p>
<p>🔺원본 문자열은 변하지 않음</p>
<h2 id="3️⃣-swapcase--대소문자-뒤집기">3️⃣ swapcase() – 대소문자 뒤집기</h2>
<blockquote>
<p>소문자는 대문자로, 대문자는 소문자로 반대로 바꿔준다.</p>
</blockquote>
<h3 id="✏️-예시-2">✏️ 예시</h3>
<pre><code class="language-python">text = &quot;AbCdeF&quot;
print(text.swapcase())  # &quot;aBcDEf&quot;</code></pre>
<h2 id="4️⃣-title--각-단어의-첫-글자만-대문자로">4️⃣ title() – 각 단어의 첫 글자만 대문자로</h2>
<blockquote>
<p>문자열의 각 단어 <strong>첫 글자만 대문자</strong>, 나머지는 소문자로 바꾼다.</p>
</blockquote>
<h3 id="✏️-예시-3">✏️ 예시</h3>
<pre><code class="language-python">text = &quot;hello world from python&quot;
print(text.title())  #&quot;Hello World From Python&quot;</code></pre>
<h3 id="🔥-특징-2">🔥 특징</h3>
<p>🔺단어는 공백(space) 기준</p>
<p>🔺제목, 이름 포맷에 유용</p>
<p>⚠️ 중간 대문자도 소문자로 바뀔 수 있음 (예: &quot;iOS&quot; → &quot;Ios&quot;)</p>
<hr />
<hr />
<h2 id="전체-비교하기">전체 비교하기</h2>
<pre><code class="language-python">s = &quot;hELLo PyThOn WORLD&quot;

print(&quot;upper():&quot;, s.upper())       # HELLO PYTHON WORLD
print(&quot;lower():&quot;, s.lower())       # hello python world
print(&quot;swapcase():&quot;, s.swapcase()) # HellO pYtHoN world
print(&quot;title():&quot;, s.title())       # Hello Python World</code></pre>
<h2 id="✨-실전에서-어떻게-활용할까❓">✨ 실전에서 어떻게 활용할까❓</h2>
<p>✅ 사용자 입력 비교 (대소문자 구분 없이)</p>
<pre><code class="language-python">email = input().lower()
if email == &quot;admin@example.com&quot;:
    print(&quot;관리자 로그인&quot;)</code></pre>
<p>✅ 사용자 이름 포맷 맞추기</p>
<pre><code class="language-python">name = &quot;kim suji&quot;
print(name.title())  # Kim Suji</code></pre>
<p>✅ 문자열 뒤집기(디버깅용, 암호화 포맷 등)</p>
<pre><code class="language-python">temp = &quot;HeLLo123&quot;
print(temp.swapcase())  # hEllO123</code></pre>
<p>✅ 아이디, 이메일 저장 시 소문자로 정리</p>
<pre><code class="language-python">user_id = input(&quot;아이디: &quot;).strip().lower()</code></pre>
<h2 id="💡중요한-포인트️">💡중요한 포인트‼️</h2>
<p>이 메서드들은 <strong>모두 원본 문자열을 수정하지 않고, 새 문자열을 반환</strong>한다.
(파이썬 <strong>문자열은 immutable 즉, 불변 객체</strong>이기 때문!)</p>
<p>그래서 항상 다음처럼 다시 저장해줘야 한다는 걸 기억하자!</p>
<pre><code class="language-python">text = text.upper()  # 이걸 안 하면 변환이 반영되지 않음!</code></pre>
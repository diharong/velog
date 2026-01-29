<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/181860">프로그래머스 - 빈 배열에 추가, 삭제하기</a></p>
<blockquote>
<p>최근에 알고리즘 문제를 풀다가 아주 기초적인 메서드 차이에서 헤매는 경험을 했다.
바로 <code>append()</code>와 <code>extend()</code>의 차이‼️
평소에 큰 차이 없이 써왔는데, 이번 문제에서 확실하게 느꼈다.</p>
</blockquote>
<h1 id="✏️-문제-요약">✏️ <strong>문제 요약</strong></h1>
<pre><code class="language-bash">arr: 정수 배열
flag: arr와 같은 길이의 불리언 배열
flag[i]가 True이면, arr[i]를 arr[i]*2번 추가
False면, 배열 뒤에서 arr[i]개 삭제</code></pre>
<pre><code class="language-python">def solution(arr, flag):
    X = []
    for i in range(len(arr)):
        if flag[i]:
            X.append(arr[i]) * (arr[i] * 2)  # ❌ 이렇게 했다가 틀림
        else:
            del X[-arr[i]:]
    return X</code></pre>
<hr />
<h1 id="🔥내가-겪은-시행착오">🔥<strong>내가 겪은 시행착오</strong></h1>
<blockquote>
<p>처음에는 <code>append()</code> 뒤에 곱하기를 붙이면 알아서 여러 개가 들어갈 줄 알았다.
하지만 실제로는 아무 일도 일어나지 않았다.</p>
</blockquote>
<h2 id="🫤-why❓">🫤 WHY❓</h2>
<h3 id="🤯-append는-한-번에-하나만-넣는다">🤯 <code>append()</code>는 한 번에 <em>하나만</em> 넣는다</h3>
<pre><code class="language-python">X = []
X.append([3] * 5)

print(X)  # [[3, 3, 3, 3, 3]] ❌ 원하는 결과가 아님</code></pre>
<blockquote>
<p><code>append</code>는 리스트 전체를 <strong>하나의 &quot;요소&quot;</strong>로 넣는다.</p>
</blockquote>
<p>➡️ <em><strong>그래서 진짜 내가 원하는 건</strong></em></p>
<pre><code class="language-python">X.extend([3] * 5)

print(X)  # [3, 3, 3, 3, 3] </code></pre>
<h3 id="🍎-extend는-리스트-안-요소들을-하나씩-꺼내서-추가해준다">🍎 <code>extend()</code>는 리스트 안 요소들을** 하나씩 꺼내서 추가**해준다.</h3>
<p>💡그래서 <em><strong>같은 값을 여러 번 추가</strong>_하려면 _<strong>반드시 리스트</strong>_로 감싸고 **_extend()</em>**를 써야 한다‼️</p>
<hr />
<hr />
<h3 id="😥-pop도-실수했다">😥 pop도 실수했다</h3>
<blockquote>
<p>X.pop(arr[i])처럼 여러 개를 한 번에 제거할 수 있는 줄 알았다.</p>
</blockquote>
<p><strong>하지만 pop()은 하나씩만 제거 가능하다.</strong></p>
<pre><code class="language-python">X = [1, 2, 3, 4]
X.pop()        # 하나만 제거 가능
del X[-2:]     # ✅ 이렇게 슬라이싱으로 여러 개 제거 가능</code></pre>
<p><strong>최종 정답 코드</strong></p>
<pre><code class="language-python">def solution(arr, flag):
    X = []
    for i in range(len(arr)):
        if flag[i]:
            X.extend([arr[i]] * (arr[i] * 2))
        else:
            del X[-arr[i]:]
    return X</code></pre>
<hr />
<hr />
<hr />
<h1 id="✍️-배운-점">✍️ 배운 점</h1>
<p>🔵** 리스트를 여러 번 반복**해서 붙일 땐 <code>extend([값] * 반복수)</code> 패턴을 써야 한다.</p>
<p>🔵 <strong>여러 요소 삭제</strong>는 <code>pop(</code>이 아닌 <code>del</code>과 <code>슬라이싱</code>을 활용하자.</p>
<hr />
<h1 id="🔑-마무리">🔑 마무리</h1>
<p>기초라고 쉽게 넘겼던 부분에서 발목 잡힌 경험이었다.</p>
<p>이제부터는 메서드 하나라도 <strong>정확하게 의도를 가지고 써야겠다</strong>는 생각이 들었음!! </p>
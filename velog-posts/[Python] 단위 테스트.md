<h1 id="단위-테스트가-뭐야">단위 테스트가 뭐야?</h1>
<p>쉽게 말하면:</p>
<blockquote>
<p>“함수 하나가 제대로 동작하는지 자동으로 확인하는 것”</p>
</blockquote>
<p>예시:</p>
<pre><code class="language-python">def add(a, b):
    return a + b</code></pre>
<p>이게 제대로 작동하는지 사람이 직접 계산하지 않고
코드가 대신 확인하게 만드는 게 단위 테스트이다.</p>
<hr />
<h2 id="pytest">pytest?</h2>
<p>pytest는:</p>
<blockquote>
<p>“테스트를 실행해주고, 성공/실패를 판정해주는 프로그램”</p>
</blockquote>
<p>내가 할 일은
테스트 함수를 만들고
pytest가 그걸 실행하게 하는 것!</p>
<hr />
<h2 id="assert가-뭐냐">assert가 뭐냐?</h2>
<p>assert는:</p>
<blockquote>
<p>&quot;이게 맞으면 통과, 틀리면 실패&quot;</p>
</blockquote>
<p>예를 들어:</p>
<blockquote>
<p>assert 2 + 2 == 4</p>
</blockquote>
<p>이건 통과.</p>
<blockquote>
<p>assert 2 + 2 == 5</p>
</blockquote>
<p>이건 실패.</p>
<p>.</p>
<p>pytest는 이걸 보고:</p>
<p>맞으면 passed</p>
<p>틀리면 failed</p>
<p>라고 알려줌</p>
<hr />
<h2 id="실행해보자">실행해보자</h2>
<p>터미널에서:</p>
<p>pytest</p>
<p>성공하면:</p>
<p>2 passed</p>
<p>이렇게 나온다.</p>
<h2 id="일부러-실패시켜보자">일부러 실패시켜보자</h2>
<p>test_add를 이렇게 바꾸면</p>
<pre><code class="language-python">def test_add():
    assert add(2, 3) == 6</code></pre>
<p>그리고 다시 실행해.</p>
<p>실패가 나옴</p>
<p><img alt="터미널결과" src="https://velog.velcdn.com/images/diha01/post/9351f441-35f0-492f-b0f4-c9e5a51df41a/image.png" /></p>
<p>이게 중요!!</p>
<p>테스트는 “통과시키는 도구”가 아니라
“문제를 잡아내는 도구”!!!! </p>
<hr />
<h2 id="이제-한-단계-up-예외-테스트">이제 한 단계 up (예외 테스트)</h2>
<blockquote>
<p>divide(10, 0)을 하면 어떻게 될까?</p>
</blockquote>
<p>에러가 난다.</p>
<p>이걸 테스트로 검증해보자.</p>
<blockquote>
<p>test_calculator.py에 추가:</p>
</blockquote>
<pre><code class="language-python">import pytest

def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)</code></pre>
<p>여기서 새로운 개념:</p>
<p><code>pytest.raises</code>란?</p>
<blockquote>
<p>“이 코드가 특정 에러를 발생시키는지 확인하는 테스트”</p>
</blockquote>
<p>이게 진짜 단위 테스트 느낌.</p>
<hr />
<p>🔥 지금까지 한 게 뭐냐?</p>
<p>✔ 함수 테스트 해봤고
✔ 실패도 만들어봤고
✔ 예외도 테스트해봤다</p>
<hr />
<h2 id="📌-여기서-중요한-연결">📌 여기서 중요한 연결</h2>
<p>이제 이해해야 할 것:</p>
<p>UI 자동화 테스트도 똑같다.</p>
<p>차이점은:</p>
<blockquote>
<p>단위 테스트 → 함수 하나 검증</p>
</blockquote>
<blockquote>
<p>UI 테스트 → 화면 기능 하나 검증</p>
</blockquote>
<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59044">오랜 기간 보호한 동물(1)</a></p>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/16886b09-aae4-4431-b0c7-72df83ae7f97/image.png" />
<img alt="" src="https://velog.velcdn.com/images/diha01/post/98f73337-0e1c-4c16-87ac-75e5aa664df6/image.png" /></p>
<hr />
<h2 id="처음-구현">처음 구현</h2>
<blockquote>
<p>-- 입양을 못갔다 =&gt; INS 에는 있고, OUTS에는 없다.</p>
</blockquote>
<pre><code class="language-SQL">SELECT I.NAME, I.DATETIME
FROM ANIMAL_INS I
LEFT JOIN ANIMAL_OUTS O
ON O.ANIMAL_ID = I.ANIMAL_ID
WHERE O.ANIMAL_ID IS NULL 
ORDER BY DATETIME</code></pre>
<p>여기서 계속 오류가 났는데</p>
<p>상위 3마리만 나타내는 로직이 없었던 게 이유였다.</p>
<hr />
<h3 id="상위-3개만-조회하기-oracle">상위 3개만 조회하기 (Oracle)</h3>
<p>Oracle에서는 <code>LIMIT</code> 대신 <code>ROWNUM</code> 을 사용한다.</p>
<p>하지만 주의할 점이 있다.</p>
<p><code>ROWNUM</code></p>
<p>은 <code>ORDER BY</code> 보다 먼저 실행된다.</p>
<hr />
<p>그래서⭐</p>
<blockquote>
<p>정렬 → 3개 선택
순서로 처리하려면 서브쿼리가 필요하다.</p>
</blockquote>
<pre><code class="language-SQL">SELECT *
FROM (
    SELECT I.NAME, I.DATETIME
    FROM ANIMAL_INS I
    LEFT JOIN ANIMAL_OUTS O
    ON O.ANIMAL_ID = I.ANIMAL_ID
    WHERE O.ANIMAL_ID IS NULL
    ORDER BY I.DATETIME ASC
)
WHERE ROWNUM &lt;= 3;</code></pre>
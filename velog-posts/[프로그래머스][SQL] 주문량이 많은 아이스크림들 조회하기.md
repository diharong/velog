<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/025d418d-e8fe-4d87-918e-9c5f1a29d7d8/image.png" />
<img alt="" src="https://velog.velcdn.com/images/diha01/post/a7082cca-3ef4-4043-9253-1758393e0254/image.png" />
<img alt="" src="https://velog.velcdn.com/images/diha01/post/af0e74ed-86f7-47ed-9315-dc8442ab6285/image.png" /></p>
<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/133027">주문량이 많은 아이스크림들 조회하기</a></p>
<hr />
<h2 id="내가-쓴-코드">내가 쓴 코드</h2>
<pre><code class="language-SQL">SELECT *
FROM (
    SELECT F.FLAVOR
    FROM FIRST_HALF F 
    JOIN (
        SELECT FLAVOR, SUM(TOTAL_ORDER) AS TOTAL_ORDER
        FROM JULY 
        GROUP BY FLAVOR
    ) J

    ON F.FLAVOR = J.FLAVOR
    ORDER BY F.TOTAL_ORDER + J.TOTAL_ORDER DESC
)
WHERE ROWNUM &lt;= 3;
</code></pre>
<hr />
<hr />
<h2 id="다른-방법">다른 방법</h2>
<h3 id="union-all">UNION ALL</h3>
<pre><code class="language-SQL">SELECT FLAVOR 
FROM (
        SELECT FLAVOR
        FROM (
                SELECT FLAVOR, TOTAL_ORDER
                  FROM FIRST_HALF
                UNION ALL 
                SELECT FLAVOR, TOTAL_ORDER
                  FROM JULY
             )
        GROUP BY FLAVOR
        ORDER BY SUM(TOTAL_ORDER) DESC
     ) 
WHERE ROWNUM &lt;=3;</code></pre>
<p>UNION ALL 을 쓰면 중복 제거 없이 테이블이 합쳐진다.
이후 GROUP BY 를 통해 쿼리 작성하면 간단하게 끝! </p>
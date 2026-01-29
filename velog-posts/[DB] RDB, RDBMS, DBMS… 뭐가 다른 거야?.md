<h1 id="✏️-rdb-rdbms-dbms-란">✏️ RDB, RDBMS, DBMS 란!</h1>
<p>요즘 데이터베이스를 공부하며 헷갈렸던 부분을 기록하려한다.</p>
<blockquote>
<p><strong>RDB</strong>, <strong>RDBMS</strong>, <strong>DBMS</strong>… 이름도 비슷하고 다 같은 건 줄 알았는데 뭐가 뭔지 하나도 모르겠었음</p>
</blockquote>
<hr />
<h2 id="🟢-dbms-database-management-system">🟢 DBMS (DataBase Management System)</h2>
<p>먼저 제일 넓은 개념부터 start ! </p>
<p><strong>DBMS</strong>는 <strong>데이터베이스를 생성하고, 데이터를 읽고/쓰기/수정/삭제할 수 있도록 해주는 시스템(소프트웨어)</strong>이다.</p>
<p>쉽게 말해서, <strong>데이터를 다루기 위한 프로그램</strong>이라고 생각하면 됨.</p>
<h3 id="예시">예시:</h3>
<ul>
<li>RDBMS (관계형 DBMS) — MySQL, Oracle, PostgreSQL 등  </li>
<li>NoSQL DBMS — MongoDB, Redis, Cassandra 등</li>
</ul>
<p>즉, <strong>RDBMS는 DBMS의 한 종류</strong>인 것.  </p>
<p>여기서 잠깐‼️  </p>
<h3 id="🤔-그런데-nosql-dbms는-뭐지">🤔 그런데 NoSQL DBMS는 뭐지?</h3>
<blockquote>
<p>NoSQL = Not Only SQL</p>
</blockquote>
<p>이름처럼 &quot;SQL만 사용하는 게 아니라&quot;는 뜻
즉, 꼭 테이블(행과 열) 형태로 저장하지 않고, <strong>다양한 방식으로 데이터를 저장</strong>할 수 있는 DBMS이다. </p>
<p>관계형 데이터베이스와 달리 NoSQL 데이터베이스는 유연한 데이터 모델을 따르므로 <strong>자주 변경되는 데이터를 저장하거나 다양한 유형의 데이터를 처리</strong>하는 애플리케이션에 적합!</p>
<hr />
<h2 id="🟢-rdb-relational-database---관계형-데이터베이스">🟢 RDB (Relational DataBase) - 관계형 데이터베이스</h2>
<p>이제 많이 들어본 RDB!</p>
<blockquote>
<p>RDB는 데이터를 <strong>표(테이블)</strong> 형식으로 저장하는 방식 </p>
</blockquote>
<p>엑셀처럼 행(Row)과 열(Column)로 구성된다고 생각하면 됨.</p>
<p>예를 들어 이런 테이블이 있다면</p>
<table>
<thead>
<tr>
<th>id</th>
<th>이름</th>
<th>전화번호</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>홍길동</td>
<td>010-1111-2222</td>
</tr>
<tr>
<td>2</td>
<td>김영희</td>
<td>010-3333-4444</td>
</tr>
</tbody></table>
<p>이런 게 바로 <strong>RDB</strong>이다. 
그리고 테이블들끼리 <strong>관계(릴레이션)</strong>도 맺을 수 있음.
예: 고객 테이블과 주문 테이블이 고객 ID로 연결됨.</p>
<h3 id="관계relation가-중요한-이유">관계(Relation)가 중요한 이유</h3>
<p>RDB가 &quot;관계형&quot; 데이터베이스라고 불리는 핵심 이유는 이 관계 때문이다. </p>
<p>테이블 간에 관계를 설정함으로써,</p>
<ul>
<li>데이터 중복을 줄일 수 있음 (정규화)</li>
<li>데이터 일관성을 유지할 수 있음</li>
<li>복잡한 쿼리로 연관 데이터를 함께 조회할 수 있음</li>
</ul>
<p>고객 테이블</p>
<table>
<thead>
<tr>
<th>고객 ID</th>
<th>이름</th>
<th>이메일</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>홍길동</td>
<td><a href="mailto:hong@example.com">hong@example.com</a></td>
</tr>
<tr>
<td>2</td>
<td>김영희</td>
<td><a href="mailto:kim@example.com">kim@example.com</a></td>
</tr>
</tbody></table>
<p>주문 테이블</p>
<table>
<thead>
<tr>
<th>주문ID</th>
<th>고객ID</th>
<th>상품명</th>
<th>가격</th>
</tr>
</thead>
<tbody><tr>
<td>101</td>
<td>1</td>
<td>노트북</td>
<td>120,000</td>
</tr>
<tr>
<td>102</td>
<td>2</td>
<td>스마트폰</td>
<td>100,000</td>
</tr>
<tr>
<td>103</td>
<td>1</td>
<td>이어폰</td>
<td>9,000</td>
</tr>
</tbody></table>
<h2 id="여기서-고객id가-두-테이블을-연결하는-관계의-열쇠가-된다">여기서 고객ID가 두 테이블을 연결하는 관계의 열쇠가 된다.</h2>
<h2 id="🟢-rdbms-relational-database-management-system">🟢 RDBMS (Relational DataBase Management System)</h2>
<blockquote>
<p>RDBMS는 RDB(관계형 데이터베이스)를 <strong>관리해주는 프로그램</strong></p>
</blockquote>
<p>즉, <strong>테이블을 만들고</strong>,  
<strong>데이터를 넣고</strong>,  
<strong>삭제하고</strong>,  
<strong>검색하고</strong>,  
<strong>보안도 설정하고</strong>,  
<strong>트랜잭션도 처리해주는</strong> 도구이다. </p>
<h3 id="대표적인-rdbms">대표적인 RDBMS:</h3>
<ul>
<li>MySQL</li>
<li>Oracle</li>
<li>PostgreSQL</li>
<li>MariaDB</li>
<li>SQLite 등</li>
</ul>
<h3 id="sql-structured-query-language">SQL (Structured Query Language)</h3>
<p>RDBMS는 SQL이라는 표준화된 언어를 사용하여 데이터를 관리한다. SQL을 통해 데이터베이스에 명령을 내릴 수 있다:</p>
<pre><code class="language-sql">-- 데이터 조회
SELECT * FROM 고객 WHERE 이름 = '홍길동';

-- 데이터 추가
INSERT INTO 고객 (이름, 전화번호) VALUES ('이철수', '010-5555-6666');</code></pre>
<h3 id="트랜잭션transaction이란">트랜잭션(Transaction)이란?</h3>
<p><strong>트랜잭션(Transaction)</strong>은 데이터베이스에서 하나의 작업 단위</p>
<p>예: 은행 이체  </p>
<ol>
<li>A 계좌에서 10만 원 출금  </li>
<li>B 계좌에 10만 원 입금  </li>
</ol>
<p>이 두 개가 <strong>모두 성공해야만 최종 반영</strong>됨!  
하나라도 실패하면 전체 취소되어야 하는데,<br />이런 걸 <strong>트랜잭션</strong>이라고 함.</p>
<blockquote>
<p>✅ 트랜잭션은 <strong>안정성(ACID)</strong>을 보장하기 위한 핵심 기능!</p>
</blockquote>
<hr />
<h2 id="😸-세-가지-용어-정리">😸 세 가지 용어 정리</h2>
<blockquote>
<p>📦 <strong>RDB</strong> = 데이터를 저장하는 &quot;표&quot;<br />🧰 <strong>RDBMS</strong> = 그 표를 만들고 다루는 도구 (MySQL 같은 프로그램)<br />🧠 <strong>DBMS</strong> = 데이터베이스를 다루는 전체 프로그램 개념 (RDBMS도 이 안에 포함!)</p>
</blockquote>
<hr />
<h2 id="🔍-비교-정리">🔍 비교 정리</h2>
<table>
<thead>
<tr>
<th>용어</th>
<th>설명</th>
<th>예시</th>
</tr>
</thead>
<tbody><tr>
<td>DBMS</td>
<td>데이터를 저장하고 관리하는 모든 시스템</td>
<td>MySQL(RDBMS), MongoDB(NoSQL), Redis(NoSQL) 등</td>
</tr>
<tr>
<td>RDB</td>
<td>데이터를 테이블 형식으로 저장하는 구조</td>
<td>고객 테이블, 주문 테이블 등</td>
</tr>
<tr>
<td>RDBMS</td>
<td>RDB를 관리해주는 프로그램 (DBMS의 하위 개념)</td>
<td>MySQL, Oracle, PostgreSQL 등</td>
</tr>
</tbody></table>
<hr />
<h2 id="👉-결론">👉 결론</h2>
<ul>
<li><strong>DBMS</strong>는 전체적인 &quot;데이터베이스 관리 프로그램&quot;</li>
<li><strong>RDBMS</strong>는 그 중에서도 &quot;관계형(테이블 기반) 데이터베이스 관리 프로그램&quot;</li>
<li><strong>RDB</strong>는 데이터가 저장되는 &quot;형식&quot; (표 구조)</li>
</ul>
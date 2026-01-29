<h1 id="🐋-도커란-무엇일까">🐋 도커란 무엇일까?</h1>
<h2 id="❓🧐-내-컴퓨터에서는-잘-되는데-서버에서는-왜-안-될까">❓🧐 &quot;내 컴퓨터에서는 잘 되는데, 서버에서는 왜 안 될까?&quot;</h2>
<p>소프트웨어 개발을 하다 보면, 내 컴퓨터에서는 잘 실행되는데 다른 사람의 컴퓨터나 서버에서는 오류가 나는 경우가 많다.</p>
<p>이런 문제는 보통 <strong>환경 차이 때문</strong>이라고 볼 수 있다.</p>
<p>예를 들어, </p>
<ul>
<li>내 컴퓨터는 Python 3.9인데, 서버는 Python 3.6이라 실행이 안 됨</li>
<li>내 환경에서는 라이브러리가 설치되어 있는데, 서버에서는 누락됨</li>
<li>운영체제(OS)가 달라서 코드가 정상적으로 실행되지 않음</li>
</ul>
<h3 id="🔎-도커docker의-등장">🔎 도커(Docker)의 등장</h3>
<p>도커는 개발 환경을 통째로 패키징해서 <strong>어디서든 똑같이 실행할 수 있도록 만든 기술</strong>이다‼️</p>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/bfd640f0-2eda-46a7-8622-520bc042e8c9/image.png" /></p>
<p>도커를 사용하면 개발 환경을 _<strong>컨테이너(container)</strong>_라는 가벼운 실행 단위로 만들고,
이 컨테이너를 서버, 클라우드, 또는 다른 개발자의 컴퓨터에서도 동일하게 실행할 수 있다. </p>
<p>👉 쉽게 말해, <strong>&quot;내 컴퓨터에서 잘 되면, 어디서든 잘 되게 만드는 기술&quot;</strong> </p>
<blockquote>
<p>즉, 도커(Docker)는 <strong>컨테이너 기술을 활용하여 애플리케이션을 가볍고 일관된 환경에서 실행</strong>할 수 있도록 해주는 플랫폼.
기존 가상 머신과 달리, OS 전체를 가상화하지 않고, 애플리케이션만 격리하여 실행하기 때문에 가볍고 빠르다. </p>
</blockquote>
<h2 id="🔎-가상머신-vm-vs-도커-docker">🔎 가상머신 (VM) vs 도커 (Docker)</h2>
<p>도커와 비슷해 보이는 개념으로 <code>VM</code> 이 있는데, 
둘의 차이점을 알아보기 전, <code>VM</code> 의 개념부터 알아보고 가자.</p>
<h3 id="🦾-가상머신-vm-이란">🦾 가상머신 (VM) 이란</h3>
<blockquote>
<p>컴퓨터 안에 또 다른 가상의 컴퓨터를 만드는 기술</p>
</blockquote>
<h4 id="❓-왜-vm이-필요할까">❓ 왜 VM이 필요할까?</h4>
<p>예를 들어, 내 컴퓨터(Windows)에서 Linux 프로그램을 실행해야 한다고 생각해자.
<del>하지만 Windows에서는 Linux 프로그램이 실행되지 않는다..!</del></p>
<p>이럴 때 <strong>가상 머신(VM)</strong>을 사용하면,
Windows 안에 가상의 Linux 컴퓨터를 만들고 그 안에서 Linux 프로그램을 실행할 수 있다.</p>
<p>👉 즉, VM은 컴퓨터 안에서 또 다른 OS를 실행할 때 사용한다. </p>
<h4 id="🔍-vm의-특징">🔍 VM의 특징</h4>
<p>✔️ <strong>하드웨어를 가상화</strong> → 한 대의 컴퓨터에서 여러 운영체제 실행 가능
✔️** 독립적인 환경 제공** → 하나의 VM이 오류 나도 다른 VM은 영향 없음
✔️ <strong>리소스 무거움</strong> → 운영체제(OS) 전체를 실행하므로 속도가 느릴 수 있음</p>
<h3 id="🆚-가상머신-vm-vs-도커-docker-차이점">🆚 가상머신 (VM) vs 도커 (Docker) 차이점</h3>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/a987973e-773f-4494-bbdc-2c9fc940987d/image.png" /></p>
<table>
<thead>
<tr>
<th>항목</th>
<th align="left">가상 머신(VM)</th>
<th align="center">도커 컨테이너</th>
</tr>
</thead>
<tbody><tr>
<td>실행 방식</td>
<td align="left">OS 전체 가상화</td>
<td align="center">애플리케이션만 격리</td>
</tr>
<tr>
<td>속도</td>
<td align="left">느림 (운영체제 부팅 필요)</td>
<td align="center">빠름 (즉시 실행)</td>
</tr>
<tr>
<td>리소스 사용</td>
<td align="left">무거움 (RAM &amp; CPU 많이 소모)</td>
<td align="center">가벼움</td>
</tr>
<tr>
<td>배포 용이성</td>
<td align="left">OS별로 다름</td>
<td align="center">어디서나 동일하게 실행 가능</td>
</tr>
</tbody></table>
<blockquote>
<p>💡 쉽게 말해?<br />👉 VM은 컴퓨터(OS)를 통째로 가상화하는 기술
👉 도커는 애플리케이션만 가볍게 가상화하는 기술</p>
</blockquote>
<h2 id="📌-도커의-주요-개념">📌 도커의 주요 개념</h2>
<ul>
<li>이미지(Image)</li>
<li>컨테이너(Container)</li>
<li>도커 허브(Docker Hub) </li>
<li>도커 파일(Dockerfile)</li>
<li>도커 컴포즈(Docker Compose)</li>
</ul>
<p>를 들 수 있는데, 우선적으로</p>
<p>도커는 크게 <strong>이미지(Image)</strong>와 <strong>컨테이너(Container)</strong> 개념으로 나뉜다. </p>
<h3 id="🖼️-도커-이미지docker-image">🖼️ 도커 이미지(Docker Image)</h3>
<blockquote>
<p>애플리케이션 실행에 필요한 모든 것을 포함한 설정 파일</p>
</blockquote>
<p>(예: 프로그램, 라이브러리, 설정, 코드 등)</p>
<p>소프트웨어 설치 파일과 같다고 생각하면 됨.
한 번 만들면 변경되지 않고 <strong>재사용 가능</strong>.</p>
<h3 id="📦-도커-컨테이너docker-container">📦 도커 컨테이너(Docker Container)</h3>
<blockquote>
<p>이미지를 실제로 실행한 실행 환경</p>
</blockquote>
<p>마치 소프트웨어를 실행한 프로그램 창과 유사.
여러 개의 컨테이너를 동시에 실행할 수도 있음.</p>
<p>💡 비유하자면?
🍔 &quot;이미지 = 레시피&quot; 
🍽️ &quot;컨테이너 = 레시피대로 만들어진 햄버거&quot;</p>
<h4 id="🆚-도커-이미지와-컨테이너의-차이는">🆚 도커 이미지와 컨테이너의 차이는?</h4>
<blockquote>
<p>✅ <strong>도커 이미지</strong>는 애플리케이션 실행에 필요한 모든 파일과 설정이 포함된 템플릿이고,
<strong>도커 컨테이너</strong>는 이미지를 실제로 실행한 환경이다. 
이미지는 변하지 않지만, 컨테이너는 실행하면서 변경될 수 있음.</p>
</blockquote>
<h3 id="🏪-도커-허브docker-hub">🏪 도커 허브(Docker Hub)</h3>
<p>👉 &quot;앱 마켓 같은 곳&quot;</p>
<blockquote>
<p>도커 이미지를 저장하고 공유하는 공식 저장소</p>
</blockquote>
<p>예를 들어, 앱스토어에서 앱을 다운받듯이 필요한 소프트웨어(이미지)를 가져올 수 있다.</p>
<h3 id="📜-도커-파일dockerfile">📜 도커 파일(Dockerfile)</h3>
<p>👉 &quot;요리 레시피&quot;</p>
<blockquote>
<p>도커 이미지를 만들기 위한 설정 파일</p>
</blockquote>
<p>어떤 운영체제를 사용할지, 어떤 프로그램을 설치할지 등을 미리 정해서 <strong>자동으로 빌드</strong>할 수 있음. </p>
<p>즉, &quot;이 레시피대로 요리(이미지) 만들어줘!&quot; 하는 역할</p>
<h3 id="🎬-도커-컴포즈docker-compose">🎬 도커 컴포즈(Docker Compose)</h3>
<p>👉 &quot;세트 메뉴 조합&quot;</p>
<blockquote>
<p>여러 개의 컨테이너(서비스)를 한 번에 실행하고 관리하는 도구</p>
</blockquote>
<p>예를 들어, 웹 서버 + 데이터베이스 + 캐시 서버를 하나의 파일에 정리해서 한 번에 실행할 수 있다. </p>
<p>즉, &quot;이렇게 구성된 환경을 한 방에 실행해줘!&quot; 하는 역할</p>
<h2 id="🐋-그럼-도커는-어떻게-동작할까">🐋 그럼 도커는 어떻게 동작할까?</h2>
<h3 id="📦-컨테이너를-만드는-방법">📦 컨테이너를 만드는 방법</h3>
<p>컨테이너를 만들기 위해서는 총 3가지가 필요하다. </p>
<ul>
<li>도커파일 </li>
<li>이미지</li>
<li>컨테이너
<img alt="" src="https://velog.velcdn.com/images/diha01/post/12f41074-688a-4688-86b7-55341a69c554/image.png" /></li>
</ul>
<p>1️⃣ <strong>Dockerfile</strong></p>
<blockquote>
<p>컨테이너를 어떻게 만들어야 하는지에 대한 설명서.</p>
</blockquote>
<ul>
<li><p>어플리케이션을 구동하기 위한 파일은 무엇이 있는지</p>
</li>
<li><p>어떤 프레임워크나 라이브러리를 설치해야하는지에 대한 외부 dependencies를 명시할 수 있다. </p>
</li>
<li><p>필요한 환경변수를 설정할 수 있다. </p>
</li>
<li><p>어떻게 구동해야하는지에 대한 script도 포함할 수 있음.</p>
</li>
</ul>
<p>이렇게 작성한 도커 파일을 통해 이미지를 만들 수 있는데 </p>
<p>2️⃣ <strong>Image</strong> </p>
<blockquote>
<p>어플리케이션을 실행하는데 필요한 코드, 런타임, 환경, 시스템 툴, 시스템 라이브러리등이 포함</p>
</blockquote>
<p>👉 즉, 실행되고 있는 어플리케이션의 상태를 찰칵, 스냅샷하여 이미지로 만들어둔다고 생각하면 된다!</p>
<p><del><em>한번 만들어지면 변경이 불가능</em></del></p>
<p>3️⃣ <strong>Container</strong> </p>
<blockquote>
<p>Image를 고립된 환경에서 개별적인 시스템 안에서 실행할 수 있는 공간</p>
</blockquote>
<p><code>container</code> 안에서 <code>image</code>를 이용하여 어플리케이션이 구동한다.</p>
<blockquote>
<p>👉 객체지향에 익숙하다면 <code>Image</code> 를 <code>class</code> 의 개념으로 생각해도 좋다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/eb368e4b-5c92-4213-84a5-f23fc325ea1f/image.png" /></p>
<h2 id="🔎-그럼-어떻게-컨테이너를-배포할-수-있을까">🔎 그럼 어떻게 컨테이너를 배포할 수 있을까?</h2>
<p>깃과 깃허브와 같은 방식으로 동작한다. 
<img alt="" src="https://velog.velcdn.com/images/diha01/post/7a06ac02-39ee-4a79-9c7a-017692015551/image.png" /></p>
<p>1️⃣ 내 <strong>로컬 머신에서 이미지</strong>를 만든 후, 
2️⃣ 깃허브와 같은 <strong><code>Container Registry</code> **에</strong> 내가 만든 이미지를 <code>push</code>** 하고,<br />3️⃣ <strong>필요한 서버</strong>나 다른 개발자 pc 에서 내가 만들어둔 이미지를 가지고 와서 <strong>그대로 실행</strong>하면 완료된다.</p>
<p>‼️ 물론 이미지를 정상적으로 실행하기 위해서는 도커와 같은 <strong><code>Container Engine</code></strong> 을 꼭 설치해두어야 한다. </p>
<h3 id="🔎-컨테이너-레지스트리container-registry란">🔎 컨테이너 레지스트리(Container Registry)란?</h3>
<blockquote>
<p>컨테이너 이미지를 저장하고, 배포할 수 있는 저장소</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/cd88896e-c749-415c-b355-08b272a4fe26/image.png" /></p>
<p>이미지를 공유할 수 있는 <code>Container Registry</code> 에는 
<code>Public</code> 과 <code>Private</code> 이 있는데, </p>
<p>✔️ <strong>Public Container Registry (공개 레지스트리)</strong></p>
<ul>
<li>누구나 접근 가능</li>
<li>대표적인 서비스: Docker Hub, GitHub Packages, Google Container Registry (GCR)</li>
<li>오픈소스 프로젝트나 일반 개발자들이 많이 사용</li>
</ul>
<p>✔️ <strong>Private Container Registry (비공개 레지스트리)</strong></p>
<ul>
<li>특정 조직 또는 사용자만 접근 가능</li>
<li>보안과 내부 관리 목적</li>
<li>대표적인 서비스: AWS Elastic Container Registry (ECR), Google Artifact Registry, Azure Container Registry (ACR), 자체 구축한 Harbor</li>
<li>기업 환경에서 많이 사용</li>
</ul>
<p><code>Public</code>에는 도커 허브나 깃허브 패키지와 같은 것이 있고, 
(현재 기준으로 도커 허브가 더 많이 사용되고 있다.) </p>
<p>많은 개발자들이 <code>Public</code> 서비스를 이용하고 있지만 
회사에서는 보안적인 이유에서 대부분 <code>Private</code> 을 사용한다. </p>
<hr />
<h2 id="💡-도커의-장점">💡 도커의 장점</h2>
<p>1️⃣ 어디서든 동일한 환경 제공
2️⃣ 빠른 배포 및 실행 (OS 부팅 없이 바로 실행)
3️⃣ 리소스 효율적 사용 (VM보다 가볍고 빠름)
4️⃣ 쉽고 강력한 확장성 (여러 컨테이너를 조합 가능)</p>
<h4 id="➕-추가적으로-알고-가면-좋을-개념">➕ 추가적으로 알고 가면 좋을 개념</h4>
<p>❓** 도커 볼륨(Volume)**이란?</p>
<blockquote>
<p>✅ 컨테이너가 종료되더라도 <strong>데이터를 유지할 수 있도록 해주는 저장소</strong>
컨테이너 내부 파일 시스템은 기본적으로 휘발성이기 때문에, 데이터를 영구적으로 저장할 때 사용함. </p>
</blockquote>
<p>참고 및 이미지 출처 : <a href="https://www.youtube.com/watch?v=LXJhA3VWXFA">https://www.youtube.com/watch?v=LXJhA3VWXFA</a></p>
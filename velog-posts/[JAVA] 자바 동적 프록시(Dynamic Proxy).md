<h1 id="intro-정적-프록시를-구현한-뒤-생긴-의문점-❓">Intro. 정적 프록시를 구현한 뒤 생긴 의문점 ❓</h1>
<p>이전 글에서 자바 정적 프록시(Static Proxy) 를 직접 구현해 보았다.
Singer 인터페이스, 실제 객체 IU, 그리고 프록시 객체 IUManager를 만들어
프록시가 어떻게 부가 로직을 추가하고 실제 객체로 위임하는지 확인했다.</p>
<p>하지만 구현을 마친 뒤 자연스럽게 한 가지 문제가 드러났다.</p>
<p>“로직은 똑같은데
대상만 바뀔 때마다
프록시 클래스를 계속 만들어야 함?”</p>
<blockquote>
<p>IU → IUManager
BTS → BTSManager
NewJeans → NewJeansManager</p>
</blockquote>
<p>프록시의 핵심 로직은 거의 동일한데
대상 클래스만 다르다는 이유로 .java 파일이 계속 늘어나는 구조였다.</p>
<p>이 지점에서 정적 프록시의 한계를 체감했고
그 해결책으로 등장한 개념이 바로 동적 프록시(Dynamic Proxy) 였다.</p>
<h2 id="1-동적-프록시">1. 동적 프록시</h2>
<p>동적 프록시는 한 문장으로 정리할 수 있다.</p>
<p>프록시 클래스를 직접 만들지 않고
실행 시점(Runtime)에 자바가 대신 프록시 객체를 생성한다.</p>
<p>즉,</p>
<p>IUManager.java 같은 프록시 클래스를 직접 작성하지 않는다</p>
<p>대신
“이 프록시는 이렇게 행동해라”라는 <strong>규칙(핸들러)</strong> 만 정의한다</p>
<p>프록시의 몸체는 JVM이 만들고,
우리는 행동 방식만 정의하는 구조다.</p>
<h2 id="2-동적-프록시---두-가지-핵심-기술">2. 동적 프록시 - 두 가지 핵심 기술</h2>
<p>동적 프록시를 이해하기 위해
자바의 두 가지 기술을 순서대로 살펴보았다.</p>
<h3 id="1️⃣-invocationhandler--프록시의-두뇌">1️⃣ InvocationHandler – 프록시의 두뇌</h3>
<p>InvocationHandler는
프록시로 들어오는 모든 메서드 호출을 <strong>가로채는</strong> 인터페이스다.</p>
<pre><code class="language-java">public interface InvocationHandler {
    Object invoke(Object proxy, Method method, Object[] args);
}</code></pre>
<p>프록시 객체의 어떤 메서드를 호출하든</p>
<p>전부 <code>invoke()</code> 하나로 들어온다</p>
<p>즉,</p>
<p>“sing이든, dance든, save든
일단 여기로 들어와서 판단해라” 이거임.</p>
<p>정적 프록시에서
메서드마다 직접 구현하던 방식과 달리,
동적 프록시는 <strong><em>모든 메서드를 하나의 진입점에서 처리</em></strong>한다.</p>
<h3 id="2️⃣-reflection--실행-시점에-메서드를-호출">2️⃣ Reflection – 실행 시점에 메서드를 호출</h3>
<p>동적 프록시는
어떤 메서드가 호출될지 미리 알 수 없다..!</p>
<p>그래서 다음과 같은 방식이 필요해졌다.</p>
<pre><code class="language-java">method.invoke(target, args);</code></pre>
<p>이 코드 의미는</p>
<p>“지금 호출된 메서드(method)를
실제 객체(target)에게
전달받은 인자(args)로 실행해라”</p>
<p>즉,</p>
<blockquote>
<p>일반 호출: iu.sing() (컴파일 시점 결정)
리플렉션 호출: method.invoke() (실행 시점 결정)</p>
</blockquote>
<p>동적 프록시는 이 리플렉션 기반 호출을 통해
모든 메서드를 유연하게 처리한다.</p>
<h2 id="3-invocationhandler-구현--robotmanager">3. InvocationHandler 구현 – RobotManager</h2>
<p>동적 프록시의 행동 규칙을 직접 구현해 보았다.</p>
<pre><code class="language-java">public class RobotManager implements InvocationHandler {

    private final Object target;

    public RobotManager(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println(&quot;매니저가 바닥을 씁니다.&quot;);
        Object result = method.invoke(target, args);
        System.out.println(&quot;매니저가 인사를 합니다.&quot;);
        return result;
    }
}</code></pre>
<p>이 코드의 역할을 정리하면</p>
<blockquote>
<p>target
→ 실제 객체(Real Object)</p>
</blockquote>
<blockquote>
<p>invoke()
→ 프록시로 들어온 모든 호출의 단일 진입점</p>
</blockquote>
<blockquote>
<p>method.invoke(target, args)
→ 실제 객체에게 책임 위임</p>
</blockquote>
<p>정적 프록시에서
프록시 클래스가 담당하던 역할을
InvocationHandler 하나가 전부 담당하게 된 구조다.</p>
<h2 id="4-프록시-객체-생성--proxynewproxyinstance">4. 프록시 객체 생성 – Proxy.newProxyInstance</h2>
<p>이제 실제로 프록시 객체를 생성한다.</p>
<pre><code class="language-java">Singer realIU = new IU();

Singer robotProxy = (Singer) Proxy.newProxyInstance(
    Singer.class.getClassLoader(),
    new Class[]{Singer.class},
    new RobotManager(realIU)
);</code></pre>
<p>이 코드를 자연어로 풀면 </p>
<p>“Singer 인터페이스를 구현한 가짜 객체 하나를 만들고
그 가짜 객체의 모든 행동은 RobotManager에게 맡긴다.”</p>
<p>중요한 점은 다음과 같다.</p>
<p><em><strong>이 시점에는 아직 sing()이 실행되지 않는다</strong></em></p>
<p>단지 프록시 구조와 연결 관계만 생성된다</p>
<p>실제로 생성되는 클래스는
우리가 작성한 클래스가 아니라
JVM이 런타임에 만든 $Proxy0 같은 익명 클래스다.</p>
<h2 id="5-실제-실행-흐름">5. 실제 실행 흐름</h2>
<pre><code class="language-java">robotProxy.sing();</code></pre>
<p>이 한 줄이 실행되면 내부적으로 다음 순서가 발생한다.</p>
<blockquote>
<p>robotProxy.sing() 호출</p>
</blockquote>
<blockquote>
<p>JVM이 이를 invoke() 호출로 변환</p>
</blockquote>
<blockquote>
<p>RobotManager.invoke() 실행</p>
</blockquote>
<blockquote>
<p>전처리 로직 실행</p>
</blockquote>
<blockquote>
<p>method.invoke(target, args)로 실제 객체 호출</p>
</blockquote>
<blockquote>
<p>후처리 로직 실행</p>
</blockquote>
<blockquote>
<p>결과 반환</p>
</blockquote>
<p>즉, 흐름은 항상 다음 구조를 따른다.</p>
<blockquote>
<p>클라이언트
 → 프록시
   → InvocationHandler.invoke()
     → 실제 객체</p>
</blockquote>
<h2 id="6-동적-프록시의-장점과-정적-프록시와의-차이">6. 동적 프록시의 장점과 정적 프록시와의 차이</h2>
<h3 id="정적-프록시">정적 프록시</h3>
<p>프록시 클래스 직접 작성</p>
<p>대상마다 프록시 클래스 필요</p>
<p>구조는 직관적이나 확장성 한계 존재</p>
<h3 id="동적-프록시">동적 프록시</h3>
<p>프록시 클래스 작성 ❌</p>
<p>InvocationHandler 하나로 모든 대상 처리</p>
<p>실행 시점에 프록시 생성</p>
<p>반복 코드 제거 및 OCP 충족</p>
<h2 id="7-이-구조가-스프링spring-data-jpa으로-이어지는-순간">7. 이 구조가 스프링(Spring Data JPA)으로 이어지는 순간</h2>
<p>동적 프록시를 직접 구현해 보며
다음 사실을 자연스럽게 이해하게 되었다.</p>
<p>Spring Data JPA에서 Repository 인터페이스만 정의해도
실제 구현체 없이 동작하는 이유는
내부적으로 이와 동일한 동적 프록시 구조를 사용하기 때문이다.</p>
<p>우리가 만든 구조를 대응시키면 다음과 같다.</p>
<blockquote>
<p>Singer → UserRepository
RobotManager → 내부 InvocationHandler
Proxy.newProxyInstance() → 스프링 내부 프록시 생성 로직
$Proxy0 → 스프링 컨테이너에 등록되는 프록시 빈</p>
</blockquote>
<p>즉,
우리가 작성한 동적 프록시 실습은
스프링 내부 동작의 축소판이었다.</p>
<h1 id="outro">Outro.</h1>
<p>동적 프록시는 단순한 자바 문법이 아니라</p>
<p>왜 인터페이스만으로 동작이 가능한지</p>
<p>왜 구현체 없이도 메서드 호출이 가능한지</p>
<p>왜 실행 시점에 동작이 결정되는 구조가 필요한지</p>
<p>를 이해하기 위한 핵심 개념이었다.</p>
<p>즉, 이번 학습을 통해 
스프링이 왜 이런 구조를 선택했는지를
직접 구현하며 확인할 수 있었다.</p>
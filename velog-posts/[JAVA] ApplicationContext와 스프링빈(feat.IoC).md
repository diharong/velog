<h1 id="intro">Intro.</h1>
<p>이전 글에서 동적 프록시를 정리하면서 드는 의문이 있었다.</p>
<blockquote>
<p>프록시 객체는 스프링이 대신 만들어준다고 했는데?
그럼 그 객체들은 어디에서 누가 관리하는 걸까</p>
</blockquote>
<p>그러고 나서 스프링 코드를 다시 보니 이상한 점이 눈에 또 들어왔다.</p>
<pre><code class="language-java">private final UserRepository userRepository;

public HelloController(UserRepository userRepository) {
    this.userRepository = userRepository;
}</code></pre>
<p>UserRepository를 사용하고 있는데
new UserRepositoryImpl() 같은 코드는 어디에도 없다..!</p>
<p>자바를 처음 배울 때 이렇게 배웠었다.</p>
<blockquote>
<p>객체를 사용하려면 반드시 <code>new</code> 로 생성해야 한다.</p>
</blockquote>
<p>그런데 스프링에서는
객체를 만드는 코드가 없었다.</p>
<p>왜? 
이 질문을 해결하기 위해서 <code>ApplicationContext</code> 라는 것을 알아야한다.</p>
<hr />
<h2 id="applicationcontext">ApplicationContext</h2>
<p>이해를 돕기 위해 스프링 부트는 풀옵션오피스라는 비유를 찾아냈다.</p>
<p>🔨 순수 자바 시절</p>
<ul>
<li><p>개발자가 직접 객체를 만든다 (new)</p>
</li>
<li><p>직접 연결하고, 직접 관리한다</p>
</li>
<li><p>코드가 커질수록 객체 관계가 복잡해진다</p>
</li>
</ul>
<p>🏭 스프링을 쓰는 지금</p>
<ul>
<li><p>개발자는 입주민</p>
</li>
<li><p>객체 생성·관리·연결은 관리인</p>
</li>
<li><p>그 관리인이 바로 ApplicationContext</p>
</li>
</ul>
<p>👉 즉 ApplicationContext 는 애플리케이션 실행에 필요한 모든 객체를 생성, 보관, 연결하는 중앙 관리자다. 이것을 흔히 '<em><strong>스프링 컨테이너</strong></em>' 라고 부른다.</p>
<blockquote>
<p>그렇다! 내가 안 만든 것이 아니라 스프링이 대신 만들어서 보관하고 있었다.</p>
</blockquote>
<hr />
<h2 id="스프링-빈bean-이란">스프링 빈(Bean) 이란?</h2>
<p>그렇다면 스프링이 세상 모든 객체를 다 관리해줄까? </p>
<p>-&gt; ❌ No!!!</p>
<p>스프링은 신고된 객체만 관리한다.
이 등록된 객체를 스프링 빈(Bean)이라 한다. </p>
<p>그럼 등록은 어떻게 하나?
-&gt; 어노테이션을 이용한다.</p>
<pre><code class="language-java">@Component
@Service
@Repository
@Controller
@Bean</code></pre>
<p>이런 애노테이션이 붙은 클래스는
서버가 실행될 때 스프링이 스캔해서 자동으로 등록한다.</p>
<hr />
<h2 id="실제로-확인해보기">실제로 확인해보기</h2>
<p>그래서 실제로 ApplicationContext가
어떤 빈들을 들고 있는지 출력해 봤다.</p>
<pre><code class="language-java">package ding.co.hellospring;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.context.ApplicationContext;

@SpringBootTest
public class ApplicationContextInfoTest {

    @Autowired // @Autowired 를 통해서 spring application 내에서 관리하고 있는 등록되어있는 자재들을 불러오는 방법 중 하나
    ApplicationContext ac;

    @Test
    void findAllBean(){

        String[] allBeanNames = ac.getBeanDefinitionNames();// 이 팩토리안에 정의되어 있는 모든 빈을 가져온다.
// 여기서 빈이라는 것은 스프링 내부에서 관리하고 있는 자바 객체들을 의미한다.
        // 스프링 어플리케이션에 정말 다양한 자바의 객체들이 존재할 텐데 그것들을 전부 조회하는 방법이 바로 이것이다.

        for (String beanName: allBeanNames) {
            Object bean = ac.getBean(beanName);

            System.out.println(&quot;이름: &quot; + beanName + &quot;객체 정보&quot; + bean );
        }

    }
}</code></pre>
<p>1️⃣ <code>@Autowired</code>는 “컨테이너에 등록된 자재를 꺼내오는 방법”이다</p>
<p>주석에 이렇게 적어놨다.</p>
<blockquote>
<p>spring application 내에서 관리하고 있는 등록되어있는 자재들을 불러오는 방법 중 하나</p>
</blockquote>
<p>이때 내가 이해한 @Autowired는 이거였다.</p>
<p>새로 만드는 게 아니다</p>
<p>이미 스프링 애플리케이션 안에 등록돼 있는 것 중 하나를 꺼내오는 것</p>
<p>즉,</p>
<blockquote>
<p>ApplicationContext도
스프링이 관리하는 대상(빈) 중 하나</p>
</blockquote>
<p>라는 걸 여기서 처음 체감했다.</p>
<p>2️⃣ getBeanDefinitionNames() = “컨테이너 안에 정의된 전체 목록”</p>
<p>이 줄에 주석을 길게 적어둔 이유가 있다.</p>
<pre><code class="language-java">String[] allBeanNames = ac.getBeanDefinitionNames();</code></pre>
<blockquote>
<p>이 팩토리안에 정의되어 있는 모든 빈을 가져온다.</p>
</blockquote>
<p>여기서 포인트는 <strong>‘팩토리 안’</strong>이었다.</p>
<p>스프링 컨테이너 = 객체를 만들어두는 공장</p>
<p>getBeanDefinitionNames() = 그 공장에 등록된 전부를 꺼내보는 방법</p>
<p>그리고 바로 다음 주석이 이거였다.</p>
<blockquote>
<p>빈이라는 것은 스프링 내부에서 관리하고 있는 자바 객체들을 의미한다.</p>
</blockquote>
<p>이 주석을 적으면서
“아하 빈은 그냥 어려운 개념이 아니라
스프링이 관리 대상으로 삼은 자바 객체구나”라고 정리됐다.</p>
<p>3️⃣ “정말 다양한 자바 객체들이 존재한다”는 걸 실제로 봤다</p>
<p>주석에 이렇게 적어놨다.</p>
<blockquote>
<p>스프링 어플리케이션에 정말 다양한 자바의 객체들이 존재할 텐데
그것들을 전부 조회하는 방법이 바로 이것이다.</p>
</blockquote>
<p>이건 실행해 보고 나서 쓴 생각이다.</p>
<p>콘솔에는</p>
<p>org.springframework...로 시작하는 내부 빈들</p>
<p>웹, 설정, 트랜잭션 관련 객체들</p>
<p>그리고 중간쯤에 내가 만든
helloController, userService, userRepository</p>
<p>가 전부 섞여서 나왔다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/diha01/post/622cca9b-810b-42db-8fe8-943bbeeebc01/image.png" /></p>
<p>이걸 보고 확실히 알았다.</p>
<p>“내가 new로 만들지 않았던 객체들이
이미 스프링 안에 다 들어가 있었구나.”</p>
<p>4️⃣ 이름만 있는 게 아니라 “실제 객체”까지 꺼내진다</p>
<pre><code class="language-java">Object bean = ac.getBean(beanName);</code></pre>
<p>이름만 조회하는 게 아니라</p>
<p>실제 객체 인스턴스를 꺼내서 출력할 수 있었다</p>
<p>👉 스프링 컨테이너는 객체 저장소 그자체였다.</p>
<h3 id="🏢-applicationcontext는-뭐라고-이해하면-좋을까">🏢 ApplicationContext는 뭐라고 이해하면 좋을까?</h3>
<p>공식 정의는 어렵지만
내가 이해한 방식은 이랬다.</p>
<p>ApplicationContext는</p>
<blockquote>
<p>애플리케이션에서 쓸 객체들을 대신 만들어서 보관하고 있는 관리자</p>
</blockquote>
<p>서버가 뜰 때 한 번 싹 만들고</p>
<p>필요한 곳에 꺼내서 넣어준다</p>
<p>그래서 우리는 그냥 이렇게 쓰는 거다.</p>
<pre><code class="language-java">@Autowired
private UserService userService;</code></pre>
<p>“이거 필요해요”라고만 말하면
이미 준비된 걸 가져다 준다.</p>
<hr />
<h2 id="🤔-그럼-왜-내가-안-만들어도-됐을까">🤔 그럼 왜 내가 안 만들어도 됐을까?</h2>
<p>이 시점에서 핵심 질문이 바뀌었다.</p>
<p>“어떻게 가능한가?” ❌
→ “왜 이런 구조를 선택했을까?” ⭕</p>
<p>그리고 그 답이 바로
<strong>IoC (Inversion of Control)</strong>였다.</p>
<h2 id="ioc란-무엇인가--정의보다-먼저-상황으로-이해하기">IoC란 무엇인가 — 정의보다 먼저 ‘상황’으로 이해하기</h2>
<p>우리가 익숙했던 방식</p>
<pre><code class="language-java">OrderService service = new OrderService();</code></pre>
<p>내가 객체를 만든다</p>
<p>내가 생성 시점을 결정한다</p>
<p>내가 어떤 구현체를 쓸지 결정한다</p>
<p>즉, <strong>제어권(Control)</strong>이 전부 개발자에게 있었다.</p>
<hr />
<h2 id="스프링의-방식">스프링의 방식</h2>
<pre><code class="language-java">@Autowired
private OrderService orderService;</code></pre>
<p>나는 “필요하다”라고만 말한다</p>
<p>누가 만들었는지는 모른다</p>
<p>언제 만들어졌는지도 모른다</p>
<p>객체 생성과 연결의 주도권이 스프링으로 넘어간 것
이게 바로 <strong>제어의 역전(IoC)</strong>이다.</p>
<h2 id="🛠-그래서-이게-언제-좋을까">🛠 그래서 이게 언제 좋을까?</h2>
<p>1️⃣ 구현체를 바꿔야 할 때</p>
<pre><code class="language-java">// 나쁜 예
private final CardPayment payment = new CardPayment();</code></pre>
<p>→ 결제 수단이 바뀌면 코드 수정</p>
<pre><code class="language-java">// 좋은 예
private final PaymentPolicy payment;</code></pre>
<p>→ 구현체 교체는 설정에서만</p>
<p>2️⃣ 테스트할 때</p>
<ul>
<li><p>진짜 DB</p>
</li>
<li><p>진짜 은행</p>
</li>
<li><p>진짜 외부 API</p>
</li>
</ul>
<p>이걸 매번 호출하면서 테스트할 수는 없다.</p>
<p>IoC 덕분에
<strong>가짜 객체(Mock)</strong>를 넣어서
로직만 안전하게 검증할 수 있다.</p>
<h2 id="🧠-ioc가-없으면-어떤-문제가-생길까">🧠 IoC가 없으면 어떤 문제가 생길까?</h2>
<p>❌ IoC가 없는 코드</p>
<pre><code class="language-java">public class OrderService {
    private final CardPayment payment = new CardPayment();
}</code></pre>
<p>구현체에 강하게 묶인다</p>
<p>결제 수단이 바뀌면 코드 수정</p>
<p>테스트 시 가짜 객체 사용 불가</p>
<p>✅ IoC가 적용된 코드</p>
<pre><code class="language-java">public class OrderService {
    private final PaymentPolicy payment;

    public OrderService(PaymentPolicy payment) {
        this.payment = payment;
    }
}</code></pre>
<p>구현체 변경 가능</p>
<p>설정만 바꾸면 됨</p>
<p>테스트 시 Fake 객체 주입 가능</p>
<p>👉 그래서 IoC는 유연성과 테스트 가능성을 만든다.</p>
<hr />
<h1 id="outro">Outro.</h1>
<p>처음에는
new가 없는 코드가 이상했다.</p>
<p>지금은 오히려 이렇게 느껴진다.</p>
<blockquote>
<p>스프링의 핵심은
<strong>내가 다 하지 않아도 되게 만드는 구조</strong>였다.</p>
</blockquote>
<ul>
<li><p>객체 관리 → ApplicationContext</p>
</li>
<li><p>나는 역할만 정의</p>
</li>
<li><p>필요하면 요청만</p>
</li>
</ul>
<p>이제야 왜
스프링 코드에 new가 거의 등장하지 않는지,
그리고 그게 왜 좋은 설계인지 이해할 수 있었다.</p>
<p>다음 글에서는
“그럼 이 빈들은 언제 만들어지고, 언제 사라질까?”
→ 빈 생명주기 &amp; 싱글톤으로 이어서 정리해 볼 예정이다.</p>
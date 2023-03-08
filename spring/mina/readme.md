## 스프링 프레임워크란
> 자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크로써 엔터프라이즈급 애플리케이션을 개발하기 위한 모든 기능을 종합적으로 제공하는 경량화된 솔루션

`엔터프라이즈급 개발`이란 기업을 상대로 하는 개발을 뜻한다. 즉, 대규모 데이터 처리와 트랜잭션이 동시에 여러 사용자로부터 행해지는 매우 큰 규모의 환경을 이야기한다.

애플리케이션 개발을 빠르고 효율적으로 할 수 있도록 애플리케이션의 바탕이 되는 툴과 공통 프로그래밍 모델, 기술 API 등을 제공해준다.

스프링 프레임워크는 경량 컨테이너로 자바 객체를 담고 직접 관리한다. 객체의 생성 및 소멸 그리고 라이프 사이클을 관리하며 언제든 스프링 컨테이너로부터 필요한 객체를 가져와 사용할 수 있다.

이는 스프링이 IoC 기반의 프레임워크임을 의미한다.

스프링이 자바에서 가장 중요하게 가치를 두는 것은 바로 객체지향 프로그래밍이 가능한 언어라는 점이다.

그렇기에 스프링이 가장 관심을 많이 두는 대상은 오브젝트다. 스프링을 이해하려면 먼저 오브젝트에 깊은 관심을 가져야 한다.

### 스프링 컨테이너
스프링은 스프링 컨테이너 또는 애플리케이션 컨텍스트라고 불리는 스프링 런타임 엔진을 제공한다.</br>
스프링 컨테이너는 설정 정보를 참고로 해서 애플리케이션을 구성하는 오브젝트를 생성하고 관리한다.</br>
스프링 컨테이너는 독립적으로 동작할 수도 있지만 보통 웹 모듈에서 동작하는 서비스나 서블릿으로 등록해서 사용한다.

스프링은 세 가지 핵심 프로그래밍 모델을 지원한다.

#### IoC/DI
오브젝트의 생명주기와 의존관계에 대한 프로그래밍 모델

스프링은 유연하고 확장성이 뛰어난 코드를 만들 수 있게 도와주는 객체지향 설계 원칙과 디자인 패턴의 핵심 원리를 담고 있는 IoC/DI를 프레임워크의 근간으로 삼고 있다.


#### 서비스 추상화
스프링을 사용하면 환경이나 서버, 특정 기술에 종속되지 않고 이식성이 뛰어나며 유연한 애플리케이션을 만들 수 있는데, 이를 가능하게 해주는 것이 바로 서비스 추상화다.</br>
구체적인 기술과 환경에 종속되지 않도록 유연한 추상 계층을 두는 방법이다.


#### AOP
AOP는 애플리케이션 코드에 산재해서 나타나는 부가적인 기능을 독립적으로 모듈화하는 프로그래밍 모델이다. </br>
스프링은 AOP를 이용해서, 다양한 엔터프라이즈 서비스를 적용하고도 깔끔한 코드를 유지할 수 있게 해준다.

**reference** </br>
https://khj93.tistory.com/entry/Spring-Spring-Framework란-기본-개념-핵심-정리 </br>
토비의 스프링 3.1

## Spring, Spring MVC, Spring Boot 차이
### Spring
> Java에서 가장 인기 있는 애플리케이션 개발 프레임워크로, 주요 기능은 종속성 주입 또는 제어 반전(IoC)dlek.
> Spring Framework의 도움으로 느슨하게 결합된 애플리케이션을 개발할 수 있다.
> 애플리케이션 유형이나 특성이 순수하게 정의된 경우 사용하는 것이 좋다.

### Spring Boot
> 스프링 프레임워크의 모듈로, 이를 통해 최소 구성 또는 제로 구성으로 독립 실행형 애플리케이션을 구축할 수 있다.
> 단순한 스프링 기반 애플리케이션이나 RESTful 서비스를 개발하고 싶다면 사용하는 것이 좋다.

- 개발자가 스프링 기반 응용 프로그램을 빠르게 시작하고 쉽게 개발할 수 있도록 많은 복잡성을 뒤에 숨긴다.

|      | Spring                                                         | Spring Boot                                         |
|------|----------------------------------------------------------------|-----------------------------------------------------|
| 개념   | 응용 프로그램을 구축하기 위해 널리 사용되는 Java EE 프레임워크                         | REST API들을 개발하기 위해 널리 사용되는 프레임워크                    |
| 목표   | 개발자의 생산성을 향상시키는 자바 EE 개발을 단순화하는 것                              | 코드 길이를 줄이고 웹 응용 프로그램을 개발하는 가장 쉬운 방법을 제공하는 것         |
| 주요기능 | 의존성 주입                                                         | 자동 구성(Autoconfiguration), 요구 사항에 따라 클래스를 자동으로 구성    |
| help | 느슨하게 결합된(loosely coupled) 애플리케이션을 개발할 수 있게 함으로써 일을 더 단순하게 만든다. | 더 적은 구성으로 독립 실행형(stand-alone) 애플리케이션을 만드는 데 도움을 준다. |

### Spring MVC
> 웹 애플리케이션을 구축하기 위한 웹 MVC 프레임워크이다. 다양한 기능을 위한 구성 파일이 많이 포함되어 있다.
> HTTP 지향 웹 애플리케이션 개발 프레임워크이다.

**reference** </br>
https://m.blog.naver.com/sthwin/221271008423 </br>
https://dzone.com/articles/spring-boot-vs-spring-mvc-vs-spring-how-do-they-compare </br>
https://www.javatpoint.com/spring-vs-spring-boot-vs-spring-mvc


## Bean
> 스프링이 제어권을 가지고 직접 만들고 관계를 부여하는 오브젝트 </br>
> 스프링 컨테이너가 생성과 관계설정, 사용 등을 제어해주는 제어의 역전이 오브젝트, 즉 스프링이 IoC 방식으로 관리하는 오브젝트

**주의** </br>
스프링을 사용하는 애플리케이션에서 만들어지는 모든 오브젝트가 다 빈은 아니다. </br>
그 중에서 스프링이 직접 그 생성과 제어를 담당하는 오브젝트만을 빈이라고 부른다.

**reference** </br>
토비의 스프링 3.1

## Container
> IoC 방식으로 빈을 관리한다는 의미에서 애플리케이션 컨텍스트나 빈 팩토리를 컨테이너 또는 IoC 컨테이너라고도 한다. </br>

후자는 주로 빈 팩토리의 관점에서 이야기하는 것이고, 그냥 컨테이너 또는 스프링 컨테이너라고 할 때는 애플리케이션 컨텍스트를 가리키는 것이라고 보면 된다. </br>
컨테이너라는 말 자체가 IoC의 개념을 담고 있기 때문에 이름이 긴 애플케이션 컨텍스트 대신에 스프링 컨테이너라고 부르는 걸 선호하는 사람도 있다. </br>
애플리케이션 컨텍스트는 그 자체로 ApplicationContext 인터페이스를 구현한 오브젝트를 가리키기도 하는데, 애플리케이션 컨텍스트 오브젝트는 하나의 애플리케이션에서 보통 여러 개가 만들어져 사용된다. 이를 통틀어서 스프링 컨테이너라고 부를 수 있다.

때로는 컨테이너라는 말을 떼고 스프링이라고 부를 때도, 바로 이 스프링 컨테이너를 가리키는 것일 수도 있다.</br>
예를 들어 '스프링에 빈을 등록하고'라는 식으로 말하는 경우에 스프링이라는 말은 컨테이너 또는 애플리케이션 컨텍스트를 가리키는 말이다.

### 빈 팩토리
`스프링의 IoC를 담당하는 핵심 컨테이너`

빈을 등록하고, 생성하고, 조회하고 돌려주고, 그 외에 부가적인 빈을 관리하는 기능을 담당한다. </br>
보통은 이 빈 팩토리를 바로 사용하지 않고 이를 확장한 애플리케이션 컨텍스트를 이용한다. </br>
`BeanFactory`라고 붙여쓰면 빈 팩토리가 구현하고 있는 가장 기본적인 인터페이스의 이름이 된다. 이 인터페이스에 getBean()과 같은 메소드가 정의되어 있다.

### 애플리케이션 컨텍스트
`빈 팩토리를 확장한 IoC 컨테이너` 

빈을 등록하고 관리하는 기본적인 기능은 빈 팩토리와 동일하다. 여기에 스프링이 제공하는 각종 부가 서비스를 추가로 제공한다. <br>
빈 팩토리라고 부를 때는 주로 빈의 생성과 제어의 관점에서 이야기하는 것이고, 애플리케이션 컨텍스트라고 할 때는 스프링이 제공하는 애플리케이션 지원 기능을 모두 포함해서 얘기하는 것이라고 보면 된다. </br>
스프링에서는 애플리케이션 컨텍스트라는 용어를 빈 팩토리보다 많이 사용한다. ApplicationContext라고 적으면 애플리케이션 컨텍스트가 구현해야 하는 기본 인터페이스를 가리키는 것이기도 하다. <br>
ApplicationContext는 BeanFactory를 상속한다.

## IOC(Inversion of Control)
> 제어의 역전, 메소드나 객체의 호출작업을 개발자가 결정하는 것이 아니라, 외부에서 결정되는 것

객체의 의존성을 역전시켜 객체 간의 결합도를 줄이고 유연한 코드를 작성할 수 있게하여 가독성 및 코드 중복, 유지 보수를 편하게 할 수 있게 한다.

**기존의 실행 순서**
1. 객체 생성
2. 클래스 내부에서 의존성 객체 생성
3. 의존성 객체 메소드 호출

**스프링 실행 순서**
1. 객체 생성
2. 의존성 주입
   1. 스스로 만드는 것이 아니라 제어권을 스프링에게 위임해 스프링이 만들어놓은 객체를 주입한다.
3. 의존성 객체 메소드 호출

스프링이 실행될 때 모든 의존성 객체를 만들어주고 필요한 곳에 주입시켜줌으로써 스프링 빈은 `싱글턴 패턴`의 특징을 가지며, </br>
제어의 흐름을 사용자가 컨트롤하는 것이 아니라 스프링에게 맡겨 작업을 처리하게 된다.

**장점**
- 프로그램의 진행 흐름과 구체적인 구현을 분리시킬 수 있다.
- 개발자는 비즈니스 로직에 집중할 수 있다.
- 구현체 사이의 변경이 용이하다.
- 객체 간 의존성이 낮아진다.

### DI(Dependency Injection)
> 의존관계 주입, 스프링 IoC의 대표적인 동작원리는 주로 의존관계 주입이라고 불린다.

- 생성자 주입(Constructor Injection)
   - 스프링에서 권장하는 방식이다.
```
public class A {
  private B b;

  public A(B b) {
  this.b = b;
  }
}
```
- 세터 주입

```
public class A {
    private B b;

    public void setB(B b) {
        this.b = b;
    }
}
```

- 인터페이스 주입

```
  public interface BInjection {
  void inject(B b);
  }

   public A implements BInjection {
   private B b;

    @Override
    public void inject(B b) {
        this.b = b;
    }
}
```

**장점**
> DI 원칙으로 코드가 더 깔끔해지고, 객체에 의존성이 제공될 때 분리하는 것이 더 효과적입니다. 객체는 의존성을 조회하지 않으며 의존성의 위치나 클래스를 알지 못합니다. 결과적으로, 특히 의존성이 인터페이스 또는 추상 기본 클래스에 있는 경우 클래스를 테스트하기가 더 쉬워지며, 이를 통해 단위 테스트에서 스텁 또는 모의 구현을 사용할 수 있습니다.

- 의존성이 줄어든다.(변경에 덜 취약해진다.)
- 모의 객체를 주입할 수 있기 때문에 단위 테스트가 쉬워진다.
- 가독성이 높아진다.
- 재사용성이 높아진다.


**reference** </br>
https://velog.io/@gillog/Spring-DIDependency-Injection </br>
https://velog.io/@ohzzi/Spring-DIIoC-IoC-DI-그게-뭔데


## POJO(Plan Old Java Object)
> 특정 기술에 종속되지 않는 순수한 자바 객체로, 객체지향적인 원리에 충실하면서, 환경과 기술에 종속되지 않고 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트

**조건**
- 특정 규약(contract)에 종속되지 않는다.
  > 특정 규약을 따라 만들게 하는 경우 대부분 규약에서 제시하는 특정 클래스를 상속하도록 요구한다. 그럴 경우 자바의 단일 상속 제한 때문에 더 이상 해당 클래스에 객체지향적인 설계 기법을 적용하기가 어려워지는 문제가 생긴다. </br>
또한 규약이 적용된 환경에 종속적이 되기 때문에 다른 환경으로의 이전이 힘들다는 문제점이 있다.
- 특정 환경에 종속되지 않는다.
   > 그렇지 않을 경우 다른 환경에서 사용하기 어렵다. 또한 비즈니스 로직과 기술적인 내용을 담은 웹 정보 코드가 섞여 이해하기 어려워진다.
- 단일 책임 원칙을 지켜야 한다.
   > 책임과 역할이 다른 코드는 서로 다른 클래스로 나눠야 한다.

**장점**
- 특정한 기술과 환경에 종속되지 않는 오브젝트는 그만큼 깔끔한 코드가 될 수 있다.
  - 로우레벨의 기술과 환경에 종속적인 코드가 비즈니스 로직과 함께 섞여나오는 것만큼 지저분하고 복잡한 코드도 없다. 
  - 그런 코드는 개발하기도 힘들고, 오류를 찾고 디버깅하기도 힘들다. 코드를 읽고 이해하기도 어려울 뿐더러 검증이나 테스트 작성에도 한계가 있으므로 유지보수가 큰 부담이 된다.


- 자동화된 테스트에 매우 유리하다.
   - 어떤 환경에도 종속적이지 않은 POJO 코드는 매우 유연한 방식으로 원하는 레벨에서 코드를 빠르고 명확하게 테스트할 수 있다.


- 객체지향적인 설계를 자유롭게 적용할 수 있다.
  - 도메인 모델, 디자인 패턴 등은 POJO가 아니고서야 적용하기 힘들다.

**reference** </br>
https://www.nowwatersblog.com/springboot/springstudy/POJO </br>
토비의 스프링 3.1

## DAO와 DTO
### DAO(Data Access Object)
데이터베이스의 데이터에 접근하기 위한 객체로, 데이터베이스에 접근하기 위한 로직 & 비즈니스 로직을 분리하기 위해 사용한다.


### DTO(Data Transfer Object)
계층 간 데이터 교환을 하기 위해 사용하는 객체로, DTO는 로직을 가지지 않는 순수한 데이터 객체다. 

## MVC 패턴
**Model - View - Controller**의 약자로 애플리케이션을 세 가지 역할로 구분한 개발 방법론이다. </br>
<img src = "https://user-images.githubusercontent.com/70634740/223713174-fe03989b-dec9-413a-9b9d-c044e8adf217.png" width = "300" height = "300" />
<img src = "https://user-images.githubusercontent.com/70634740/223713293-dddc69e0-9a21-4b88-a649-7e296e6af258.png" width = "400" height = "300" /> </br>

### 특징
- 기본적으로 Blocking이고 동기 방식을 사용한다.
- 사용자의 요청이 들어올 때마다 Thread를 생성해 처리한다.
- 보통은 요청 시마다 스레드를 생성, 삭제해주면 일정한 리소스가 지속적으로 소모되므로 Thread를 미리 생성해 저장해두는 Thread Pool을 생성해 사용한다.
- 따라서 Spring MVC 같은 경우 요청이 들어오면 그 요청을 Queue에 쌓고 순서에 따라서 스레드를 하나 점유해 요청을 처리한다.
- 동시 다발적으로 스레드 수를 초과하는 요청이 발생하면 계속해서 요청이 큐에 대기하게 되는 Thread Pool Hell 현상이 발생할 수 있다.


### Model
**애플리케이션의 정보, 데이터를 나타낸다.**
- 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 한다.
- 뷰나 컨트롤러에 대해서 어떤 정보도 알면 안된다.
- 변경이 일어나면, 변경 통지에 대한 처리 방법을 구현해야만 한다.

### View
**사용자에게 보여지는 부분, 즉 유저 인터페이스를 의미한다.** </br>
MVC 패턴은 여러 개의 뷰가 존재할 수 있으며, 모델에게 질의하여 데이터를 전달받는다.

뷰는 받은 데이터를 화면에 표시해주는 역할을 하며, 모델에게 전달받은 데이터를 별도로 저장하지 않아야 한다.

사용자가 화면에 표시된 내용을 변경하게 되면 모델에게 전달해 모델을 변경해야 한다.

- 모델이 가지고 있는 정보를 따로 저장해서는 안된다.
- 모델이나 컨트롤러와 같이 다른 구성 요소들을 몰라야 한다.
- 변경이 일어나면 변경통지에 대한 처리방법을 구현해야만 한다.

### Controller
**모델과 뷰 사이를 이어주는 다리 역할을 의미한다.**

모델이나 뷰는 서로의 존재를 모르며, 변경 사항을 외부로 알리고 수신하는 방법만 있다.

컨트롤러는 이를 중재하기 위해 모델과 뷰에 대해 알고 있어야 하며, 모델이나 뷰로부터 변경 내용을 전달받으면 이를 각 구성 요소에게 통지해야 한다.

사용자가 애플리케이션을 조작하여 발생하는 변경 이벤트들을 처리하는 역할을 수행한다.

- 모델이나 뷰에 대해 알고 있어야 한다.
- 모델이나 뷰의 변경을 모니터링 해야 한다.

### 왜 사용할까?
`유지보수의 편리성`

최초 설계를 꼼꼼히 진행한 시스템이라도 유지보수가 발생하기 시작하면 각 기능간의 결합도(coupling)가 높아지는 경우가 발생한다.

이는 최초 설계 이념을 정했던 사람들의 부재 혹은 비즈니스 요건 변경으로 인해 필연적으로 발생한다.

결합도가 높아진 시스템은 유지보수 작업 시 다른 비즈니스 로직에 영향을 미치게 되므로 사소한 코드의 변경이 의도치 않은 버그를 유발할 수 있다.

MVC 패턴을 가진 시스템의 각 컴포넌트는 자신이 맡은 역할만 수행한 후 다른 컴포넌트로 결과만 넘겨주면 되기 때문에 시스템 결합도를 낮출 수 있다.

유지보수 시에도 특정 컴포넌트만 수정하면 되기 때문에 보다 쉽게 시스템 변경이 가능하다.

### 한계
복잡한 대규모 프로그램의 경우 다수의 뷰와 모델이 컨트롤러를 통해 연결되기 때문에 컨트롤러가 불필요하게 커지는 현상이 발생한다.

복잡한 화면을 구성하는 경우에도 동일한 현상이 발생하는데 이를 **'Massive-View-Controller'** 라고 한다. </br>

<img src = "https://user-images.githubusercontent.com/70634740/223713363-bda5f385-7400-4eb2-a492-26611da38417.png" width = "400" height = "200" /> </br>
https://www.infoq.com/news/2014/05/facebook-mvc-flux/

이러한 문제점을 보완하기 위해 다양한 패턴이 파생되었다.
- MVP 패턴
- MVVM
- Flux
- Redux
- RxMVVM

**reference** </br>
https://junhyunny.github.io/information/design-pattern/mvc-pattern/ </br>
https://thalals.tistory.com/381

## mvc vs webflux
### webflux
> Spring 5에서 새롭게 추가된 모듈로 클라이언트, 서버에서 reactive 스타일의 애플리케이션 개발을 도와준다.</br>
> reactive-stack web framework이며 non-blocking에 reactive stream을 지원한다.

**특징**
- Event-Driven 방식으로 요청을 처리하며 논블로킹 방식이다.
- 이벤트 루프가 돌아서 요청이 발생할 경우 그것에 맞는 핸들러에게 처리를 위임하고 처리가 완료되면 callback 메소드 등을 통해 응답을 반환한다.
- 이 방식의 경우 요청이 처리될 때까지 기다리지 않기 때문에 Spring MVC에 비해 사용자의 요청을 대량으로 받아낼 수 있다는 장점이 있다.

**장점**
- 고성능
- spring과 완벽한 통합
- netty 지원
- 비동기 non-blocking 메세지 처리

**단점**
- 다소 복잡한 오류 처리

### Spring MVC vs WebFlux
**공통점**
- @Controller, Reactive 클라이언트
  - 둘 다 tomcat, Jetty, Undertow와 같은 서버에서 실행할 수 있다.

**차별점**
- Spring MVC
  - 명령형 논리, JDBC, JPA를 가질 수 있다.
- Spring WebFlux
  - 기능적 엔드포인트, 이벤트 루프, 동시성 모델을 가질 수 있다.
  - Netty 서버에서 실행할 수 있다.

### mono, flux
Spring Webflux에서 사용하는 reactive library가 Reactor이고 Reactor가 Reactive Streams의 구현체다.<br>
그래서 Webflux 문서에 Reactive Streams가 언급되는 것이고 그와 같이 Reactor가 나오고 주요 객체인 Mono / Flux가 나오게 된다. </br>
결국 Webflux의 동작 구조를 이해하는 Flux와 Mono를 알고 넘어가야 한다.

Flux와 Mono의 차이점은 발생하는 데이터 갯수이다.
- Flux: 0 ~ N개의 데이터 전달
- Mono: 0 ~ 1개의 데이터 전달

**Mono**

Mono는 Reactive Steams의 Publisher 인터페이스를 구현하는 구현체이다.

**Flux**

Reactive Streams에서 정의한 Publisher의 구현체로서, 0-N개의 데이터를 발행(전달, 방출)할 수 있다. </br>
하나의 데이터를 전달할 때마다 onNext 이벤트를 발생시킨다. Flux 내의 모든 데이터의 전달 처리가 완료되면 onComplete 이벤트가 발생하며, 
데이터를 전달하는 과정에서 오류가 발생하면 onError 이벤트가 발생한다.


**Reference** </br>
https://devuna.tistory.com/108
https://devuna.tistory.com/120

## Filter와 Interceptor
스프링은 공통적으로 여러 작업을 처리함으로써 중복된 코드를 제거할 수 있는 3가지 기능을 지원한다. 

1. Filter
2. Interceptor
3. AOP(Aspect Oriented Programming, 관점 지향 프로그래밍)

### Filter
> 요청과 응답을 거른 뒤 정제하는 역할

Dispatcher Servlet에 요청이 전달되기 전후에 url 패턴에 맞는 모든 요청에 대해 부가 작업을 할 수 있는 기능 제공

스프링 컨테이너가 아닌 톰캣과 같은 웹 컨테이너에 의해 관리되며, 스프링 범위 밖에서 처리되는 것</br>

![img_3](https://user-images.githubusercontent.com/70634740/223713437-39fd0047-6729-40a8-a6b1-22a6861e5fa5.png)

필터를 초기화하기 위해서는 javax.servlet의 Filter 인터페이스를 구현해야 하며, 다음과 같은 메소드를 가진다.

```
public interface Filter {

  public default void init(FilterConfig filterConfig) throws ServletException {}

  public void doFilter(ServletRequest request, ServletResponse response,FilterChain chain) throws IOException, ServletException;

  public default void destroy() {}
```
1. init()
   - 필터 객체를 초기화하고 서비스에 추가하기 위한 메소드
   - 웹 컨테이너가 1회 init()을 호출해 필터 개체를 초기화하면 이후 요청들은 doFilter()를 통해 처리된다.


2. doFilter()
  - url-pattern에 맞는 모든 HTTP 요청이 디스패처 서블릿으로 전달되기 전에 웹 컨테이너에 의해 실행되는 메소드
  - doFilter의 파라미터로 FilterChain이 있는데, filterChain의 doFilter를 통해 다음 대상으로 요청을 전달할 수 있게 된다.
  - chain.doFilter()로 전후에 우리가 필요한 처리 과정을 넣어줌으로써 원하는 처리를 진행할 수 있다.

3. Destroy()
  - 필터 객체를 제거하고 사용하는 자원을 반환하기 위한 메소드
  - 웹 컨테이너가 1회 destroy()를 호출해 필터 객체를 종료하면 이후에는 doFilter에 의해 처리되지 않는다.


### Interceptor
> Dispatcher Servlet이 Controller를 사용하기 전후에 인터셉터가 끼어들어 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공한다. </br>
> 웹 컨테이너에서 동작하는 필터와 달리 인터셉터는 스프링 컨텍스트에서 동작한다.

디스패처 서블릿이 핸들러 매핑을 통해 컨트롤러를 찾도록 요청하는데, 그 결과로 실행 체인(HandlerExcutionChain)을 돌려준다. </br>
여기서 하나 이상의 인터셉터가 등록되어 있다면 순차적으로 인터셉터들을 거쳐 컨트롤러가 실행되도록 하고, 인터셉터가 없다면 바로 컨트롤러를 실행한다.

![img_4](https://user-images.githubusercontent.com/70634740/223713474-295cd2c2-30a0-4d06-b9d1-16e535c779ac.png)

인터셉터를 추가하기 위해서는 org.springframework.web.servlet의 HandlerInterceptor 인터페이스를 구현해야 하며, 다음과 같은 메소드들을 가진다.

```
public interface HandlerInterceptor {
 
	default boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
		return true;
	}
 
	default void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, @Nullable ModelAndView modelAndView) throws Exception {
	}
 
	default void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, @Nullable Exception ex) throws Exception {
	}
```

1. preHandle()
  - 컨트롤러가 호출되기 전에 실행된다.
  - 컨트롤러 이전에 처리해야 하는 전처리 작업이나 요청 정보를 가공하거나 추가하는 경우에 사용할 수 있다.

2. postHandle()
    - 컨트롤러가 호출된 후에 실행된다. (View 렌더링 전)
    - 컨트롤러 이후에 처리해야 하는 후처리 작업이 있을 때 사용할 수 있다.
    - 컨트롤러가 반환하는 ModelAndView 타입의 정보가 제공되는데, 최근에는 JSON 형태로 데이터를 제공하는 RestAPI 기반의 컨트롤러를 만들면서 자주 사용되지 않는다.

3. afterCompletion()
   - 모든 뷰에서 최종 결과를 생성하는 일을 포함해 모든 작업이 완료된 후에 실행된다. (View 렌더링 후)
   - 요청 처리 중에 사용한 리소스를 반환할 때 사용할 수 있다.

**인터셉터와 AOP**

인터셉터 대신 컨트롤러에 적용할 부가기능을 어드바이스로 만들어 AOP를 적용할 수도 있다. </br>
하지만 다음과 같은 이유로 컨트롤러의 호출 과정에 적용되는 부가기능들은 인터셉터를 사용하는 것이 낫다.

1. 컨트롤러는 타입과 실행 메소드가 모두 제각각이라 포인트컷(적용할 메소드 선별)의 작성이 어렵다.
2. 컨트롤러는 파라미터나 리턴 값이 일정하지 않다.

즉, 타입이 일정하지 않고 호출 패턴도 정해져 있지 않기 때문에 컨트롤러에서 AOP를 적용하려면 번거로운 부가작업들이 생기게 된다.

**필터와 인터셉터**

1. 필터는 Request와 Response를 조작할 수 있지만, 인터셉터는 조작할 수 없다.
2. 사용 사례
   1. 필터
      - 보안 및 인증/인가 관련 작업
      - 모든 요청에 대한 로깅 또는 검사
      - 이미지/데이터 압축 및 문자열 인코딩
      - Spring과 분리되어야 하는 기능
      - 스프링과 무관하게 전역적으로 처리해야 하는 작업들을 처리할 수 있으며, 인터셉터보다 앞단에서 동작하기 때문에 보안검사(XSS 방어 등)를 통해 올바른 요청이 아닐 경우 차단하 ㄹ수 있다.
      - 웹 애플리케이션에 전반적으로 사용되는 기능들을 구현하기에 적당하다.

   2. 인터셉터
      - 세부적인 보안 및 인증/인가 공통 작업
      - API 호출에 대한 로깅 또는 검사
      - 컨트롤러로 넘겨주는 정보(데이터)의 가공
      - 클라이언트의 요청과 관련되어 전역적으로 처리해야 하는 작업들을 처리할 수 있다.
      - HttpServletRequest나 HttpServletResponse 등과 같은 객체를 제공받으므로 객체 자체를 조작할 수 없다.
      - 대신 해당 객체가 내부적으로 갖는 값은 조작할 수 있으므로 컨트롤러로 넘겨주기 위한 정보를 가공하기에 용이하다.
      - ex) JWT 토큰 정보를 파싱해서 컨트롤러에게 사용자 정보를 제공하도록 가공
      
3. 필터와 인터셉터 모두 비즈니스 로직과 분리되어 특정 요구사항(보안, 인증, 인코딩 등)을 만족시켜야 할 때 적용한다.
4. 필터는 특정 요청과 컨트롤러에 관계없이 전역적으로 처리해야 하는 작업이나 웹 어플리케이션에 전반적으로 사용되는 기능을 구현할 때 적용하고,
인터셉터는 클라이언트의 요청과 관련된 작업에 대해 추가적인 요구사항을 만족해야 할 때 적용한다.

**Reference** </br>
https://dev-coco.tistory.com/173

## AOP(Aspect Oriented Programming, 관점 지향 프로그래밍)
> 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어 보고 그 관점을 기준으로 각각 모듈화하는 것

흩어진 관심사(Crosscutting Concerns)를 모듈화할 수 있는 프로그래밍 기법

![img_5](https://user-images.githubusercontent.com/70634740/223713513-8c06f7f5-203b-4b47-81fe-ee71a58d395f.png)

여기서의 색깔 블록은 중복되는 메서드, 필드, 코드 등이고

클래스 A의 주황색 블록 부분을 수정해야 한다면 클래스 B,C의 주황색 부분도 일일이 찾아 수정해야 한다.

-> SOLID 원칙을 위배하며 유지보수를 어렵게 만든다.

이런 식으로 소스 코드상에서 계속 반복해서 사용되는 부분을 `흩어진 관심사(Crosscutting Concerns)`라고 하며,

결국 각 관점을 기준으로 모듈화한다는 것은 흩어진 관심사를 모듈화하겠다는 의미이다.

이 때 모듈화시켜둔 블록을 `Aspect`라고 한다.

**특징**
- 스프링에서 제공하는 스프링 AOP는 프록시 기반의 AOP 구현체이다.
  - 따라서 AOP를 적용하려면 항상 프록시를 통해 대상 객체(Target)를 호출해야 한다.
  - AOP를 적용하면 스프링은 대상 객체 대신 프록시를 스프링 빈으로 등록한다. 
    - 따라서 스프링은 의존관계 주입 시 항상 프록시 객체를 주입한다.


- 프록시 객체를 사용하는 것은 접근 제어 및 부가 기능을 추가하기 위해서이다.


- 스프링 AOP는 스프링 Bean에만 적용할 수 있다.


- 모든 AOP 기능을 제공하는 것이 목적이 아닌 중복 코드, 프록시 클래스 작성의 번거로움 등 흔한 문제를 해결하기 위한 솔루션을 제공하는 것이 목적이다.


- 스프링 AOP는 순수 자바로 구현되었기 때문에 특별한 컴파일 과정이 필요하지 않다.

**reference** </br>
https://engkimbs.tistory.com/746 </br>
https://code-lab1.tistory.com/193


## 스프링 mvc에서 많은 요청이 발생할 때 생기는 상황

1. 스프링부트는 내장 서블릿 컨테이너인 Tomcat을 이용한다.
2. Tomcat은 다중 요청을 처리하기 위해서, 부팅할 때 스레드의 컬렉션인 Thread Pool을 생성한다.
3. 유저 요청(HttpServletRequest)이 들어오면 Thread Pool에서 하나씩 Thread를 할당한다.
4. 해당 Thread에서 스프링부트에서 작성한 Dispatcher Servlet을 거쳐 유저 요청을 처리한다.
5. 작업을 모두 수행하고 나면 스레드는 스레드풀로 반환된다.

**스레드풀의 기본 플로우**

1. 첫 작업이 들어오면, core size만큼의 스레드를 생성합니다.


2. 유저 요청(Connection, Server socket에서 accept한 소캣 객체)이 들어올 때마다 작업 큐(queue)에 담아둡니다.


3. core size의 스레드 중, 유휴상태(idle)인 스레드가 있다면 작업 큐에서 작업을 꺼내 스레드에 작업을 할당하여 작업을 처리합니다. 
   1. 만약 유휴상태인 스레드가 없다면, 작업은 작업 큐에서 대기합니다.
   2. 그 상태가 지속되어 작업 큐가 꽉 찬다면, 스레드를 새로 생성합니다.
   3. 3번과정을 반복하다 스레드 최대 사이즈 에 도달하고 작업큐도 꽉 차게 되면, 추가 요청에 대해선 connection-refused 오류를 반환합니다.


4. 태스크가 완료되면 스레드는 다시 유휴상태로 돌아갑니다.
   1. 작업큐가 비어있고 core size이상의 스레드가 생성되어있다면 스레드를 destory합니다.

즉, 스레드를 미리 만들어놓고 필요한 작업에 할당했다가 돌려받는다.



**refernece** 

https://velog.io/@sihyung92/how-does-springboot-handle-multiple-requests </br>
https://jeong-pro.tistory.com/204

## Spring JDBC를 통한 데이터 접근

`JDBC(Java Database Connectivity)`

> DB에 접근할 수 있도록 Java에서 접근하는 API(모든 Java의 Data Access 기술의 근간)

- 데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법 제공
- 문제점
  - 쿼리를 해결하기 전과 후에 많은 코드를 작성해야함(연결 생성, 명령문, ResultSet 닫기 등)
  - 데이터베이스 로직에서 예외 처리 코드를 수정해야 한다.
  - 트랜잭션을 처리해야 한다.
  - 이러한 코드의 반복으로 인한 시간 낭비

### JDBC Template
> Spring JDBC 접근 방법 중 하나로, 내부적으로 Plain JDBC API를 사용하지만 위와 같은 문제점을 제겅한 형태로 스프링이 제공하는 클래스

- 스프링 JDBC가 하는 일
  - Connection 열기 닫기
  - Statement 준비 닫기
  - Statement 실행
  - ResultSet Loop 처리
  - Exception 처리 및 반환
  - Transaction 처리

- 개발자가 할 일
  - 핵심적으로 해야 할 작업만 해주면 나머지는 Framework가 알아서 처리
  - datasource 작성
  - sql문 작성
  - 결과 처리

- JDBC Template이 제공하는 기능
  - 실행: Inser, Update와 같이 DB의 데이터에 변경이 일어나는 쿼리를 수행하는 작업
  - 조회: Select를 이용해 데이터를 조회하는 작업
  - 배치: 여러 개의 쿼리를 한 번에 수행해야 하는 작업

### JDBC Driver
자바 프로그램의 요청을 DBMS가 이해할 수 있는 프로토콜로 변환해주는 클라이언트 사이드 어댑터
- DB마다 Driver가 존재하므로 자신이 사용하는 DB에 맞는 JDBC Driver를 사용한다.
- DataSource를 JDBC Template에 주입(Dependency Injection) 시키고 JDBC Template은 JDBC Driver를 이용해 디비에 접근한다.


### Data Access Layer

![img](https://user-images.githubusercontent.com/70634740/223713552-b4894ace-5f6e-447c-8505-dd8c02a165a6.png)


#### DAO(Data Access Object)
- 실제로 DB에 접근하는 객체
- Service와 DB를 연결하는 고리 역할
- "Object" 단위 - SQL을 이용한 CRUD -> DB의 "record" 단위로 저장
  - 오브젝트와 레코드 간의 miss match 발생 가능

#### DataSource
JDBC 명세의 일부분이면서 일반화된 연결 팩토리

즉, DB와 관계된 connection 정보를 담고 있으며, bean으로 등록해 인자로 넘겨준다.

이 과정을 통해 스프링은 DataSource로 DB와의 연결을 획득한다.

**역할**
- DB Server와의 기본적인 연결
- DB Connection Pooling 기능
- 트랜잭션 처리

`DB Connection Pooling`
- 자바 프로그램에서 데이터베이스에 연결하는 것(Connection 객체를 얻는 것)은 시간이 오래 걸린다.
- 만약 일정량의 connection을 미리 생성시켜 저장소에 저장했다가 프로그램에서 요청이 있으면 저장소에서 Connection에서 꺼내 제공한다면 시간을 절약할 수 있다.
- 이러한 프로그래밍 기법을 Connecting Pooling 이라고 한다.
- 속도와 퍼포먼스를 향상시킨다.

**reference** </br>
https://gmlwjd9405.github.io/2018/05/15/setting-for-db-programming.html


## tomcat 내부구조

**reference**
https://byungmin.tistory.com/61

## 톰캣 기본 사이즈, 최대 사이즈
**JVM 메모리**

메모리 기본 설정값의 경우 아무 설정을 하지 않을 경우 jvm의 설정을 그대로 따라간다.

물리 메모리의 1/64를 초기 힙사이즈로 할당하고 1/4를 최대 힙사이즈로 할당한다.

Post로 넘길 수 있는 파라미너의 최대 크기: 2097152(2 megabytes)

최대 개수: 10,000개

(8.0 기준)


**reference**

https://mine-it-record.tistory.com/237

https://findmypiece.tistory.com/236

## N+1 문제
> 연관관계가 설정된 엔티티를 조회할 경우에 조회된 데이터 갯수(n)만큼 연관관계의 조회 쿼리가 추가로 발생하여 데이터를 읽어오는 현상

- WHEN: JPA Repository를 활용해 메소드를 호출할 때(Read)
- WHO: 1:N or N:1 관계를 가진 엔티티를 조회할 때 발생
- JPA Fetch 전략이 EAGER 전략으로 데이터를 조회하는 경우
- JPA Fetch 전략이 LAZY 전략으로 데이터를 가져온 이후에 연관 관계인 하위 엔티티를 다시 조회하는 경우
- WHY: JPA Repository로 find 시 실행하는 첫 쿼리에서 하위 엔티티까지 한 번에 가져오지 않고, 하위 엔티티를 사용할 때 추가로 조회하기 때문에
- JPQL은 기본적으로 글로벌 Fetch 전략을 무시하고 JPQL만 가지고 SQL을 사용하기 때문에

### EAGER(즉시 로딩)인 경우
1. JPQL에서 만든 SQL을 통해 데이터 조회
2. 이후 JPA에서 Fetch 전략을 가지고 해당 데이터의 연관 관게인 하위 엔티티들을 추가 조회
3. 2번 과정으로 N+1 문제 발생


### LAZY(지연 로딩)인 경우
1. JPQL에서 만든 SQL을 통해 데이터 조회
2. JPA에서 Fetch 전략을 가지지만, 지연 로딩이기 때문에 추가 조회는 하지 않음
3. 하지만 하위 엔티티를 가지고 작업하게 되면 추가 조회가 발생하기 때문에 결국 N+1 문제 발생


### 해결 방법
1. Fetch Join
  - 두 테이블을 조인하는 쿼리를 직접 작성
```
@Query("select DISTINCT o from Owner o join fetch o.pets")
List<Owner> findAllJoinFetch();
```

-> 쿼리가 한 번만 발생하고 미리 owner와 pet 데이터를 조인(Inner Join)해서 가져오는 것을 볼 수 있다.

**단점**
- 쿼리 한 번에 모든 것을 가져오기 때문에 JPA가 제공하는 Paging API 제공 불가능
- 1:N 관계가 두 개 이상인 경우 사용 불가
- 패치 조인 대상에게 별칭(as) 부여 불가능
- 번거로움

2. Entity Graph
  - Fetch Join과 동일하게 JPQL을 통해 쿼리를 작성하고, 필요한 연관관계를 EntityGraph에 설정하면 된다.

```
@EntityGraph(attributePaths = {"pets"})
@Query("select DISTINCT o from Owner o")
List<Owner> findAllEntityGraph();
```

-> 쿼리가 한 번만 발생하고 onwer와 pet의 데이터를 조인(Outer Join)해서 가져온다.

**주의점**
FetchJoin과 EntityGraph는 공통적으로 카테시안 곱(Cartesian Product)이 발생해 중복이 생길 수 있다.

`카테시안 곱`: 두 테이블 사이에 유효 join을 적지 않았을 때 해당 테이블에 대한 모든 데이터를 전부 결합해 테이블에 존재하는 행 갯수를 곱한만큼의 결과 값이 반환되는 것

이를 해결하기 위한 방법으로는 다음과 같은 것들이 있다.
1. JPQL에 DISTINCT를 추가해 중복 제거
2. OneToMany 필드 타입을 Set으로 선언해 중복 제거

**refernece**

https://dev-coco.tistory.com/165

# Spring

## Spring
- 보통 스프링이라는 말은 스프링 생태계를 통칭하는 말
- 스프링 자체는 자바(JVM) 플랫폼을 위한 애플리케이션 프레이웜크로 보통 동적 웹 사이트를 만드는데 활용
- 후술될 container, ioc, id, aop, mvc 같은 개념들이 스프링 프레임워크의 특징 또는 모듈이라고 할 수 있음

### 스프링 생태계
- 일반적으로 spring framework, spring boot를 필수로 사용하고, 애플리케이션의 목적에 따라서 spring data, spring cloud, spring security, spring session, spring batch 등의 프로젝트를 결합해서 사용
- [참고](https://spring.io/projects)

#### 스프링 프레임워크
- 핵심 기술 : 스프링 DI 컨테이너, AOP, 이벤트, etc.
- 웹 기술 : 스프링 MVC, 스프링 WebFlux
- 데이터 접근 기술 : 트랜잭션, JDBC, ORM 지원, XML 지원
- 기술 통합 : 캐시, 이메일, 원격 접근, 스케줄링
- 테스트 : 스프링 기반 테스트 지원
- 언어 : 코틀린, 그루비

#### 스프링 부트
- 스프링을 편리하게 사용할 수 있도록 지원, 최근에는 기본으로 사용
- 단독으로 실행할 수 있는 스프링 애플리케이션을 쉽게 생성
- Tomcat 같은 웹 서버를 내장해서 별도의 웹 서버를 설치하지 않아도 됨
- 편리한 빌드 구성을 위한 starter 종속성 제공
- 스프링과 서드파트(외부) 라이브러리 자동 구성
- 메트릭, 상태 확인, 외부 구성과 같은 프로덕션 준비 기능 제공

### 스프링 핵심 개념
- 자바 언어 기반의 프레임워크
- 자바 언어의 가장 큰 특징 : 객체 지향 언어
  - OOP 특징: 추상화, 캡슐화, 상속, 다형성
  - OOP 설계 방법: SOLID
  - 관련 내용은 [링크](https://velog.io/@ruthetum/spring-1-%EC%8A%A4%ED%94%84%EB%A7%81%EC%9D%B4%EB%9E%80) 참고
- 스프링은 객체 지향 언어가 가진 특징을 살려내는 프레임워크
- 스프링은 좋은 객체 지향 애플리케이션을 개발할 수 있게 돕는 프레임워크

## Bean 
- 스프링 컨테이너에 등록된 객체

## Container
- 파라미터로 넘어온 설정 클래스 정보(@Configuration)를 사용해서 스프링 빈을 등록

## DI(Dependency Injection), IOC(Inversion of Control)
### 의존성 주입
- 의존성이 있다 : 하나의 코드가 다른 코드를 사용
- 의존성 주입은 의존성이 있는 코드(객체)를 넣어준다
<img width="1127" alt="스크린샷" src="https://user-images.githubusercontent.com/59307414/222955659-2a97000d-bd54-4952-9fb5-62aaff1c932a.png">

ref. https://tecoble.techcourse.co.kr/post/2021-04-27-dependency-injection/

#### 방법
- **생성자 주입**
- 필드 주입
- 수정자 주입(setter 주입)

#### 어떤 걸 써야됨?
- 수정자 주입은 setter가 public하게 열려있기 때문에 취약하고,
- 필드 주입과 생성자 주입의 경우 bean이 생성된 후, 의존 객체를 주입하기 때문에 아래 문제점이 발생할 수 있음
  - 순환 참조 발생: 순환 참조가 발생할 경우 빈 생성 시점에는 에러를 확인할 수 없음
  - NullPointerException 발생: 객체가 생성된 후 주입하기 때문에 실제 코드가 호출되기 전까지는 NullPointerException을 알 수 없음
  - 불변 객체를 생성하지 못함: 객체 생성 후 주입하기 때문에 당연히 불변 객체로 생성하지 못함
- 따라서 위 문제를 방지할 수 있는 생성자 주입을 권장

ref. https://dev-coco.tistory.com/70

### 제어의 역전
- 개발자가 직접 제어하는 것이 아닌 외부에서 제어 및 관리해주는 것
<img width="953" alt="스크린샷" src="https://user-images.githubusercontent.com/59307414/222955666-0ccd4b7c-36d7-4ead-a860-d7576086bfc2.png">

<img width="884" alt="스크린샷" src="https://user-images.githubusercontent.com/59307414/222955665-7c23bc4e-87b2-4df1-aaf3-5ddb88f21ed1.png">

### 장점
- 의존성 감소
- 코드양 감소
- 테스트 용이

## POJO(Plan Old Java Object)
- 직역하면 오래된 방식의 간단한 자바 오브젝트
- 다양한 프레임워크들이 등장하면서 특정 기술과 환경에 종속되어 의존하게 된 자바 코드들이 작성되었고, 이로 인해 가독성이 떨어져 유지보수가 어렵고 확장성이 매우 떨어지는 단점이 발생
- 이는 객체지향 언어인 자바가 객체지향의 장점들이 사라지기 때문에 POJO 개념 등장
- **객체지향적인 원리에 충실하면서, 환경과 기술에 종속되지 않고 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트**

---

## DAO(Data Access Object), DTO(Data Transfer Object)
- DAO: 데이터베이스에 접근하기 위한 객체
  - ex. repository 객체
- DTO: 계층 간 데이터 교환을 하기 위해 사용하는 객체

<img width="773" alt="스크린샷" src="https://user-images.githubusercontent.com/59307414/222956431-1125ba1e-f797-4445-a88a-118a44ccc495.png">

## MVC pattern
- Model: 데이터를 담당
- View: 사용자에게 보여지는 화면을 담당
- Controller: 사용자의 요청을 받아서 처리하고, 그 결과를 보여줄 View를 선택

## Spring MVC vs Spring WebFlux
### 동기/비동기, 블로킹/논블로킹
- 동기: 함수 A가 함수 B를 호출한 뒤, 함수 B의 리턴값을 계속 확인
- 비동기: A가 함수 B를 호출할 때 콜백 함수를 함께 전달, B 작업이 완료될 때 콜백함수가 실행 (A는 B 함수의 작업 완료 여부를 신경쓰지 않음)
> 동기 vs 비동기 : 호출한 함수의 작업 완료 여부를 확인하느냐
- 블로킹: A 함수가 B 함수를 호출하면, 제어권을 A가 호출한 B 함수에게 전달
- 논블로킹: A 함수가 B 함수를 호출해도 제어권은 그대로 A가 가지고 있음
> 블로킹 vs 논블로킹 : 제어권을 어떻게 처리하느냐

ref. https://velog.io/@nittre/%EB%B8%94%EB%A1%9C%ED%82%B9-Vs.-%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9-%EB%8F%99%EA%B8%B0-Vs.-%EB%B9%84%EB%8F%99%EA%B8%B0

### MVC vs WebFlux
#### MVC
- 동기 + 블로킹
- 멀티 스레드 형태로 작업을 처리
- 요청마다 스레드를 생성하는 것은 코스트가 크기 때문에 미리 스레드풀을 생성해서 작업을 처리
  - 사용자가 동시에 많은 요청을 하는 경우? -> 후술할 Thread pool hell 현상
- 결국 사용자의 요청마다 스레드를 할당(생성)해서 작업 처리
- 기본 스레드 수는 200

#### WebFlux
- 비동기 + 논블로킹
- node처럼 이벤트 루프(싱글 스레드) 존재
- 이벤트 루프가 돌면서 요청이 발생하면 핸들러를 요청 처리 위임, 처리 완료 시 콜백 함수를 통해 응답 반환
- MVC에 비해 요청을 많이 받을 수 있음

### Mono, Flux
- Mono : 0 또는 1 개의 데이터 전달
- Flux : 0 ~ N 개의 데이터 전달
  - 0 또는 1인 경우 Mono를 사용

### Spring MVC 에서 많은 요청이 발생할 때 생기는 상황
- Thread Pool Hell 현상
  - 스레드를 할당받기 위해 대기하고, 그로 인해 latency 발생
- ref. https://devahea.github.io/2019/04/21/Spring-WebFlux%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%A0%81%EC%9D%80-%EB%A6%AC%EC%86%8C%EC%8A%A4%EB%A1%9C-%EB%A7%8E%EC%9D%80-%ED%8A%B8%EB%9E%98%ED%94%BD%EC%9D%84-%EA%B0%90%EB%8B%B9%ED%95%A0%EA%B9%8C/

## Filter, Interceptor
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9983FB455BB4E5D30C)
- Interceptor와 Filter는 Servlet 단위에서 실행
  - Filter는 Dispatcher Servlet 앞단, Interceptor는 뒷단
- AOP는 메소드 앞에 Proxy패턴의 형태로 실행
- Filter와 다르게 Interceptor는 Spring Context, Spring Bean을 활용할 수 있음
  - Filter는 스프링 컨텍스트 외부에 존재하기 때문에 Spring과 무관한 자원에 대한 처리를 담당

## AOP(Aspect-Oriented Programming)
- AOP는 애스펙트를 사용한 프로그래밍 방식을 관점 지향 프로그래밍을 의미
  - 애스팩트(aspect): 부가 기능과 부가 기능을 어디에 적용할지 선택하는 기능을 합해서 하나의 모듈로 만드는 것
  - AOP는 OOP를 대체하기 위한 것이 아니라 횡단 관심사를 깔끔하게 처리하기 어려운 OOP의 부족한 부분을 보조하는 목적으로 개발

- Spring AOP의 구현은 이전 강의 혹은 아래 자료 참고

ref. https://github.com/ruthetum/my-spring/edit/main/i-advanced/aop/readme.md

---

## Spring JDBC를 통한 데이터 접근
- JDBC(JAVA Database Connectivity): 자바에서 데이터베이스에 접근하기 위한 API
- Spring에서 JDBCTemplate을 이용해서 데이터 처리
  - 템플릿 콜백 패턴 사용
    - 전략 패턴을 변환한 형태
    - 템플릿(슈퍼 클래스)을 유지하고, 서브 클래스의 메서드를 바꾸는 형태로 작동
      - 변화되는 부분을 매번 클래스로 만들지 않음 -> 익명 내부 클래스로 바로 생성해서 사용
    - 콜백: 다른 객체에 전달되는 객체를 의미

## TOMCAT 
### 내부 구조
- 자바 기반의 웹 서버로 tomcat 위에서 스프링이 돌아감
- 스프링(mvc)에서 디스패처 서블렛을 통해 모든 요청을 입력받는데 이 서블렛이 tomcat에서 제공하는 서블렛 컨테이너에서 수행
  - 서블릿의 라이프사이클을 관리하는 것이 서블릿 컨테이너
- 즉 spring container(spring application context)에 진입 전 단계인 서블렛 컨테이너를 톰캣에서 수행

### 기본 설정
- 기본 메모리(heap) 사이즈는 64MB
  - 간혹 이 메모리 부족으로 문제가 발생할 수 있음

### Spring JPA 에서 N+1 문제
#### N+1 문제란?
- 연관 관계에서 발생하는 이슈로 연관 관계가 설정된 엔티티를 조회할 경우에 조회된 데이터 갯수(n) 만큼 연관관계의 조회 쿼리가 추가로 발생하여 데이터를 읽어오는 문제
- 한 팀에 여러 멤버가 존재하고, 멤버는 팀에 종속되어 있을 때 팀을 조회(1번 조회)하면 멤버를 조회하는 쿼리(팀이 N개이면, N번 조회)가 추가로 조회 

#### 원인
- JPA에서는 메서드 이름을 바탕으로 JPQL 실행
- 개별 JPQL에서는 연관관계를 무시하고 각 엔티티를 기준으로 쿼리를 조회하기 때문에 추가 쿼리 발생

#### 해결
- SQL 기준으로 생각해보면 JOIN을 사용하면 해결이 가능
- Spring에서는 Fetch Join을 사용해서 Join을 시켜주면 됨 (`@Query` 어노테이션으로 fetch join)

ref.
- https://incheol-jung.gitbook.io/docs/q-and-a/spring/n+1
- https://programmer93.tistory.com/83
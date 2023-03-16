## 클래스, 객체, 인스턴스 차이
**클래스** 
- 객체를 정의하고 만들어 내기 위한 설계도 혹은 틀을 말한다

**객체**
- 물리적으로 존재하거나 추상적으로 생각할 수 있는 것 중에서 자신의 속성을 가지고 있고 다른 것과 식별 가능한 것을 말한다.

**인스턴스**
- Java 프로그램 실행 시 클래스는 JVM 메모리의 클래스 영역(Class Area)에 로드되고 이 클래스를 사용하여 힙 영역(Heap Area)에 새로운 인스턴스(객체)를 생성할 수 있다. 즉, 인스턴스란 현실의 객체를 소프트웨어 내에서 구현한 실체라고 볼 수 있다.
## JVM, GC

stop-the-world : GC를 실행하기 위해 JVM이 애플리케이션의 실행을 멈추는 것

이때는 GC 처리 쓰레드 외에 모든 쓰레드가 작업을 멈춘다. GC 튜닝의 최종 목적은 stop-the-world 시간을 줄이는 것이다.

GC는 두가지 가설을 기반으로 동작한다 (Weak generaitonal hypothesis)
- 대부분의 객체는 금방 접근 불가능한 상태가 된다
- 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다

Hotspot JVM은 heap 공간을 young 영역과 old 영역으로 나눔

![스크린샷 2023-03-15 오후 8.56.26.png](/image/gc_1.png)

**Young 영역**

새로 생성된 대부분의 객체가 이 영역에 위치한다. 대부분의 객체가 금방 접근 불가능한 상태가 되기 때문에 young영역에 생성됐다가 여기서 사라진다.

young 영역에서 객체를 정리하는걸 minor GC라고 한다.

**Old 영역** 

young 영역에서 살아남은 객체들이 이 영역으로 이동한다. young 영역보다 크게 할당되고 GC도 적게 발생한다. 여기서 GC가 발생하면 Major GC 혹은 Full GC라고 한다.

![스크린샷 2023-03-13 오전 1.30.07.png](..%2F..%2F..%2FDesktop%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-03-13%20%EC%98%A4%EC%A0%84%201.30.07.png)

Old 영역에 있는 객체가 young 영역에 있는 객체를 참조하는 경우
- Old 영역에는 512바이트 짜리 카드 테이블이 존재 -> Old 영역에 있는 객체가 Young 영역의 객체를 참조할때마다 참조 정보가 카드테이블에 기록된다. Young 영역 GC 할때는 카드테이블 뒤져서 GC 대상 식별함
- 카드 테이블 관리는 write barrier 사용한다. Minor GC를 빠르게 해준다.

![스크린샷 2023-03-15 오후 8.56.39.png](..%2F..%2F..%2FDesktop%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-03-15%20%EC%98%A4%ED%9B%84%208.56.39.png)
Young 영역은 eden 영역과 두개의 survivor 영역으로 구분된다

1. 새로 생성한 객체들 eden 영역 배치
2. eden 영역에서 살아남았으면 survivor중 하나로 감
3. survivor 하나 다 차면 다음 survivor로 이동
4. 3개 다 지나면 old로 이동

### old 영역 GC

old 영역의 gc는 **mark-sweep-compact** 알고리즘 사용한다

1. old 영역의 살아있는 객체 식별
2. 힙 앞부분부터 살아있는 것만 남김
3. 앞 부분부터 객체들이 다시 쌓이게 정리함


### GC의 종류

Serial GC : GC 쓰레드가 하나임

parallel GC : GC 처리 쓰레드가 여러개임

### CMS GC 
![스크린샷 2023-03-15 오후 9.07.34.png](..%2F..%2F..%2FDesktop%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-03-15%20%EC%98%A4%ED%9B%84%209.07.34.png)

initial mark: 
- 클리스 로더에서 가장 가까운 객체 중 살아있는것만 다 체크

concurrent mark: 
- 다른 실행 쓰레드들과 병렬로 나머지 객체 참조를 체크한다

remark: 
- concurrent mark에서 새로 추가되거나 참조 끊긴것들 확인한다

concurrent sweep: 
- 여기서는 참조가 없는 Garbage들 다른 실행 쓰레드와 병렬로 처리한다


- 장점 : stop the world 매우 짧음, 동시성 성능 보장됨
- 단점 : 다른 GC보다 CPU 많이 먹음, compaction 제공 안해서, 컴펙션 실행하면 오히려 파편화된거 많아서 성능 안나올수도 있음

> 현재 default는 G1 GC, 런타임에 G1 GC가 필요한 영역을 튜닝하고 STW 시간을 줄임


## JRE, JDK
JRE
- 자바 실행 환경(Java Runtime Environment)의 약자로 자바로 만들어진 프로그램을 실행시키는데 필요한 라이브러리들과 각종 API, 그리고 자바 가상 머신 (JVM)이 포함되어 있다.

JDK
- JDK는 자바 개발키트(Java Development Kit)의 약자로 이름 그대로 개발자들이 자바로 개발하는 데 사용된다 JDK안에는 개발 시 필요한 라이브러리들과 javac, javadoc 등의 개발 도구들을 포함되어 있고 개발을 하려면 당연히 실행도 시켜줘야 하기 때문에 JRE (Java Runtime Environment)도 함께 포함되어 있다.
## Java 장단점

### 장점

플랫폼 독립성
- 하드웨어 또는 운영체제와 같은 플랫폼에 독립적으로 실행 가능한 특성

- 자바는 Java Virtual Machine(JVM)을 기반으로 동작하기 때문에 자바로 만든 프로그램은 어떤 환경에서도 완벽히 똑같이 동작한다.


객체 지향 언어
- 신뢰성 있는 소프트웨어를 손쉽게 작성 가능하다.

- 코드 재사용이 유리하다.

오픈 소스
- 이용자들에 의해 기존 문제가 해결되고 발전하며 운영되기 때문에 발전 속도가 빠르고 정보를 얻기 쉽다.

- 오픈소스 라이브러리가 풍부해 짧은 시간 내 안정적인 애플리케이션 구현이 가능하다.



자동 메모리 관리
- Garbage Collector 는 객체가 프로그램에서 더 이상 사용되지 않고 명시적 프로그래밍에 의해 역참조 되거나 제거할 필요가 없는 항목을 참조하지 않을 때마다 자동으로 제거해준다.

- 이로 인해 사용자는 메모리 관리를 신경쓰지않고 비즈니스 로직에 집중할 수 있다.



### 단점

실행 속도가 느리다
- JVM을 거쳐서 실행되기 때문에 다른 언어에 비해 실행 속도가 느리다.

- 처리 속도가 중요한 애플리케이션에서 적합하지 않다.

## 접근 제어자 종류와 특징

public 
- 모든 위치에서 접근 가능

protected
- 자식만 접근 가능

private 
- 자신 외에는 모두 접근 불가

default 
- 같은 패키지에서만 접근 가능

## Wrapper class

래퍼 클래스

뜻
- 원시 타입의 데이터를 객체로 포장해주는 클래스

박싱: 

- 기본 타입을 래퍼 클래스로 변환하는 과정

언박싱: 
- 래퍼 클래스를 기본 타입으로 변환하는 과정

오토 박싱: 
- 자바 컴파일러가 자동으로 박싱 진행

```java
list.add(1) // 예전에는 불가
list.add(Integer.valueOf(1)) // 원래 이렇게 했어야 하는데 지금은 오토 박싱 해줘서 필요없음
```
- 값이 적절한 래퍼클래스 타입 변수에 할당될때
- 래퍼 클래스 타입이 기대되는 파라미터로 기본형 타입이 전달될때

오토 언박싱: 
- 자바 컴파일러가 자동으로 언박싱 진행

**래퍼 클래스 특징**
- Immutable 하기 때문에 생성된 이후로는 상태가 변경되지 않는다
- final로 선언되서 상속 불가능하다
- 원시 타입은 Stack에 저장되지만, wrapper 클래스들은 Heap에 저장된다.

메모리의 stack 공간 : 쓰레드 마다 하나씩 할당된다.
메모리의 heap 공간 : 모든 쓰레드들이 공유한다.

원시 변수 사용하면 Stack 메모리에서 데이터 가져오므로 빠르다
래퍼 클래스 사용하면 Heap을 참조해야 함으로 조금 느리다

## 인터페이스와 추상클래스 차이
> 공통된 기능의 사용 여부가 중요하다

공통된 기능을 사용해야 하는 경우에는 인터페이스를 사용할 경우 모든 클래스에서 다 오버라이딩 해줘야함
만약 추상 메서드를 상속할 경우, 공통 메서드는 부모 추상 메서드에 선언하고, 땨로 중복 오버라이딩 할 필요없이 자식에서 가져다 쓰면 된다

공통점
- 추상 메서드를 통해 상속/구현을 통한 메소드 강제 구현 규칙을 가진다

인터페이스: 인터페이스에 정의된 메서드를 클래스의 목적에 맞게 기능 구현하는 느낌

추상 클래스: 자신의 기능을 하위 클래스로 확장 시키는 느낌

**추상 클래스 사용 이유** 

- 공통으로 가지는 메소드와 필드가 많아서 중복 통합 시켜야 할때

```java
abstract class Exam {
    int kor;
    int eng;
    int math;

    abstract void total();
    abstract void avg();
}

class NewlecExam extends Exam {
    int com;

    void total(){}
    void avg(){}
}

class YBMExam extends Exam {
    int toeic;

    void total(){}
    void avg(){}
}
```

인터페이스의 단점 : 중복 멤버 통합, 인터페이스에서는 모두 다 오버라이딩 해야 한다



## final keyword

Java에서 불변성을 확보하도록 하기 위해 final 키워드를 제공함

변수 앞에 final 키워드를 붙일때

변수 앞에 final을 붙이면 초기화 후에는 변수 값을 변경할 수 없다.

```java
class Test{
    
    // 이후에는 다시 값을 변경할 수 없다.
    private final value = "hello";
    
}
```

매개 변수 앞에 final

메소드 내에서 변경이 불가능하다. 즉, 함수 내부에서 읽는 목적으로만 사용해야 한다

```java
public void testMethod(final int value)
        {
            value = 3; // 이렇게 값을 내부에서 변경하는거 불가능하다.
        }
```

Final 클래스
   
클래스 앞에 final 붙이면 다른 클래스가 상속할 수 없다

```java
final class Parent{
    
}

class Child extends Parent{ // 컴파일 에러
    
}
```

Final 메소드
   
오버라이딩 금지, 즉 있는 그대로 사용해야 한다.

```java
class Parent {
    final void parentMethod(int k)
    {
        return k;
    }
}

class Child extends Parent{
    
    @Override  // 컴파일 에러
    void parentMethod(int k)
    {
        return k+1;
    }
}
```
## Overriding vs OverLoading
1. 오버로딩(Overloading)
- 메서드의 이름은 같고 매개변수의 갯수나 타입이 다른 함수를 정의하는 것을 의미한다.
- 리턴값만을 다르게 갖는 오버로딩은 작성 할 수 없다.

2. 오버라이딩(Overriding)
- 상위 클래스의 메서드를 하위 클래스가 재정의 하는 것이다.
- 메서드의 이름은 물론 파라메터의 갯수나 타입도 동일해야 하며, 주로 상위 클래스의 동작을 상속받은 하위 클래스에서 변경하기 위해 사용된다.

즉,
오버로딩(Overloading)은 기존에 없던 새로운 메서드를 정의하는 것이고,
오버라이딩(Overriding)은 상속 받은 메서드의 내용만 변경 하는 것이다.

## static vs non static

Static 키워드는 클래스의 인스턴스가 아니라, 해당 타입 자체에 속하는 멤버를 말한다. 정적 멤버 Static 변수는 정확하게는 heap memory 안에 할당되고, 그 내부에서도 static 영역에 할당된다

특정 값이 객체에 독립적이여야 하고, 모든 객체에서 값을 공유해야 할때 Static field 사용한다

> 인스턴스를 생성해서 접근하는건 피해야 한다. 우리는 그 field가 static인지 인스턴스 변수인지 구분하기 힘들게 만든다

### Static method
- 인스턴스를 만들지 않고도 사용 가능
- 보통 유틸리티 함수를 만들기 위해 사용한다

**사용 이유**
- Static field나 다른 static method를 제어하기 위해서 사용한다
- Helper 클래스나 유틸리티 클래스 구현에 사용

**주의할 점**

- Static method는 컴파일 시점에 이미 올라온다. 오버라이딩은 런타임의 영역 따라서 static method는 오버라이딩 불가!
- Static 메서드에서는 this나 super 키워드 사용 불가

### 조합
- 인스턴스 메서드는 다른 인스턴스 메서드나 인스턴드 변수에 접근 가능
- 인스턴스 메서드는 static 변수나 static 변수에 접근 가능
- Static 메서드는 static 변수나 메서드에 접근 가능
- Static 메서드는 인스턴스 변수나 메서드에 접근 불가능!


### Static block
- Static 변수의 초기화가 추가 로직이 필요할때 아니면 에러 핸들링 필요할때

```java
public class StaticBlockDemo {
    public static List<String> ranks = new LinkedList<>();

    static {
        ranks.add("Lieutenant");
        ranks.add("Captain");
        ranks.add("Major");
    }
    
    static {
        ranks.add("Colonel");
        ranks.add("General");
    }
}
```

- 클래스 내부에는 여러 static block 가질 수 있다. 즉, static 로딩 시점에 동작할 로직들을 넣을 수 있다

### Static class

내부 클래스 사용하는 방법
- Static class
- Inner class

Static class 사용 이유
- 한곳에서만 사용될 클래스들을 그루핑 할 수 있다
- 코드를 실제 사용될 위치 근처에 정의할 수 있어서 가독성과 유지보수성 증가
- 만약 중첩 클래스가 외부 클래스의 인스턴스 멤버에 접근이 필요하지 않다면, static 으로 정의하는게 낫다
- 이 방식을 사용하면 외부 클래스에 커플링 되지 않도록 한다
- 외부 클래스의 static 멤버의 경우 private 도 접근 가능
- Top -level 클래스의 경우, static 선언 불가

## main 메서드가 static인 이유

- JVM(Java Virtual Machine)이 접근 하기 위해서 public을 사용해야만한다.

- 프로그램이 실행되면 제일 먼저 호출되는 메서드이기 때문에 객체를 생성하지 않은 채로 바로 작업을 수행해야 하기 때문에 static이어야한다.

- 메인 메서드를 호출하는 JVM(Java Virtual Machine)에서 반환값을 요구하지 않으니 void타입을 사용한다.

## OOP 특징 (중요)

- SRP(Single Responsibility Principle): 단일 책임 원칙
- OCP(Open Closed Priciple): 개방 폐쇄 원칙
- LSP(Listov Substitution Priciple): 리스코프 치환 원칙
- ISP(Interface Segregation Principle): 인터페이스 분리 원칙
- DIP(Dependency Inversion Principle): 의존 역전 원칙

### SRP
- 한 클래스는 하나의 책임만 가져야 한다.
- 중요한 기준은 변경이다, 변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것
> 예) UI 변경, 객체의 생성과 사용을 분리

### OCP

• 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다

```java
public class MemberService {
 private MemberRepository memberRepository = new MemoryMemberRepository();
}
```

- 인터페이스를 사용시, 구체 클래스가 바뀌어도 클라이언트 코드는 변경할 필요가 없다 (폐쇄성)
- 인터페이스를 사용시, 구체 클래스 종류는 인터페이스만 지킨다면 얼마든지 교체 가능하다 (개방성)

### LSP

- 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀
수 있어야 한다
- 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것, 다형성을 지원하기 위
한 원칙, 인터페이스를 구현한 구현체는 믿고 사용하려면, 이 원칙이 필요하다.
> 예) 자동차 인터페이스의 엑셀은 앞으로 가라는 기능, 뒤로 가게 구현하면 LSP 위반, 느리
더라도 앞으로 가야함

### ISP
- 다양한 기능을 포함하고 있는 큰 인터페이스보다 기능에 맞춰서 인터페이스를 여러개로 쪼개야 한다는 원칙

### DIP
- 구체 클래스가 인터페이스에 의존하게 만듬으로써 의존성을 역전시키는 방식

## Multi thread 환경에서의 개발

### ThreadLocal

ThreadLocal은 특정 쓰레드마다 개별적으로 사용할 수 있는 공간을 제공해준다. 특정 쓰레드만 사용하고 싶은 값이 있다면 threadLocal에 넣어주면 된다. 쉽게 Thread-safety를 보장해주지만, 쓰레드 풀 환경에서는 좋지 않다.

ThreadPool에서 꺼내서 사용 후 반납 전에 clear 해주지 않으면, 이전 request의 민감 정보를 다음 request에서 그대로 사용할수도 있다.

해결방법 : ExecuterService를 사용해서 hook을 통해 threadpool 반납 전 꼭 clear를 실행하게 해줄 수 있다.

### 쓰레드 풀
![스크린샷 2023-03-15 오후 9.29.39.png](..%2F..%2F..%2FDesktop%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-03-15%20%EC%98%A4%ED%9B%84%209.29.39.png)


```java

// 고정된 크기의 쓰레드풀 생성 -> 보통 쓰레드 개수는 CPU 코어 수
ExecutorService executorService = Executors.newFixedThreadPool(int nThreads);
// 싱글 쓰레드 생성
ExecutorService executorService = Executors.newSingleThreadExecutor();

public class ExecutorServiceTest {

  public static void main(String args[]) throws InterruptedException {
    ExecutorService executor = Executors.newFixedThreadPool(4);

    executor.submit(() -> {
      String threadName = Thread.currentThread().getName();
      System.out.println("Job1 " + threadName);
    });
    executor.shutdown();

    // shutdown() 호출 전에 등록된 Task 중에 아직 완료되지 않은 Task가 있을 수 있습니다.
    // Timeout을 20초 설정하고 완료되기를 기다립니다.
    // 20초 전에 완료되면 true를 리턴하며, 20초가 지나도 완료되지 않으면 false를 리턴합니다.
    if (executor.awaitTermination(20, TimeUnit.SECONDS)) {
      System.out.println(LocalTime.now() + " All jobs are terminated");
    } else {
      System.out.println(LocalTime.now() + " some jobs are not terminated");
      
      executor.shutdownNow();
    }
  }
}
```

### 자바에서 제공하는 동시성 관리

멀티 쓰레드를 사용하는 상황에서는 동시성 관리가 중요하다. 자바에서는 동시성 관리를 위해 synchronized, volatile라는 키워드 제공한다.

**synchronized**
```java
public class Test{
    
    int cnt =0;
    
    // 이 메서드에는 한번에 하나의 쓰레드만 진입 가능
    public synchronized void countStock()
    {
        cnt++;
    }
}
```

**volatile**

멀티 쓰레드 환경에서는 여러 CPU Core가 사용된다. 이때 CPU Core들은 각각 캐시를 가지고 있다. 

![스크린샷 2023-03-15 오후 9.36.01.png](..%2F..%2F..%2FDesktop%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-03-15%20%EC%98%A4%ED%9B%84%209.36.01.png)

쓰레드들은 값을 조회할때 바로 RAM에서 가져오는 것이 아니라 자신의 L1 Cache에 저장된 값을 사용한다. 따라서 자신이 조회한 값이 최신의 값이 아닐 가능성이 있다.

따라서 쓰레드간 동기화가 중요한 데이터의 경우 volatile 키워드를 통해 동시성을 보장할 수 있다. volatile 키워드를 사용할 경우 캐시가 아니라 메인 메모리에서 바로 데이터를 가져온다.

```java
public class Test{
    
    // 해당 키워드를 붙일 경우 cnt 변수값을 무조건 메인메모리에서 가져옴
    private volatile int cnt;
    
    public void increase()
    {
        cnt++;
    }
}
```


## 컬렉션

객체의 모음, 그룹이라 할 수 있다

자바에서 모든 컬렉션 클래스와 인터페이스를 포함 하는 "Collection Framework"라는 개념이 JDK 1.2에서 정의가 되었다

Collection 인터페이스(java.util.Collection) 와 Map 인터페이스(java.util.Map) 자바 컬렉션 클래스의 주요 "루트"인터페이스이다

![collection.png](..%2F..%2F..%2FDesktop%2Fcollection.png)

### 컬렉션 사용 이유

1. 일괄된 API : Collection의 일관된 API를 사용하여 Collection 밑에 있는 모든 클래스(ArrayList, Vector, LinkedList 등) Collection에서 상속받아 통일된 메서드를 사용하게 된다.

2. 프로그래밍 노력 감소 : 객체 지향 프로그래밍의 추상화의 기본 개념이 성공적으로 구현되어있다.

3. 프로그램 속도 및 품질 향상 : 유용한 데이터 구조 및 알고리즘은 성능을 향상시킬 수 있습니다 Collection을 사용하여 최상의 구현을 생각할 필요없이 간단하게 Collection API를 사용하여 구현을 하면 된다.

### 컬렉션에 원시 타입이 사용되지 못하는 이유

- 자바 원시 타입은 참조 타입이 아니다
- 자바는 컬렉션에서 와일드 카드 제레닉을 제공한다 List<?>, ?에는 객체가 들어와야하는데 원시 타입은 객체가 아니다.

만약 컬렉션에 원시 타입을 대입한다고 해도, 자동으로 Wrapper 클래스로 박싱이 된 뒤에 컬렉션으로 들어간다.
## 어노테이션

### 어노테이션의 역할

- 컴파일러에게 코드 작성 문법 에러를 체크하도록 정보를 제공
- 소프트웨어 개발툴이 빌드나 배치시 코드를 자동으로 생성할 수 있도록 정보 제공
- 실행시(런타임시)특정 기능을 실행하도록 정보를 제공
- 불필요한 코드의 중복을 줄여준다

![annotation.png](..%2Fimage%2Fannotation.png)

**@Retention**

자바 컴파일러가 어노테이션을 다루는 방법을 기술하며, 특정 시점까지 영향을 미치는지를 결정한다.
- RetentionPolicy.SOURCE : 컴파일 전까지만 유효. (컴파일 이후에는 사라짐)
- RetentionPolicy.CLASS : 컴파일러가 클래스를 참조할 때까지 유효.
- RetentionPolicy.RUNTIME : 컴파일 이후에도 JVM에 의해 계속 참조가 가능. (리플렉션 사용)


**@Documented**

해당 어노테이션을 Javadoc에 포함시킨다.


**@Target**

어노테이션이 적용할 위치를 선택한다.

- ElementType.PACKAGE : 패키지 선언
- ElementType.TYPE : 타입 선언
- ElementType.ANNOTATION_TYPE : 어노테이션 타입 선언
- ElementType.CONSTRUCTOR : 생성자 선언
- ElementType.FIELD : 멤버 변수 선언
- ElementType.LOCAL_VARIABLE : 지역 변수 선언
- ElementType.METHOD : 메서드 선언
- ElementType.PARAMETER : 전달인자 선언
- ElementType.TYPE_PARAMETER : 전달인자 타입 선언
- ElementType.TYPE_USE : 타입 선언

### 메타 어노테이션

특정 어노테이션에 붙어서 어노테이션의 기능을 추가해주는 어노테이션, 부모 어노테이션이라 보면 된다. 위 @Component의 경우에는 @Target이나 @Document 등이 메타 어노테이션이다.

### 어노테이션 프로세서

애노테이션 프로세서는 컴파일 타임에 애노테이션을 스캔하고 처리하기 위해 javac에서 확장해서 사용하는 도구.

보통 애노테이션 프로세서는 Java코드 혹은 컴파일된 Java Bytecode를 입력으로 받아서, 파일을(대개는 .java 파일) 출력으로 생성합니다. 
메서드를 추가하기 위해서 이미 존재하는 자바 클래스파일을 조작할 필요는 없음. 이 생성된 java 파일은 다른 java 파일과는 동일하게 javac로 컴파일 됨.

## Generic , c++ 템플릿과의 차이

### C++ 템플릿
- int 같은 원시 타입을 매개변수로 넘길 수 있다.

### 자바 제네릭
- Object만 매개변수로 사용할 수 있다.
- 매개변수로 넘겨지는 타입을 특정 타입으로 제한할 수 있다.
```java
Stock<? extends StockClass>
```
- 매개변수로 넘겨진 타입으로 static field나 method를 선언할 수 없다 -> 여러 타입이 올 수 있는데 static은 모든 인스턴스가 공유하기 때문


## 직렬화와 역직렬화

**직렬화**

객체를 직렬화하여 전송 가능한 형태로 만드는 것을 의미한다. 객체들의 데이터를 연속적인 데이터로 변형하여 Stream을 통해 데이터를 읽도록 해준다. 주로 객체들을 통째로 파일로 저장하거나 전송하고 싶을 때 주로 사용된다.

**역직렬화**

직렬화된 파일 등을 역으로 직렬화하여 다시 객체의 형태로 만드는 것을 의미한다. 저장된 파일을 읽거나 전송된 스트림 데이터를 읽어 원래 객체의 형태로 복원한다.

**직렬화 가능하게 만드는 방법**

- Serializable 인터페이스를 구현한다
- 클래스에 명시적으로 implement Serializable이 없는 경우, extends한 클래스들을 보면 Serializable이 구현되있을 수 있다.
## Call by reference vs Call by value

변수가 선언될때는 스택 영역이나 힙 영역에 할당된다

스택 영역
- 함수의 호출과 함께 지역 변수나 매개변수가 할당됨, 정렬된 방식으로 할당 및 해제가 진행됨

힙 영역
- 인스턴스 변수나 객체가 할당된다. 
- 무질서하게 메모리가 할당된다. -> 따라서 가비지 컬렉터로 힙 영역 관리

```java
public void test(){
    
    int x = 3;
    float y = 10.102f;
    String s = "hello";
        }
```

메모리 내부에는 해당 내용이 스택영역에 저장된다. 즉 실제 원시 값들이 저장된다
하지만 객체인 String의 경우, 실제 데이터는 힙 영역에 저장되고, stack 영역에는 그 힙 영역에 대한 실제 주소가 저장된다. 

- heap 영역은 stack 영역과 다르게 무질서하게 메모리 공간 활용
- 객체의 메모리 할당의 경우 stack 영역에는 실제 주소값만 저장
- 배열의 경우 각 인덱스마다 참조값이 할당되고 이를 통해 접근 즉, 배열 내부에 실제값이 있는게 아니라, 그 실제 값의 참조 주소들이 들어있다

pass by value
- 복사된 데이터를 전달함, 값을 수정하여도 원본 데이터에 영향 주지 않는다

pass by reference
- 메인 이후 호출되는 함수의 콜스택에 매개변수로 실제 값을 넣는 것이 아니라, 메인 함수 내의 변수의 주솟값을 넣는다.

> Java의 전달방식은? pass by value

pass by reference가 아닌 이유

call by reference의 경우, 만약 메인 함수의 변수 7을 함수 매개변수로 전달할때, 주소 값을 전달하여 실제 값에 대한 Alias를 구성함으로써, 값을 수정하면 원본의 데이터가 수정되도록 하는 방식

즉, 내부 값을 바꾸면 외부도 같이 바뀜

자바의 경우 객체의 경우, 변수에는 주소값이 들어간다. 하지만 매개변수로 옮겨질때는 그 주소값 변수 자체가 복사가 된다. 그렇다면 그 변수를 통해서 같은 객체에 접근 가능하고, 그 객체 내부의 값을 변경할 수는 있지만, 객체 자체를 다른 객체로 바뀌끼울수는 없다. 
바꿔봤자 복사본이기 때문!

## String, StringBuffer, StringBuilder

String
- 불변의 속성 가짐

```java
String str = "hello";
str = str + "world";
```

해당 로직을 실행하면 str이라는 변수에 그대로 world가 이어지는게 아니라, 새로운 str 변수를 만들고 그 변수의 주소를 가리키도록 한다. 이전 str은 GC 대상이 된다

-> 변하지 않는 문자열 자주 조회시 좋음
-> 문자열 추가 수정 삭제 시 힙 메모리에 많은 gc 대상 객체가 생성됨, 힙메모리 부족이 될 수 있음

이를 해결하기 위해 가변성 가지는 StringBuffer, StringBuilder 도입함
api 사용해서 동일 객체 내의 문자열 변경 가능함
-> 문자열의 빈번한 추가 수정 삭제 발생 시, StringBuffer와 StringBUilder가 좋음

### StringBuilder vs Stringbuffer

둘의 차이점 : 동기화 유무

- Stringbuffer는 동기화 키워드를 통해 멀티 쓰레드 환경에서 안전하다
- String도 불변성이 유지되서 멀티 쓰레드 환경에서 안전함
- StringBuilder는 동기화 고려 안해서 단일 쓰레드에서는 좋다.

사용처
- String : 문자열 연산 적고 멀티쓰레드 환경
- Stringbuffer: 문자열 연산 많고 머티 쓰레드
- StringBuilder : 문자열 연산 많고 단일 쓰레드일때

## checked exception, unchecked  exception (ok)
![스크린샷 2023-03-15 오후 8.41.06.png](..%2F..%2F..%2FDesktop%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-03-15%20%EC%98%A4%ED%9B%84%208.41.06.png)

**예외를 처리하는 방법**
- try-catch를 통해서 처리 후 정상 로직으로 변환
- throws를 통해서 외부로 던지기

**예외를 끝까지 던지면 어떻게 될까**

**일반 자바 프로그램**
- 예외 로그를 던지면서 프로그램이 종료된다

**웹 어플리케이션**
- 여러 사용자가 사용하기에 예외가 던져졌다고 서비스가 죽으면 안된다. WAS가 지정한 예외 페이지가 반환되거나 사용자 지정 예외 페이지가 반환된다.

### 체크 예외

체크 예외는 Exception 클래스와 그 하위 클래스들이다.

- 체크 예외는 무조건 Throw 하거나 try-catch로 예외를 잡아야 한다. 아니면 컴파일 에러 발생

**장점:**

개발자가 실수로 예외를 누락하지 않도록 컴파일러를 통해 문제를 잡아주는 훌륭한 안전 장치이다. 

**단점:** 

개발자가 모든 체크 예외를 반드시 잡거나 던지도록 처리해야 하기 때문에, 너무 번거로운 일이 된다. 크게 신경쓰고 싶지 않은 예외까지 모두 챙겨야 한다. 

> 보통 언체크 예외를 많이 사용하고, 비즈니스적으로 의미가 있을 경우에만 체크 예외를 주로 사용한다.

```java
public void minusStock(){
   
    if(cnt < 1){
        throw new MinusCountException();
        }
    
    cnt--;
    
}
```
위의 상황의 경우, 시스템적으로 문제가 있지도 않고 사용자가 예상하지 못한 상황도 아니다. 이때는 사용자에게 재고를 줄일 수 없다는 메세지만 던저주면 되는 것이다. 이럴때 체크 예외를 사용한다.

### 언체크 예외

언체크 예외는 명시적으로 예외를 던지거나 처리하지 않아도 된다.

**장점:** 

신경쓰고 싶지 않은 언체크 예외를 무시할 수 있다. 

**단점:** 

언체크 예외는 개발자가 실수로 예외를 누락할 수 있다.

## ==와 equals 차이

- ==는 연산자로써 비교 대상의 주소값을 비교한다

- equals는 메서드로써 비교 대상의 실제 값을 비교한다.

> equals도 내부적으로는 == 비교를 사용한다
> String에서는 == 비교 후, 주소값이 다르다면 실제 문자열 값으로도 비교를 하는 로직이 포함되어 있다

```java
 public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```
## 리플렉션
구체적인 클래스 타입을 알지 못해도 그 클래스의 메소드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API

런타임에 지금 실행되고 있는 클래스를 가져와서 실행해야하는 경우, 동적으로 객체를 생성하고 메서드를 호출하는 방법

자바의 리플렉션은 클래스, 인터페이스, 메소드들을 찾을 수 있고, 객체를 생성하거나 변수를 변경하거나 메소드를 호출할 수 있다.

우리가 스프링 고급편에서 학습했던 JDK 동적 프록시가 리플렉션을 사용하는 기술이다.
### 리플렉션 사용 예시

리플렉션을 사용하면 싱글톤을 깰 수 있다.
```java
public static void main(String[] args) throws NoSuchMethodException, InstantiationException, IllegalAccessException, InvocationTargetException {
    /* Reflection API */
    
    // 1. Singleton의 Class에서 생성자를 가져온다
    Constructor<Singleton> consructor = Singleton.class.getDeclaredConstructor();

    // 2. 생성자가 private 이기 때문에 외부에서 access 할 수 있도록 true 설정
    consructor.setAccessible(true);

    // 3. 가져온 생성자를 이용해 인스턴스화 한다
    Singleton singleton1 = consructor.newInstance();
    Singleton singleton2 = consructor.newInstance();

    System.out.println("singleton1 == singleton2 : " + (singleton1 == singleton2));
    System.out.println(singleton1);
    System.out.println(singleton2);
}
```

따라서 우리가 싱글톤을 직접 구현하다고 해도 리플렉션을 사용한다면 쉽게 깨질 수 있다. 따라서 싱글톤으로 유지해야 하는 경우 Enum을 사용하는게 좋은 방법이다.

```java
public static void main(String[] args) throws NoSuchMethodException, InstantiationException, IllegalAccessException, InvocationTargetException {

    /* Reflection API */

    // 1. Singleton Enum의 생성자는 숨겨져 있기 때문에 getDeclaredConstructors로 배열로 가져온다.
    Constructor<?>[] consructors = Singleton.class.getDeclaredConstructors();

    // 2. 생성자 배열을 순회하여 인스턴스를 생성한다
    for(Constructor<?> constructor : consructors){
        constructor.setAccessible(true); // 생성자가 private 이기 때문에 외부에서 access 할 수 있도록 true 설정
        Singleton singleton = (Singleton) constructor.newInstance("INSTANCE");
    }
}
```

Enum의 경우에도 리플렉션을 통해 생성자를 호출하도록 시도해볼 수 있다. 하지만 Enum은 자체적으로 리플렉션을 통한 생성자 호출이 불가능하도록 설계되어있다.

![스크린샷 2023-03-15 오후 8.34.54.png](..%2F..%2F..%2FDesktop%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-03-15%20%EC%98%A4%ED%9B%84%208.34.54.png)
## 스트림

### Stream API의 특징
- 원본의 데이터를 변경하지 않는다.
- 일회용이다.
- 내부 반복으로 작업을 처리한다.



### 원본의 데이터를 변경하지 않는다.
Stream API는 원본의 데이터를 조회하여 원본의 데이터가 아닌 별도의 요소들로 Stream을 생성한다. 그렇기 때문에 원본의 데이터로부터 읽기만 할 뿐이며, 정렬이나 필터링 등의 작업은 별도의 Stream 요소들에서 처리가 된다.
```java
List<String> sortedList = nameStream.sorted()
.collect(Collections.toList());
```


### Stream은 일회용이다.

Stream API는 일회용이기 때문에 한번 사용이 끝나면 재사용이 불가능하다. Stream이 또 필요한 경우에는 Stream을 다시 생성해주어야 한다. 만약 닫힌 Stream을 다시 사용한다면 IllegalStateException이 발생하게 된다.
```java
userStream.sorted().forEach(System.out::print);

// 스트림이 이미 사용되어 닫혔으므로 에러 발생
int count = userStream.count();

// IllegalStateException 발생
java.lang.IllegalStateException: stream has already been operated upon or closed
at java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:229)
at java.util.stream.ReferencePipeline.noneMatch(ReferencePipeline.java:459)

```


### 내부 반복으로 작업을 처리한다.
   Stream을 이용하면 코드가 간결해지는 이유 중 하나는 '내부 반복' 때문이다. 기존에는 반복문을 사용하기 위해서 for이나 while 등과 같은 문법을 사용해야 했지만, stream에서는 그러한 반복 문법을 메소드 내부에 숨기고 있기 때문에, 보다 간결한 코드의 작성이 가능하다.

```java
// 반복문이 forEach라는 함수 내부에 숨겨져 있다.
nameStream.forEach(System.out::println);
```
## 람다

람다식(Lambda Expression)이란 함수를 하나의 식(expression)으로 표현한 것이다. 함수를 람다식으로 표현하면 메소드의 이름이 필요 없기 때문에, 람다식은 익명 함수(Anonymous Function)의 한 종류라고 볼 수 있다.

**람다식(Lambda Expression) 의 장점**
- 코드를 간결하게 만들 수 있다.
- 식에 개발자의 의도가 명확히 드러나 가독성이 높아진다.
- 함수를 만드는 과정없이 한번에 처리할 수 있어 생산성이 높아진다.
- 병렬프로그래밍이 용이하다.


**람다식(Lambda Expression) 의 단점**
- 람다를 사용하면서 만든 무명함수는 재사용이 불가능하다.
- 디버깅이 어렵다.
- 람다를 남발하면 비슷한 함수가 중복 생성되어 코드가 지저분해질 수 있다.
- 재귀로 만들경우에 부적합하다.

### 함수형 인터페이스(Functional Interface)
이제 우리는 람다식으로 순수 함수를 선언할 수 있게 되었다. 하지만 Java는 기본적으로 객체지향 언어이기 때문에 순수 함수와 일반 함수를 다르게 취급하고 있으며, Java에서는 이를 구분하기 위해 함수형 인터페이스가 등장하게 되었다.

함수형 인터페이스란 함수를 1급 객체처럼 다룰 수 있게 해주는 어노테이션으로, 인터페이스에 선언하여 단 하나의 추상 메소드만을 갖도록 제한하는 역할을 한다.
```java
public class Lambda {

    public static void main(String[] args) {
    
        // 기존의 익명함수
        System.out.println(new MyLambdaFunction() {
            public int max(int a, int b) {
                return a > b ? a : b;
            }
        }.max(3, 5));

    }

}
```
함수형 인터페이스를 구현하기 위해서는 인터페이스를 개발하여 그 내부에는 1개 뿐인 abstract 함수를 선언하고, 위에는 @FunctionalInterface 어노테이션을 붙여주면 된다. 위의 코드를 람다식으로 변경하면 다음과 같다.
```java
@FunctionalInterface
interface MyLambdaFunction {
int max(int a, int b);
}

public class Lambda {

    public static void main(String[] args) {

        // 람다식을 이용한 익명함수
        MyLambdaFunction lambdaFunction = (int a, int b) -> a > b ? a : b;
        System.out.println(lambdaFunction.max(3, 5));
    }

}
```
### Java에서 제공하는 함수형 인터페이스
Java에는 자주 사용될 것 같은 함수형 인터페이스가 이미 정의되어 있으며, 총 4가지 함수형 인터페이스를 지원하고 있다.

- Supplier<T>
- Consumer<T>
- Function<T, R>
- Predicate<T>



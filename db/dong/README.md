# DB

### [인덱스](https://github.com/ruthetum/study/blob/main/db/real-mysql/ch08-index.md)란?

<details>
<summary>답변</summary>
<div markdown="1">

일종의 책갈피, 책 끝에 있는 '찾아보기'(또는 색인)으로 이해, 데이터를 빠르게 찾아가기 위한 도구(수단)

SortedList 형태로 생각하면 되고, 저장되는 컬럼의 값을 정렬된 상태로 유지한다는 특징이 있어서 당연히 읽기 성능이 좋고, 쓰기 성능은 좋지 않음
- 일반적인 서비스에는 쓰기/읽기 비율이 1:9, 2:8이다보니 읽기 효율이 좋은 것이 성능에 도움됨

데이터 저장 방식은 다양하게 분류할 수 있지만 대표적으로는 B-Tree 인덱스와 Hash 인덱스로 구분할 수 있음
- B-Tree 알고리즘: 컬럼의 값을 변형하지 않고, 원래의 값을 이용해 인덱싱하는 알고리즘
- Hash 인덱스 알고리즘: 컬럼의 값으로 해시값을 계산해서 인덱싱하는 알로기즘으로 빠른 검색을 지원, 주로 메모리 기반의 DB에서 많이 사용

왜 index 를 생성하는데 b-tree 를 사용하는가?
- SELECT 질의의 조건에는 부등호(<>) 연산도 포함
- hash table 을 사용하게 된다면 등호(=) 연산이 아닌 부등호 연산의 경우에 문제가 발생
- 동등 연산(=)에 특화된 hashtable은 데이터베이스의 자료구조로 적합하지 않음

</div>
</details>

<br/>

### B-Tree

<details>
<summary>답변</summary>
<div markdown="1">

Balanced Tree

일반적으로 생각하는 tree처럼 부모 노드 밑에 자식 노드가 붙어있는 형태로

최상위 루트 노드 밑에 브랜치 노드가 존재하고, 트리 구조의 가장 하위에 있는 노드를 리프 노드라고 명명

데이터베이스에서 인덱스와 실제 데이터가 저장된 데이터는 따로 관리되고, 리프 노드는 실제 데이터 레코드를 찾아가기 위한 주소값을 저장

인덱스 추가
- B-Tree에 저장될 키 값을 이용해 B-Tree상의 적절한 위치를 검색하고, 이를 통해 B-Tree의 리프 노드에 저장
- 리프 노드가 꽉 차서 더는 저장할 수 없을 때는 리프 노드가 분리(split)되어야 하는데, 이는 상위 브랜치 노드까지 같이 처리되어야 함
- 따라서 B-Tree는 쓰기 작업 시 비용이 더 많이 발생
    - 대략적으로 테이블에 레코드를 추가하는 작업 비용을 1이라고 가정하면, 인덱스에 키를 추가하는 작업 비용은 1.5 정로 예측

인덱스 삭제
- B-Tree에서 키 값이 삭제할 때는 해당 키 값이 저장된 리프 노드를 찾아서 삭제함

인덱스 변경
- 삭제하고, 추가하는 작업으로 처리

B-Tree의 깊이
- 인덱스의 깊이는 중요하지만 직접 제정할 수 있는 방법은 없음
- 당연히 깊이가 얕을수록 좋고, 인덱스 키 값의 크기는 가능하면 작게 만드는 것이 좋음
- 아무리 대용량 데이터베이스라도 깊이는 5단계 이상까지 깊어지는 경우는 흔치 않음

</div>
</details>

<br/>

### 정규화
<details>
<summary>답변</summary>
<div markdown="1">

데이터 이상 현상을 방지하기 위해 테이블을 나누는 작업
- 삽입이상: 새 데이터를 삽입하기 위해 불필요한 데이터도 함께 삽입해야 함
- 삭제이상: 기존 데이터를 삭제하기 위해 꼭 필요한 데이터까지 삭제해야 함
- 수정이상: 기존 데이터를 수정하려면 다른 row들도 수정해야 함

정규화의 장단점
- 이상현상이 줄어든다.
- db구조 확장시 구조 변경이 용이해진다.
- join연산이 많아진다. → 속도저하

1NF
- 모든 속성의 도메인이 원자 값으로만 구성되어 있는 형태

2NF
- 1NF에서 부분함수종속 제거

3NF
- 2NF에서 이행적 함수종속 제거

BCNF
- 3NF에서 후보키가 아닌 것들 제거

4NF
- BCNF에서 다중치 종속 존재 시 함수 종속

5NF
- 4NF에서 모든 조인 종속이 릴레이션의 후보키를 통해서만 성립

</div>
</details>

<br/>

### 트랜잭션
    - 트랜잭션이란?
    - 트랜잭션 특징
    - 트랜잭션 격리수준

<details>
<summary>답변</summary>
<div markdown="1">

트랜잭션
- 쪼개질 수 없는 하나의 논리적인 작업
- 작업의 완전성을 보장해주기 위한, 데이터의 정합성을 보장하기 위한 기능

트랜잭션 특징 - ACID
- A : 원자성(Atomicity). 출금은 됐는데 입금이 안되는 상황은 있을 수 없음. 둘 다 되거나, 둘 다 안되거나.
- C : 일관성(Consistency). 마이너스 통장을 허락하지 않는다. 제약은 지켜야 함.
- I : 독립성(Isolation). 한 트랜잭션에 다른 트랜잭션이 끼어들면 안됨.
- D : 지속성(Durability). 트랜잭션 성공시 결과는 영구히 반영되어야 함.

격리 수준
| Isolation level  | DIRTY READ | NON-REPEATABLE READ | PHANTOM READ |
|:----------------:|------|-----------------|--------------|
| READ UNCOMMITTED | **발생**   | **발생**              | **발생**           |
|  READ COMMITTED  |      | **발생**              | **발생**           |
| REPEATABLE READ  |      |                 | 발생(InnoDB는 없음) |
|   SERIALIZABLE   |      |                 |              | 

- READ UNCOMMITTED
    - 변경 내용이 커밋과 롤백 여부에 상관없이 다른 트랜잭션에 보여진다
    - 데이터 정합성에 문제가 많기 때문에 보통 사용되지 않는다

- READ COMMITTED
    - 커밋이 된 데이터만 다른 트랜잭션에서 조회할 수 있다
    - 오라클에서 기본으로 사용되는 격리 수준이며, 온라인 서비스에서 가장 많이 사용된다

- REPEATABLE READ
    - 동일 트랜잭션 내에서는 동일한 결과를 보장한다
    - MySQL은 최소 REPEATABLE READ 격리 수준 이상을 사용

- SERIALIZABLE
    - 보통 SELECT는 아무런 레코드 잠금도 설정하지 않고 실행되지만 SERIALIZABLE 수준에서는 읽기 작업도 공유 잠금을 획득해야 하고, 다른 트랜잭션이 레코드를 변경하지 못한다

부정합 문제
- Dirty read
    - 트랜잭션에서 처리한 작업이 완료되지 않았음에도 불구하고 다른 트랜잭션에서 볼 수 있게 되는 현상
    - 데이터가 나타났다가 사라졌다하는 현상을 초래

- Non-repeatable read
    - 하나의 트랜잭션 내에서 동일한 SELECT 쿼리를 실행했을 때 항상 같은 결과를 보장해야 한다는 REPEATABLE READ 정합성에 어긋나는 현상

- Phantom read
    - SELECT ... FOR UPDATE 쿼리와 같은 쓰기 잠금을 거는 경우 다른 트랜잭션에서 수행한 변경 작업에 의해 레코드가 보였다가 안 보였다가 하는 현상


- 더 자세한 내용은 https://github.com/ruthetum/study/blob/main/db/real-mysql/ch05-transaction-lock.md#mysql%EC%9D%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80 참고

</div>
</details>

<br/>

### 교착상태

<details>
<summary>답변</summary>
<div markdown="1">

복수의 트랜잭션을 사용하다보면 교착상태가 일어날 수 있음

두 개 이상의 트랜잭션이 특정 자원(테이블 또는 행)의 잠금(Lock)을 획득한 채 다른 트랜잭션이 소유하고 있는 잠금이 걸린 경우 아무리 기다려도 상황이 바뀌지 않는 상태

</div>
</details>

<br/>

### join

<details>
<summary>답변</summary>
<div markdown="1">

테이블 간의 결합

한 데이터베이스 내의 여러 테이블의 레코드를 조합하여 하나의 데이터로 만듦

</div>
</details>

<br/>

### SQL Injection
<details>
<summary>답변</summary>
<div markdown="1">

클라이언트의 입력값에 악의적으로 쿼리 관련 값을 조작하여 비정상적인 동작을 유발하는 공격

- 클라이언트 입력 값에 대한 유효성 검사
- 특수문자 유효화
- prepared statement 사용하는 경우 입력값을 다시 문자열로 치환

유사한 개념은 XSS

</div>
</details>

<br/>

### Statement, PreparedStatement
<details>
<summary>답변</summary>
<div markdown="1">

java에 한정된 개념

PreparedStatement : 프리컴파일 된 SQL 문을 나타내는 객체

속도(쿼리를 수행하기 전에 이미 쿼리가 컴파일), 보안(SQL Injection 보완) 때문에 PreparedStatement를 사용하는 것 권장

https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database#statement-vs-preparedstatement

</div>
</details>

<br/>

### RDBMS, NoSQL
<details>
<summary>답변</summary>
<div markdown="1">

![image](https://user-images.githubusercontent.com/59307414/219953113-4cd6a691-a95e-417b-a8e1-a48842354007.png)

nosql 종류
- k-v : redis(elasticache), dynamodb
- document: mongodb
- column-family: HBase, cassandra
- graph: neo4j

</div>
</details>

<br/>

### ORM

<details>
<summary>답변</summary>
<div markdown="1">

object-relational mapper

DB를 OOP처럼 다루는 것.

entitymanager한테 쿼리를 맡기고, 앱 내에서 entitymanager를 움직이는 함수를 쓰는 식으로 DB에 접근

orm vs odm

https://medium.com/@julianam.tyler/what-is-the-difference-between-odm-and-orm-267bbb7778b0

object-document mapper

NoSQL에서 document batabase (mongo db)를 지원하기 위해 데이터를 변환하는 프로그래밍 기법

</div>
</details>

<br/>

### JDBC

<details>
<summary>답변</summary>
<div markdown="1">


Java Database Connectivity

DB에 접근할 수 있도록 Java에서 제공하는 API

</div>
</details>

<br/>

### 단일키 vs 복합키 vs index
<details>
<summary>답변</summary>
<div markdown="1">

단일키 : 컬럼 1개를 key로 사용

복합키 : 컬럼 2개 이상을 조합하여 key로 사용

</div>
</details>

<br/>

### join 연산 속도
<details>
<summary>답변</summary>
<div markdown="1">

???

- 서브쿼리보다는 join 쓰는 것을 권장
- join에 거는 컬럼은 인덱스를 활용 (당연히 인덱스 스캔이 효율적이니)


</div>
</details>

<br/>

### select 조회 시 컬럼이 많은 데이터가 효율적일까, 로우가 많은 데이터가 효율적일까?
<details>
<summary>답변</summary>
<div markdown="1">

그냥 디스크를 적게 읽는 게 효율적이다

</div>
</details>

<br/>

### 실행계획, 옵티마이저
<details>
<summary>답변</summary>
<div markdown="1">

실행 계획 : SQL문이 어떻게 실행될지에 대한 계획

- `explain`

옵티마이저 : SQL문을 실행하기 전에 비용 기반으로 다양한 최적의 실행계획을 수립하는 도구


</div>
</details>

<br/>

### 복제

<details>
<summary>답변</summary>
<div markdown="1">

database replication 

말 그대로 데이터베이스의 복제본을 운용하는 것

마스터-슬레이브 형태로 운용하면서 슬레이브(레플리카)는 마스터 내용을 복제
- 마스터가 수신한 쓰기/수정/삭제 요청을 레플리카에 전송

백업으로 활용할 수 있는 장점이 있고, reader-writer를 각각 활용해서 성능 개선 효과 있음

다만 replica lag가 존재

</div>
</details>

<br/>

### 파티셔닝/샤딩
<details>
<summary>답변</summary>
<div markdown="1">

![image](https://user-images.githubusercontent.com/59307414/220341581-09e9f8fc-2c58-4c62-8420-bd8250a556c8.png)

partion이라는 테이블보다 작은 단위로 나누는 작업

테이블을 물리적으로 분할 -> 읽어야 할 레코드 수가 줄어듬 -> 데이터 조회, 조작 관련 성능 개선

partion 단위로 백업 가능 

다만 테이블보다 작은 단위로 나누기 때문에 테이블 간 join이 상대적으로 더 발생할 수 있음

일반적으로 파티셔닝은 수직 / 수평으로 두 가지로 나누는데, 수평적인 파티셔닝이 샤딩

</div>
</details>

<br/>

### ERD

<details>
<summary>답변</summary>
<div markdown="1">

entity relationship diagram

엔티티간의 연관성을 표현하는 다이어그램

</div>
</details>
# DB

### [인덱스](https://github.com/suyeoniii/study/blob/main/CS/database/index.md)

<details>
<summary>답변</summary>
<div markdown="1">

- 인덱스는 책 뒤에있는 색인과 같이 정렬된 단어 중 원하는 단어를 찾고, 해당 페이지로 바로 이동하는 것과 같다.
- 데이터 조회의 성능을 향상시킬 수 있으며, 데이터를 저장, 수정, 삭제할 때는 적절한 위치에 넣는 것이 필요하므로 인덱스가 없을 때에 비해 성능이 떨어지게 된다. 하지만 대부분의 서비스는 조회를 하는 경우가 더 많으니 인덱스를 사용하는 것이 더 효율적일 때가 대부분이다.

Q. 인덱스를 사용하면 조회 성능을 향상시킬 수 있는데, 그럼 모든 컬럼에 인덱스를 걸면 좋은걸까?
A. 조회 성능은 더 좋아질 수 있지만, 데이터를 추가, 수정, 삭제할 때 그만큼 많은 인덱스 트리를 수정해야하므로 성능 저하가 일어날 수 있고 인덱스를 저장하는 공간 또한 추가로 필요하므로 적절한 컬럼에만 인덱스를 설정하는 것이 좋다.

Q. 이름 컬럼을 인덱스로 설정했을때, 홍길동이란 데이터를 찾고싶다.
홍 또는 홍길로 검색을 했을 때 인덱스를 이용해서 데이터를 찾을 수 있을까?
길동을 검색했을 때도 인덱스를 이용해서 데이터를 찾을 수 있을까?
A. ..

Q. x, y 컬럼 순서로 결합인덱스를 생성하고, y컬럼만 WHERE 조건으로 설정했을 때 인덱스를 활용할 수 있을까?
A. y컬럼은 x컬럼에 종속되므로 y컬럼만으로 인덱스를 활용할 수는 없다.
x컬럼만 사용하는 것은 가능하다. x, y순으로 정렬되어 있기때문이다.

</div>
</details>

<br/>

### B-Tree

<details>
<summary>답변</summary>
<div markdown="1">

인덱스 자료구조로 가장 일반적으로 사용됨
루트, 브랜치, 리프노드로 이루어져있는 균형잡힌트리이다.
시간복잡도는 O(log n)

</div>
</details>

<br/>

### [정규화](https://github.com/suyeoniii/study/blob/main/CS/database/normalization.md)

<details>
<summary>답변</summary>
<div markdown="1">

제1 정규형
각 데이터 값은 쪼갤 수 없는 원자값이어야한다. (여러값이 하나에 들어가면 안됨)

제2 정규형
완전함수 종속성을 만족해야함
기본키에 부분적으로 종속적인 값이 있으면 안됨

제3 정규형
이행적 함수 종속성 제거
한 테이블에서 A->B, B->C인 경우 분리되어야함

BCNF 정규형
모든 결정자가 후보키 집합에 속해야함

제4 정규형
다치종속이 없어야함.
다치종속 = 컬럼이 3개 이상이면서 A->B일 때 하나의 A값에 여러 B가 존재하는 곳

제5 정규형
조인 종속이 제거된 것

</div>
</details>

<br/>

### [트랜잭션](https://github.com/suyeoniii/study/blob/main/CS/database/transaction.md)

<details>
<summary>답변</summary>
<div markdown="1">

데이터베이스의 상태를 변경하기 위한 작업의 단위

A: 원자성. 작업이 모두 반영되거나 모두 안되거나
C: 일관성. 실행이 완료되면 일관성이 유지되어야함
I: 독립성. 둘 이상의 트랜잭션이 동시에 실행될 경우 서로의 연산에 끼어들 수 없다.
D: 영속성. 완료된 결과는 영구적으로 반영되어야함

격리수준

- READ UNCOMMITED: 커밋되지 않은 변경사항도 다른 트랜잭션이 볼 수 있음. dirty read 발생가능
- READ COMMITED: 커밋된 변경사항만 다른 트랜잭션이 볼 수 있음. Phantom Read, NON-REPEATABLE READ 발생가능
- REPEATABLE READ: 자신의 트랜잭션변호보다 낮은 트랜잭션에서 커밋된 것만 볼 수 있음
  Update 부정합 발생가능
- SERIALIZABLE: 한 트랜잭션이 수행되는 동안 다른 트랜잭션은 값을 변경할 수 없음

</div>
</details>

<br/>

### [교착상태](https://github.com/suyeoniii/study/blob/main/CS/database/deadlock.md)

<details>
<summary>답변</summary>
<div markdown="1">

트랜잭션이 잠금이 되어있는 자원을 무한히 기다리게 되는 현상

예방 방법

- 테이블 접근 순서를 유지
- 트랜잭션을 짧게 가져가기
- SELECT FOR UPDATE 지양

</div>
</details>

<br/>

### [join](https://github.com/suyeoniii/study/blob/main/CS/database/join.md)

<details>
<summary>답변</summary>
<div markdown="1">

조인 방법

- NL Join - 이중포문과 유사
- Sort Merge Join - 정렬후 비교
- Hash Join - 해시함수 사용

Q. join을 코드로 구현한다면?
A. for문 2개를 두고, 한 테이블에서 일치하는 값을 찾았을 때, 안쪽 포문에서 다음 테이블에서의 일치하는 값을 찾으면 됨. 인덱스가 있다면 인덱스를 이용할 수 있음

Q. 이중포문으로 join을 구현한다 했을 때 크기가 큰 테이블과 작은 테이블 중 어떤 테이블을 앞에 두어야할까?
A. 작은 테이블을 앞에 두어야함

</div>
</details>

<br/>

### [SQL Injection](https://github.com/suyeoniii/study/blob/main/CS/database/SQLInjection.md)

<details>
<summary>답변</summary>
<div markdown="1">

SQL injection은 입력값에 SQL구문을 넣어서 공격하는 기법

예방방법

- prepared statement 사용
- 입력값 검증
- error message 노출 X

</div>
</details>

<br/>

### Statement, PreparedStatement

<details>
<summary>답변</summary>
<div markdown="1">

prepared statement는 쿼리를 먼저 파싱, 컴파일하고 바인딩변수를 집어넣어 바인딩 변수를 문자열로 취급하기때문에 SQL injection을 피할 수 있으며 쿼리를 먼저 처리하기때문에 속도 향상에도 도움이 된다.

</div>
</details>

<br/>

### [RDBMS, NoSQL](https://github.com/suyeoniii/study/blob/main/CS/database/RDBMS%2CNosql.md)

<details>
<summary>답변</summary>
<div markdown="1">

RDBMS의 경우 데이터구조가 정해져있으므로 구조가 잘 변하지 않는 경우 유리함
Nosql의 경우 데이터구조가 정해져있지 않으므로 형태를 사전에 알 수 없는 데이터 저장시 유리함. 유연함

</div>
</details>

<br/>

### [ORM](https://github.com/suyeoniii/study/blob/main/CS/database/orm.md)

<details>
<summary>답변</summary>
<div markdown="1">

객체 - 테이블을 자동으로 매핑해줌
패러다임 불일치 해결

</div>
</details>

<br/>

### [JDBC](https://github.com/suyeoniii/study/blob/main/CS/database/JDBC.md)

<details>
<summary>답변</summary>
<div markdown="1">

Java에서 데이터베이스 작업을 위한 표준 인터페이스

</div>
</details>

<br/>

### [단일키 vs 복합키 vs index](https://github.com/suyeoniii/study/blob/main/CS/database/key.md)

<details>
<summary>답변</summary>
<div markdown="1">

단일키 - 한 컬럼을 PK로 설정
복합키 - 여러 컬럼을 PK로 설정

복합키보다는 단일키 사용이 추천됨

</div>
</details>

<br/>

### join 연산 속도

<details>
<summary>답변</summary>
<div markdown="1">

일치하는 값이 더 적은 테이블을 앞에두면 속도가 더 빠르다?
인덱스를 타도록 하면 더 빠르다?

</div>
</details>

<br/>

### [select 조회 시 컬럼이 많은 데이터가 효율적일까, 로우가 많은 데이터가 효율적일까?](https://github.com/suyeoniii/study/blob/main/CS/database/etc.md)

<details>
<summary>답변</summary>
<div markdown="1">

컬럼이 많은 것보다 로우가 많은게 낫다
컬럼이 너무 많은 경우 인덱스를 효과적으로 사용하기 어려우므로..?

</div>
</details>

<br/>

### [실행계획, 옵티마이저](https://github.com/suyeoniii/study/blob/main/CS/database/optimizer.md)

<details>
<summary>답변</summary>
<div markdown="1">

옵티마이저 = 실행계획은 산출하고 선택

</div>
</details>

<br/>

### [복제](https://github.com/suyeoniii/study/blob/main/CS/database/etc.md)

<details>
<summary>답변</summary>
<div markdown="1">

master, slave DB를 두어 master DB에서 삽입, 수정, 삭제를 담당하고 slave DB에서 조회를 담당한다.
master DB는 변경사항 발생시 작업후 slave DB에 복사본을 전달한다.

</div>
</details>

<br/>

### [파티셔닝/샤딩](https://github.com/suyeoniii/study/blob/main/CS/database/partition.md)

<details>
<summary>답변</summary>
<div markdown="1">

`파티셔닝`
한 테이블을 내부적으로 여러 테이블로 나누어 관리하는 기법

</div>
</details>

<br/>

### [ERD](https://github.com/suyeoniii/study/blob/main/CS/database/erd.md)

<details>
<summary>답변</summary>
<div markdown="1">

여러 특성(속성)으로 이루어진 entity와 entity간 관계를 다이어그램으로 표현한 것

</div>
</details>

# Data Structure

~~- Array~~

~~- LinkedList~~

~~- Array vs Linked List~~

## Array / ArrayList / LinkedList / Vector
| | Array | ArrayList | LinkedList | Vector |
|:---:|:---:|:---:|:---:|:---:|
| 크기 | 고정 | 동적 | 동적 | 동적 |
| 접근 | 인덱스 접근 | 인덱스 접근 | 순차 접근 | 인덱스 접근 |
| 자료형 | Primitive type과 Object 모두 사용 가능 | Object(wrapper class)만 사용 가능 | Object(wrapper class)만 사용 가능 | Object(wrapper class)만 사용 가능 |
| 동기화<br>(thread-safe) | synchronized을 통해 동기화 (기본적으로 동기화 제공하지 않음) | synchronized & synchronizedList을 통해 동기화<br>(기본적으로 동기화 제공하지 않음) | synchronized & synchronizedList을 통해 동기화<br>(기본적으로 동기화 제공하지 않음) | 자동 동기화 |

> ### Primitive(원시) type vs Object(객체) type
> #### Primitive type
> - Java에서 제공하는 기본적인 데이터형
> - ex) int, float, boolean, char...
>
> #### Object type
> - 객체 변수
> - ex) Integer, Float, Boolean, Char...
>
> #### 특징
> - java에서 제공하는 자료구조(e.g. ArrayList, Set...)에는 데이터를 넣을 때 Object로만 넣을 수 있음
> - 그럼에도 primitive type을 지원하는 이유는 메모리 이점 및 비트연산이 가능하기 때문


**Array vs ArrayList**

- 고정 vs 동적 크기
- primitive type(int, byte, char 등)과 object 모두를 담을 수 있지만, arrayList는 object element(wrapper class)
- 배열은 제네릭 사용 X, ArrayList는 사용 가능

**ArrayList vs LinkedList**

- 데이터 검색 시
    - ArrayList : index를 통한 접근 → o(1)
    - LinkedList : 순차 탐색 → o(n)
- 데이터 추가, 삭제 시
    - ArrayList : 최악의 경우 → o(n)
    - LinkedList : 마지막 노드만 확인 → o(1)

> 요약 : 데이터 검색 시에는 arraylist가, 추가/삭제 시에는 linkedlist가 유리

**ArrayList vs Vector**

- 기본적인 내부 구조는 동일
- 차이는 동기화의 여부
    - ArrayList는 자동 동기화를 지원하지 않음
    - Vector는 자동으로 동기화 (동기화된 메소드로 구성)
- 동기화된 메소드로 구성(Vector)되는 경우 하나의 스레드가 완료된 후 다른 스레드가 실행될 수 있기 때문에 안전하게 추가, 삭제를 수행할 수 있지만 속도가 느림.
- 속도를 고려하는 경우 ArrayList, 안전함이 우선인 경우 Vector(동기화를 하기 때문에 멀티스레드 환경에서도 안전하게 수행 가능)

~~- HashTable~~

~~- 고려해야 할 점~~

~~- 해시값 충돌이 안 나게 하려면~~

## Hashtable vs HashMap
> vector(Hashtable)와 ArrayList(HashMap)의 차이라고 생각

| | Hashtable | HashMap |
|:---:|:---:|:---:|
| 동기화<br>(thread-safe) | thread safe | thread safe 하지 않음 |
| Key에 Null 값 허용 여부 | 허용하지 않음 | 허용 |
| 데이터 접근 | Enumeration | Iterator |
| 성능 | 상대적으로 낮음 | 상대적으로 좋음 |

> Enumeration vs Iterator 
> - 컬렉션(collection) 인터페이스를 사용하는 클래스의 데이터를 순환해서 가져오는 방법
> - Enumeration은 스레드에 안전한 구조
> - Iterator는 스레드에 안전하지 않는 구조

### Hashtable vs SynchronizedMap vs ConcurrentHashMap
- Hashtable: legacy class로 thread-safe하지만 병목 발생
- SynchronizedMap: thread-safe하지만 map 전체에 lock/unlock
- ConcurrentHashMap: thread-safe하며 세그먼트(map을 작은 단위로 분리) 단위로 lock/unlock

> ConcurrentHashMap이 가장 성능이 좋음

### Hash 조회 시 big-o
- 일반적으로 k-v 형태이기 때문에 데이터 처리의 시간복잡도는 O(1)
- 다만 hash function이 매우 복잡한 경우 연산 시간이 증가할 수 있음

~~- ## Stack~~

~~- ## Queue~~

## Stack / Queue
| | Stack | Queue |
|:---:|:---:|:---:|
| I/O | LIFO | FIFO |
| Access point | top | front(삭제), rear(삽입) |  
| Method | push, pop | enqueue, dequeue |

---

~~- Graph~~

~~- Tree~~

~~- 그래프와 트리의 차이점~~

## Graph / Tree
| | Graph | Tree |
|:---:|:---:|:---:|
| component | 점(노드), 간선(노드 간의 연결) | 점(노드), 간선(노드 간의 연결) |
| cycle | 순환, 비순환, 자기순환 | 비순환 |
| root | root node 존재 X | root node 존재 |
| parent-child | X | O |
| model | 네트워크 모델	| 계층 모델 |

### Heap
- 트리 기반 자료구조로 힙 속성을 만족하는 거의 완전한 트리
    - 최대힙(Max Heap)일 경우 부모 노드는 반드시 자식 노드보다 값이 커야 한다는 법칙 or 최소
- 보통 PriorityQueue 사용

#### Binary Heap
- 이진 트리 형태인 힙
- 최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안

#### Heap sort
- 힙에 자료를 하나 넣을 때 평균 logn의 복잡도를 갖기 때문에 이를 n번 반복하면 전체 복잡도는 nlgon
- 힙 정렬은 퀵 정렬과 평균 시간 복잡도는 동일하지만, 퀵 정렬이 최악의 경우 n^2이 나오는 것에 비해 언제나 nlogn을 넘지 않음

### Red-Black Tree
- 자가 균형 이진 탐색 트리

    ```
    1. 모든 노드는 빨간색 혹은 검은색이다.
    2. 루트 노드는 검은색이다.
    3. 모든 리프 노드(NIL)들은 검은색이다. (NIL : null leaf, 자료를 갖지 않고 트리의 끝을 나타내는 노드)
    4. 빨간색 노드의 자식은 검은색이다.
    == No Double Red(빨간색 노드가 연속으로 나올 수 없다)
    5. 모든 리프 노드에서 Black Depth는 같다.
    == 리프노드에서 루트 노드까지 가는 경로에서 만나는 검은색 노드의 개수가 같다.
    ```

- ref. https://code-lab1.tistory.com/62

- 자료의 삽입과 삭제, 검색에서 최악의 경우에도 일정한 실행 시간을 보장
    - Java의 Collection에서 ArrayList의 내부적인 알고리즘이 RBT로 이루어져 있음.

## B-Tree / B+Tree

### B-Tree
- 하나의 노드에 많은 정보를 가지거나, 두 개 이상의 자식을 가질 수 있음, 균형 이진 트리의 연속
    - 균형이진트리는 leaf node들의 레벨차이가 최대 1레벨까지만 나는 트리

- File system 또는 DB에 활용
    - 어떤 값에 대해서도 같은 시간에 결과를 얻을 수 있음 (균형 유지)
    - InnoDB는 B+Tree

### B+Tree
- B+tree는 B-tree의 확장개념으로, B-tree의 경우, internal 또는 branch 노드에 key와 data를 담을 수 있음
    - 하지만, B+tree의 경우 브랜치 노드에 key만 담아두고, data는 담지 않음
    - 오직 리프 노드에만 key와 data를 저장하고, 리프 노드끼리 Linked list로 연결

- 리프 노드를 제외하고 데이터를 담아두지 않기 때문에 메모리를 더 확보함으로써 더 많은 key들을 수용할 수 있음
    - 하나의 노드에 더 많은 key들을 담을 수 있기에 트리의 높이(depth)는 더 낮아짐 (cache hit를 높일 수 있음)
- 풀 스캔 시, B+tree는 리프 노드에 데이터가 모두 있기 때문에 한 번의 선형탐색만 하면 되기 때문에 B-tree에 비해 빠름

- ref. https://zorba91.tistory.com/293

## 요청이 계속 들어오는 서버가 있고 접속로그를 저장하고 싶다. 어떤 자료구조를 활용하면 좋은가?

LSM 트리

- https://sungwookkang.com/1480
- https://www.linkedin.com/pulse/comparing-lsm-tree-b-tree-sameh-muhammed/  
- https://sukill.tistory.com/87
- https://velog.io/@kimtjsdlf/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%EC%99%80-%EC%9D%B8%EB%8D%B1%EC%8A%A4LSM%ED%8A%B8%EB%A6%AC%EA%B3%BC-B%ED%8A%B8%EB%A6%AC
---
full-text index vs elastic search : https://kyuu.oopy.io/544f9ee8-7750-4315-ac7c-910175f8c40c
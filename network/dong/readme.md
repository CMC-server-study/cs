# Network

## OSI 7계층
- 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것 -> why? : 규격화를 통해 통신과 관련된 유지보수 용이, 사용성 향상, 비용 절감

- https://devhdong.tistory.com/9

## TCP/IP
- 대부분의 애플리케이션들이 인터넷을 통해 통신하는데 사용하는 프로토콜
- network layer(네트워크상 최종 목적지까지 정확하게 연결되도록 연결성을 제공)와 transport layer(연결을 제어하고, 신뢰성 있는 데이터 전송을 담당)의 프로토콜
- HTTP를 많이 쓰고 있으면서 TCP/IP가 강조되는 이유?
    - HTTP 명세는 HTTP 메시지 포맷에 대해서 구체적으로 정의하고 있지만, HTTP 커넥션과 메시지 흐름에 대한 내용은 충분히 다루지 않음
    - HTTP는 application layer protocol이고, 커넥션 및 전송과 관련된 부분은 하위 layer 기반해서 작동하기 때문

## TCP와 UDP
- 가장 큰 차이는 신뢰성과 연결성에 있음

- TCP는 신뢰성 있고 연결지향적이지만 UDP는 신뢰성이 없고, 비연결적

- TCP는 송신자-수신자 연결이 되어야 통신가능, UDP는 연결 없이도 통신 가능
    - TCP: Segment
    - UDP: Datagram

- https://devhdong.tistory.com/10

## TCP의 3 way handshake와 4 way handshake
- TCP의 연결 성립과 종료 방법

### 3 way handshake

![image](https://user-images.githubusercontent.com/59307414/226628415-84d49954-9603-4128-8229-95fe471ce5a0.png)

1. 클라이언트가 서버에게 SYN 패킷을 보냄 (sequence : x)

    - sequence number는 random (https://github.com/Effective-Java-Camp/http-the-definitive-guide/issues/4)

2. 서버가 SYN(x)을 받고, 클라이언트로 받았다는 신호인 ACK와 SYN 패킷을 보냄
    
    - (sequence : y, ACK : x + 1)
    
3. 클라이언트는 서버의 응답은 ACK(x+1)와 SYN(y) 패킷을 받고, ACK(y+1)를 서버로 보냄

### 4 way handshake

![image](https://user-images.githubusercontent.com/59307414/226628860-2b150c2a-9cb2-4584-8a33-7aec40a0f596.png)

- 연결 성립 후, 모든 통신이 끝났다면 해제

1. 클라이언트는 서버에게 연결을 종료한다는 FIN 플래그를 보낸다.
2. 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보낸다. (이때 모든 데이터를 보내기 위해 CLOSE_WAIT 상태가 된다)
3. 데이터를 모두 보냈다면, 연결이 종료되었다는 FIN 플래그를 클라이언트에게 보낸다.
4. 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보낸다. (아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT을 통해 기다린다.)

- 서버는 ACK를 받은 이후 소켓을 닫는다 (Closed)
- TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (Closed)

## TCP의 흐름 제어, 혼잡 제어
- 흐름 제어(Flow control): 송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법
    - 수신측이 송신측보다 데이터 처리 속도가 빠르면 문제없지만, 송신측의 속도가 빠를 경우 문제가 생긴다
    - Flow Control은 receiver가 packet을 지나치게 많이 받지 않도록 조절하는 것
    - 기본 개념은 receiver가 sender에게 현재 자신의 상태를 feedback 한다는 점

- 혼잡 제어(Congestion control): 송신측의 데이터 전달과 네트워크의 데이터 처리 속도 차이를 해결하기 위한 기법
    - 송신측의 데이터는 지역망이나 인터넷으로 연결된 대형 네트워크를 통해 전달된다. 만약 한 라우터에 데이터가 몰릴 경우, 자신에게 온 데이터를 모두 처리할 수 없게 된다. 이런 경우 호스트들은 또 다시 재전송을 하게되고 결국 혼잡만 가중시켜 오버플로우나 데이터 손실을 발생시키게 된다. 따라서 이러한 네트워크의 혼잡을 피하기 위해 송신측에서 보내는 데이터의 전송속도를 강제로 줄이게 되는데, 이러한 작업을 혼잡제어라고 한다.

- https://github.com/wilump-labs/cs/tree/main/network#tcp-%ED%9D%90%EB%A6%84-%EC%A0%9C%EC%96%B4flow-control--%ED%98%BC%EC%9E%A1-%EC%A0%9C%EC%96%B4congestion-control

## 데이터 캡슐화
- 계층 간 데이터 전송을 위해 캡슐화/역캡슐화를 진행

- https://velog.io/@qmasem/TIL-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%BA%A1%EC%8A%90%ED%99%94-%EC%97%AD%EC%BA%A1%EC%8A%90%ED%99%94-encapsulation-decapsulation

---

## HTTP와 HTTPS
### HTTP
- 웹 서버와 클라이언트 간의 문서를 교환하기 위한 통신 규약
- 웹에서만 사용하는 프로토콜로 TCP/IP 기반으로 서버와 클라이언트 간의 요청과 응답을 전송한다.

### HTTPS
- HTTP 통신하는 소켓 부분을 인터넷 상에서 정보를 암호화하는 SSL(Secure Socket Layer)라는 프로토콜로 대체한 것이다.
    - HTTPS는 단지 보안 전송 계층을 통해 전송되는 HTTP이다.
    - HTTP 메시지를 TCP로 보내기 전에 먼저 그것들을 암호화하는 보안 계층으로 보낸다.
    - HTTPS의 보안 계층은, SSL과 그것의 현대적인 대체품인 TLS로 구현되었다.
    - HTTPS 프로토콜에서 URL의 스킴 접두사는 https다.
    - HTTPS의 포토는 443(기본값)을 이용하며 HTTP 80과는 다르다.
    - HTTPS는 443번 포트로 연결하고 서버와 바이너리 포맷으로 된 몇몇 SSL 보안 매개변수를 교환하면서 핸드셰이크를 하고, 암호화된 HTTP 명령이 뒤따른다.

- HTTP는 TCP와 통신했지만, HTTPS에서 HTTP는 SSL과 통신하고 SSL이 TCP와 통신하게 된다.
    - 즉, 하나의 레이어를 더 둔 것이다.

- HTTPS의 SSL에서는 대칭키 암호화 방식과 공개키 암호화 방식을 모두 사용한다.

- https 동작 과정: https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Network/HTTP%2C%20HTTPS.md

### SSL(Secure Sockets Layer)
- 웹사이트와 브라우저 사이(또는 두 서버 사이)에 전송되는 데이터를 암호화하여 인터넷 연결을 보호하기 위한 기술

- TLS(Transport Layer Security) : SSL의 업데이트 버전 (SSL 표현이 상용화되어서 HTTPS를 이야기할 때 SSL을 이야기하지만 실제로 TLS 암호화를 의미)

- https://kanoos-stu.tistory.com/46

### cf. 공개키/대칭키
#### 대칭키
- 암호화와 복호화에 같은 암호키(대칭키)를 사용하는 알고리즘
- 동일한 키를 주고받기 때문에, 매우 빠르다는 장점이 있음
- 그러나 대칭키 전달 과정에서 해킹 위험에 노출

#### 공개키
- 암호화와 복호화에 사용하는 암호키를 분리한 알고리즘
- 자신이 가지고 있는 고유한 암호키(비밀키)로만 복호화할 수 있는 암호키(공개키)를 대중에 공개

#### 공개키 암호화 방식 진행 과정
1. A가 웹 상에 공개된 'B의 공개키'를 이용해 평문을 암호화하여 B에게 보냄
2. B는 자신의 비밀키로 복호화한 평문을 확인, A의 공개키로 응답을 암호화하여 A에게 보냄
3. A는 자신의 비밀키로 암호화된 응답문을 복호화함

- 대칭키의 단점을 완벽하게 해결했지만, 암호화 복호화가 매우 복잡함
    - 암호화하는 키가 복호화하는 키가 서로 다르기 때문

- 대칭키와 공개키 암호화 방식을 적절히 혼합해보면?
    - SSL 탄생의 시초가 됨

1. A가 B의 공개키로 암호화 통신에 사용할 대칭키를 암호화하고 B에게 보냄
2. B는 암호문을 받고, 자신의 비밀키로 복호화함
3. B는 A로부터 얻은 대칭키로 A에게 보낼 평문을 암호화하여 A에게 보냄
4. A는 자신의 대칭키로 암호문을 복호화함
5. 앞으로 이 대칭키로 암호화를 통신함
즉, 대칭키를 주고받을 때만 공개키 암호화 방식을 사용하고 이후에는 계속 대칭키 암호화 방식으로 통신하는 것!

## HTTP 1, 1.1, 2, 3의 차이
- HTTP 1.0 vs 1.1 : https://github.com/Effective-Java-Camp/http-the-definitive-guide/issues/2

- HTTP 1.1 vs 2.0 : https://github.com/Effective-Java-Camp/http-the-definitive-guide/issues/10

- HTTP 3.0
    - UDP 기반
    - QUIC 프로토콜
        - 응답 헤더에 `alt-svc` 붙음
            <img width="692" alt="스크린샷" src="https://user-images.githubusercontent.com/59307414/226635304-bff099ef-a05d-4531-a4a8-d946870de464.png">

    - https://www.smashingmagazine.com/2021/08/http3-core-concepts-part1/
    - https://evan-moon.github.io/2019/10/08/what-is-http3/

## HTTP의 GET과 POST
- 요청하는 HTTP 메세지 본문(body) 유무 차이
    - GET: 없음
    - POST: 있음
- 안전성(호출 시 리소스 변경 여부)
    - GET: 안전함
    - POST: 안전하지 않음
- 멱등성(중복 호출 시 결과 변경 여부)
    - GET: 멱등성 보장
    - POST: 멱등성 보장하지 않음

## HTTP 요청 응답 헤더
- 요청과 응답 메시지에 더하는 추가 정보
- 이름/값 쌍의 목록
- 일반적인 헤더

    | 헤더              | 설명                                                         |
    | ----------------- | ------------------------------------------------------------ |
    | Connection        | 클라이언트와 서버가 요청/응답 연결에 대한 옵션을 정할 수 있게 해준다 |
    | Date              | 메세지가 언제 만들어졌는지에 대한 시간                       |
    | MIME-Version      | 발송자가 사용한 MIME의 버젼을 알려준다                       |
    | Transfer-Encoding | 수신자에게 안전한 전송을 위해 어떠한 인코딩이 적용되었는지 알려준다 |
    | Upgrade           | 발송자가 업그레이드 하길 원하는 프로토콜 버젼                |
    | Via               | 어떤 중개자로부터 왔는지 알려준다             |
    | Cache-Control     | 메세지와 함께 캐시 지지자를 전달하기 위해 사용               |

## CORS(Cross-Origin Resource Sharing)
- 교차 출처 리소스 공유
    - 다른 origin의 리소스를 공유하려고 한다.
    - origin = protocol + host + port
- 그럼 왜 막는가?
    - 다른 사이트에서 원래 사이트를 모방할 수 있음
- 절대로 안 되는가?
    - 서버에서 cors 허용 설정

### cf. SOP(Same-Origin Policy)
- 같은 출처에서만 리소스를 공유
- 근데 일반적인 애플리케이션에서 같은 origin의 리소스만을 사용할 수 없기 때문에 이 정책에 대한 예외로 cors 존재

## REST와 RESTful
- URI에 자원을 명시해서 의미를 명확하게 전달
- cf. SOAP(Simple Object Access Protocol): XML 기반 프로토콜
    - https://www.redhat.com/en/topics/integration/whats-the-difference-between-soap-rest
    - 두 프로토콜 비교를 요약하면 REST API가 가볍고 요구사항을 고려했을 때 조금 더 유연하게 사용할 수 있다

## 소켓
- 네트워크 상에서 돌아가는 두 개의 프로그램 간 양방향 통신의 하나의 엔트 포인트

- bind: 소켓에 주소를 할당
- listen: 연결 요청 대기
- accept: 연결 요청 수락
- https://github.com/Effective-Java-Camp/http-the-definitive-guide/blob/main/examples/tcp-socket/server.c

## Socket.io와 WebSocket
### WebSocket
- HTML5 웹 표준 기술로, 서버와 브라우저 간 연결을 유지한 상태로 데이터를 교환할 수 있는 프로토콜
    - 양방향 실시간 통신이 가능
- https://datatracker.ietf.org/doc/html/rfc6455
- https://ko.javascript.info/websocket

### Socket.io
- WebSocket을 이용해서 JavaScript 진영에서 만든 이벤트 기반 라이브러리가 socket.io

---

## 쿠키와 세션
### 쿠키
- 사용자의 컴퓨터에 저장하는 작은 기록 정보 파일 (클라이언트 보관)

### 세션
- 웹 브라우저를 통해 웹 서버에 접속한 시점부터 웹 브라우저를 종료하기 전까지를 하나의 연결(요청)으로 간주하고 상태를 유지하는 방법 (서버 보관 - 클라이언트의 쿠키 이용)

### 쿠키 vs 세션
- https://dev-coco.tistory.com/61   

### 브라우저는 쿠키를 어떻게 저장하는가?
- 쿠키는 '임의의 이름=값' 형태의 리스트를 가지고, 그 리스트는 Set-Cookie 혹은 Set-Cookie2(확장 헤더) 같은 HTTP 응답 헤더에 기술되어 전달
- 브라우저가 서버 관련 정보를 저장하고 그 서버에 접속할 때 마다 그 정보를 활용
- 구글 크롬 쿠키
    - 각 브라우저는 각기 다른 방식으로 쿠키를 저장한다.
    - 구글 크롬은 Cookies라는 SQLite 파일에 쿠키를 저장한다.
    - 각 행이 쿠키 한 개에 해당하며, 총 13개 필드가 있다.

## DNS(Domain Name System)
- 숫자로 된 IP 주소를 사람이 인식하기 쉽게 변환 (e.g. 서울특별시 종로구 효자로 12 -> 광화문)

- DNS 작동 원리 : https://velog.io/@minj9_6/DNS%EC%99%80-%EC%9E%91%EB%8F%99%EC%9B%90%EB%A6%AC
    - https://aws.amazon.com/ko/route53/what-is-dns/

### Round Robin DNS 
- RR: 선점형 스케줄링로, 프로세스들 사이에 우선순위를 두지 않고, 순서대로 시간단위(Time Quantum/Slice)로 CPU를 할당하는 방식의 CPU 스케줄링 알고리즘

- 별도의 LB 장비를 두지 않고, DNS만을 이용하여 도메인 레코드 정보를 조회하는 시점에서 트래픽을 분산하는 기법
    - 도메인 주소를 입력하면 해당 도메인 주소에 연결되는 서버를 RR로 접속을 분배

- 단점: 각 서버 별로 health check를 진행할 수 없음(why? RR로 랜덤하게 선택하기 때문에 특정 서버를 선택하지 못함) -> 고가용성(HA) 보장 X

## ~~Nginx와 아파치 웹 서버의 차이~~
- https://github.com/ruthetum/study/blob/main/nginx/compairson-apache-nginx.md

- nginx load balancing: https://www.lesstif.com/system-admin/nginx-load-balancing-35357063.html

## CDN(Content Delivery Network)
- Geographically distributed users (지리적으로 분산된 사용자에게 지리적 제약을 해소)
- Faster performance (빠른 성능)
- Peak traffic handling (트래픽 처리 향상)
- Traditional - Enterprise CDN
    - Akamai, Limelight Networks, Edgio, Cloudflare ...
- CDN on the cloud service
    - AWS CloudFront, Google Cloud CDN, Azure CDN

## LRU 캐싱
- LRU(Least Recently Used): 가장 오랫동안 참조되지 않은 페이지를 교체
- 캐시에 공간이 부족할 때 가장 오랫동안 사용하지 않은 항목을 제거하고 새로운 녀석을 배치하는 형식

## daum.net을 쳤을 때 일어나는 과정을 네트워크 관점에서 설명해보아라.
1. URL에서 protocol, host, (port), path 확인
2. 웹 브라우저가 도메인명의 IP 주소 조회 (DNS 조회)
3. 웹 브라우저가 서버와의 TCP 연결 시작
4. 웹 브라우저는 서버에 HTTP 요청 전송
5. 서버는 웹 브라우저에 HTTP 응답 반환 (리소스)
6. 커넥션이 닫히면, 웹 브라우저는 문서를 출력 (컨텐츠 렌더링)

- 3,4,5 : application layer to application layer
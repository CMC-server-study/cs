# Network

- OSI 7계층
    - ref. https://devhdong.tistory.com/9

- TCP/IP
    - TL;DR

- TCP와 UDP
    - https://devhdong.tistory.com/10

- TCP의 3 way handshake와 4 way handshake
    - https://github.com/wilump-labs/cs/tree/main/network#tcp-3-way-handshake--4-way-handshake

- TCP의 흐름 제어, 혼잡 제어
    - https://github.com/wilump-labs/cs/tree/main/network#tcp-%ED%9D%90%EB%A6%84-%EC%A0%9C%EC%96%B4flow-control--%ED%98%BC%EC%9E%A1-%EC%A0%9C%EC%96%B4congestion-control

- 데이터 캡슐화
    - https://velog.io/@qmasem/TIL-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%BA%A1%EC%8A%90%ED%99%94-%EC%97%AD%EC%BA%A1%EC%8A%90%ED%99%94-encapsulation-decapsulation

---

- HTTP와 HTTPS
    - HTTP 1, 1.1, 2, 3의 차이

        - HTTP 1.0 vs 1.1 : https://github.com/Effective-Java-Camp/http-the-definitive-guide/issues/2
        - HTTP 1.1 vs 2.0 : https://github.com/Effective-Java-Camp/http-the-definitive-guide/issues/10

        - HTTP 3.0
            - UDP 기반
            - QUIC 프로토콜
            - ref. https://evan-moon.github.io/2019/10/08/what-is-http3/
            - 추가 자료 첨부

    - HTTP의 GET과 POST

        - 요청하는 HTTP 메세지 본문(body) 유무 차이
            - GET: 없음
            - POST: 있음
        - 안전성(호출 시 리소스 변경 여부)
            - GET: 안전함
            - POST: 안전하지 않음
        - 멱등성(중복 호출 시 결과 변경 여부)
            - GET: 멱등성 보장
            - POST: 멱등성 보장하지 않음

    - HTTP 요청 응답 헤더
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

    - HTTP와 HTTPS 동작 과정

        - 


- SSL

- CORS

- REST와 RESTful

- 소켓

- Socket.io와 WebSocket

---

- 쿠키와 세션
    - 브라우저는 쿠키를 어떻게 저장하는가?
- DNS
    - DNS Round Robin

- ~~Nginx와 아파치 웹 서버의 차이~~

    - https://github.com/ruthetum/study/blob/main/nginx/compairson-apache-nginx.md

- CDN

- LRU 캐싱


- daum.net을 쳤을 때 일어나는 과정을 네트워크 관점에서 설명해보아라.
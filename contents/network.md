# 2. Network

#### :small_orange_diamond:OSI 7계층
<img src="./images/osi-7-layer.png" width="60%" height="60%">

> - []()

#### :small_orange_diamond:TCP/IP의 개념
<!-- * 네트워크를 상호 연결시켜 정보를 전송할 수 있도록 하는 기능을 가진 다수의 프로토콜이 모여있는 프로토콜 집합
* 인터넷: 데이터 링크 계층을 지원하는 네트워크는 TCP/IP 프로토콜을 이용하여 상호 연결하는 네트워크 -->

#### :small_orange_diamond:TCP와 UDP
* 네트워크 계층 중 **전송 계층에서 사용하는 프로토콜**
* TCP(Transmission Control Protocol)  
    <img src="./images/tcp-virtual-circuit.png" width="60%" height="60%">
    * 인터넷 상에서 데이터를 메세지의 형태(**세그먼트** 라는 블록 단위)로 보내기 위해 IP와 함께 사용하는 프로토콜이다.
    * TCP와 IP를 함께 사용하는데, IP가 데이터의 배달을 처리한다면 TCP는 패킷을 추적 및 관리한다.
    * **연결형 서비스로** 가상 회선 방식을 제공한다.
        * 3-way handshaking과정을 통해 연결을 설정하고, 4-way handshaking을 통해 연결을 해제한다.
    * 흐름제어 및 혼잡제어를 제공한다.
        * 흐름제어
            * 데이터를 송신하는 곳과 수신하는 곳의 데이터 처리 속도를 조절하여 수신자의 버퍼 오버플로우를 방지하는 것
            * 송신하는 곳에서 감당이 안되게 많은 데이터를 빠르게 보내 수신하는 곳에서 문제가 일어나는 것을 막는다.
        * 혼잡제어
            * 네트워크 내의 패킷 수가 넘치게 증가하지 않도록 방지하는 것
            * 정보의 소통량이 과다하면 패킷을 조금만 전송하여 혼잡 붕괴 현상이 일어나는 것을 막는다.
    * 높은 신뢰성을 보장한다.
    * UDP보다 속도가 느리다.
    * 전이중(Full-Duplex), 점대점(Point to Point) 방식이다.
        * 전이중
            * 전송이 양방향으로 동시에 일어날 수 있다.
        * 점대점
            * 각 연결이 정확히 2개의 종단점을 가지고 있다.
        * 멀티캐스팅이나 브로드캐스팅을 지원하지 않는다.
    * 연속성보다 신뢰성있는 전송이 중요할 때에 사용된다.
* UDP(User Datagram Protocol)  
    <img src="./images/udp-datagram.png" width="60%" height="60%">
    * 데이터를 **데이터그램** 단위로 처리하는 프로토콜이다.
    * **비연결형 서비스로** 데이터그램 방식을 제공한다.
        * 연결을 위해 할당되는 논리적인 경로가 없다.
        * 그렇기 때문에 각각의 패킷은 다른 경로로 전송되고, 각각의 패킷은 독립적인 관계를 지니게 된다.
        * 이렇게 데이터를 서로 다른 경로로 독립적으로 처리한다.
    * 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.
    * UDP헤더의 CheckSum 필드를 통해 최소한의 오류만 검출한다.
    * 신뢰성이 낮다.
    * TCP보다 속도가 빠르다.
    * 신뢰성보다는 연속성이 중요한 서비스, 예를 들면 실시간 서비스(streaming)에 사용된다.
* 참고
  * UDP와 TCP는 각각 별도의 포트 주소 공간을 관리하므로 같은 포트 번호를 사용해도 무방하다. 즉, 두 프로토콜에서 동일한 포트 번호를 할당해도 서로 다른 포트로 간주한다.
  * 또한 같은 모듈(UDP or TCP) 내에서도 클라이언트 프로그램에서 동시에 여러 커넥션을 확립한 경우에는 서로 다른 포트 번호를 동적으로 할당한다. (동적할당에 사용되는 포트번호는 49,152~65,535이다.)

> - [http://mangkyu.tistory.com/15](http://mangkyu.tistory.com/15)
> - [http://ddooooki.tistory.com/21](http://ddooooki.tistory.com/21)

#### :small_orange_diamond:TCP와 UDP의 헤더 분석

> - [https://idchowto.com/?p=18352](https://idchowto.com/?p=18352)
> - [https://m.blog.naver.com/PostView.nhn?blogId=koromoon&logNo=120162515270&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F](https://m.blog.naver.com/PostView.nhn?blogId=koromoon&logNo=120162515270&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F)

#### :small_orange_diamond:TCP의 3-way-handshake, 4-way-handshake
* TCP는 장치들 사이에 논리적인 접속을 성립(establish)하기 위하여 연결을 설정하여 **신뢰성을 보장하는 연결형 서비스** 이다.
* 3-way handshake 란
  * TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 **연결을 설정(Connection Establish)** 하는 과정
  * 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한 쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.
  * 즉, TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.
      * A 프로세스(Client)가 B 프로세스(Server)에 연결을 요청
      <img src="./images/3-way-handshaking.png" width="60%" height="60%">
      * 1. A -> B: SYN
          * 접속 요청 프로세스 A가 연결 요청 메시지 전송 (SYN)
          * 송신자가 최초로 데이터를 전송할 때 Sequence Number를 임의의 랜덤 숫자로 지정하고, SYN 플래그 비트를 1로 설정한 세그먼트를 전송한다.
          * PORT 상태 - B: LISTEN, A: CLOSED
      * 2. B -> A: SYN + ACK
          * 접속 요청을 받은 프로세스 B가 요청을 수락했으며, 접속 요청 프로세스인 A도 포트를 열어 달라는 메시지 전송 (SYN + ACK)
          * 수신자는 Acknowledgement Number 필드를 (Sequence Number + 1)로 지정하고, SYN과 ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.
          * PORT 상태 - B: SYN_RCV, A: CLOSED
      * 3. A -> B: ACK
          * PORT 상태 - B: SYN_RCV, A: ESTABLISHED
          * 마지막으로 접속 요청 프로세스 A가 수락 확인을 보내 연결을 맺음 (ACK)
          * 이때, 전송할 데이터가 있으면 이 단계에서 데이터를 전송할 수 있다.
          * PORT 상태 - B: ESTABLISHED, A: ESTABLISHED
* 4-way handshake 란
  * TCP의 **연결을 해제(Connection Termination)** 하는 과정
      * A 프로세스(Client)가 B 프로세스(Server)에 연결 해제를 요청
      <img src="./images/4-way-handshaking.png" width="60%" height="60%">
      * 1. A -> B: FIN
          * 프로세스 A가 연결을 종료하겠다는 FIN 플래그를 전송
          * 프로세스 B가 FIN 플래그로 응답하기 전까지 연결을 계속 유지
      * 2. B -> A: ACK
          * 프로세스 B는 일단 확인 메시지를 보내고 자신의 통신이 끝날 때까지 기다린다. (이 상태가 TIME_WAIT 상태)
          * 수신자는 Acknowledgement Number 필드를 (Sequence Number + 1)로 지정하고, ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.
          * 그리고 자신이 전송할 데이터가 남아있다면 이어서 계속 전송한다.
      * 3. B -> A: FIN
          * 프로세스 B가 통신이 끝났으면 연결 종료 요청에 합의한다는 의미로 프로세스 A에게 FIN 플래그를 전송
      * 4. A -> B: ACK
          * 프로세스 A는 확인했다는 메시지를 전송
* 참고 - ***포트(PORT) 상태 정보***
  * CLOSED: 포트가 닫힌 상태
  * LISTEN: 포트가 열린 상태로 연결 요청 대기 중
  * SYN_RCV: SYNC 요청을 받고 상대방의 응답을 기다리는 중
  * ESTABLISHED: 포트 연결 상태
* 참고 - ***플래그 정보***
  * TCP Header에는 CONTROL BIT(플래그 비트, 6bit)가 존재하며, 각각의 bit는 "URG-ACK-PSH-RST-SYN-FIN"의 의미를 가진다.
    * 즉, 해당 위치의 bit가 1이면 해당 패킷이 어떠한 내용을 담고 있는 패킷인지를 나타낸다.
  * SYN(Synchronize Sequence Number) / 000010
    * 연결 설정. Sequence Number를 랜덤으로 설정하여 세션을 연결하는 데 사용하며, 초기에 Sequence Number를 전송한다.
  * ACK(Acknowledgement) / 010000
    * 응답 확인. 패킷을 받았다는 것을 의미한다.
    * Acknowledgement Number 필드가 유효한지를 나타낸다.
    * 양단 프로세스가 쉬지 않고 데이터를 전송한다고 가정하면 최초 연결 설정 과정에서 전송되는 첫 번째 세그먼트를 제외한 모든 세그먼트의 ACK 비트는 1로 지정된다고 생각할 수 있다.
  * FIN(Finish) / 000001
    * 연결 해제. 세션 연결을 종료시킬 때 사용되며, 더 이상 전송할 데이터가 없음을 의미한다.

> - [http://needjarvis.tistory.com/157](http://needjarvis.tistory.com/157)
> - [http://hyeonstorage.tistory.com/286](http://hyeonstorage.tistory.com/286)

#### :question:TCP 관련 질문 1
* Q. TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유?
  * A. Client가 데이터 전송을 마쳤다고 하더라도 Server는 아직 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문이다.
  * [관련 Reference](http://ddooooki.tistory.com/21)

#### :question:TCP 관련 질문 2
* Q. 만약 Server에서 FIN 플래그를 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN 패킷보다 늦게 도착하는 상황이 발생하면 어떻게 될까?
  * A. 이러한 현상에 대비하여 Client는 Server로부터 FIN 플래그를 수신하더라도 일정시간(Default: 240sec)동안 세션을 남겨 놓고 잉여 패킷을 기다리는 과정을 거친다. (TIME_WAIT 과정)
  * [관련 Reference]((http://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)

#### :question:TCP 관련 질문 3
* Q. 초기 Sequence Number인 ISN을 0부터 시작하지 않고 난수를 생성해서 설정하는 이유?
  * A. Connection을 맺을 때 사용하는 포트(Port)는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용된다. 따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용하는 가능성이 존재한다. 서버 측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데 난수가 아닌 순처적인 Number가 전송된다면 이전의 Connection으로부터 오는 패킷으로 인식할 수 있다. 이런 문제가 발생할 가능성을 줄이기 위해서 난수로 ISN을 설정한다.
  * [관련 Reference](http://asfirstalways.tistory.com/356)

#### :small_orange_diamond:HTTP, HTTPS
* HTTP 프로토콜
  * 웹상에서 클라이언트와 서버 간에 요청/응답으로 정보를 주고 받을 수 있는 프로토콜

#### :small_orange_diamond:GET 메서드와 POST 메서드
* HTTP 프로토콜을 이용해서 서버에 데이터(요청 정보)를 전달할 때 사용하는 방식
* GET 메서드 방식
  * 개념
    * 정보를 조회하기 위한 메서드
    * 서버에서 어떤 데이터를 가져와서 보여주기 위한 용도의 메서드
    * **가져오는 것(Select)**
  * 사용 방법
    * URL의 끝에 '?'가 붙고, 요청 정보가 (key=value)형태의 쌍을 이루어 ?뒤에 이어서 붙어 서버로 전송한다.
    * 요청 정보가 여러 개일 경우에는 '&'로 구분한다.
    * Ex) www.urladdress.xyz?name1=value1&name2=value2
  * 특징
    * URL에 요청 정보를 붙여서 전송한다.
    * URL에 요청 정보가 이어붙기 때문에 길이 제한이 있어서 대용량의 데이터를 전송하기 어렵다.
      * 한 번 요청 시 전송 데이터(주솟값 + 파라미터)의 양은 255자로 제한된다.(HTTP/1.1은 2048자)
    * 요청 정보를 사용자가 쉽게 눈으로 확인할 수 있다.
      * POST 방식보다 보안상 취약하다.
    * HTTP 패킷의 Body는 비어 있는 상태로 전송한다.
      * 즉, Body의 데이터 타입을 표현하는 'Content-Type' 필드도 HTTP Request Header에 들어가지 않는다.
    * POST 방식보다 빠르다.
      * GET 방식은 캐싱을 사용할 수 있어, GET 요청과 그에 대한 응답이 브라우저에 의해 캐쉬된다.
* POST 메서드 방식
  * 개념
    * 서버의 값이나 상태를 바꾸지 위한 용도의 메서드
    * **수행하는 것(Insert, Update, Delete)**
  * 사용 방법
    * 요청 정보를 HTTP 패킷의 Body 안에 숨겨서 서버로 전송한다.
    <!-- * Form 태그을 이용해서 submit 하는 형태 -->
    * Request Header의 Content-Type에 해당 데이터 타입이 표현되며, 전송하고자 하는 데이터 타입을 적어주어야 한다.
      * Default: application/octet-stream
      * 단순 txt의 경우: text/plain
      * 파일의 경우: multipart/form-date
  * 특징
    * Body 안에 숨겨서 요청 정보를 전송하기 때문에 대용량의 데이터를 전송하기에 적합하다.
    * 클라이언트 쪽에서 데이터를 인코딩하여 서버로 전송하고, 이를 받은 서버 쪽이 해당 데이터를 디코딩한다.
    * GET 방식보다 보안상 안전하다.
* Q. 조회하기 위한 용도 POST가 아닌 GET 방식을 사용하는 이유?
  1. 설계 원칙에 따라 GET 방식은 서버에게 여러 번 요청을 하더라도 동일한 응답이 돌아와야 한다. (Idempotent, 멱등)
      * GET 방식은 **가져오는 것(Select)** 으로, 서버의 데이터나 상태를 변경시키지 않아야 한다.
          * Ex) 게시판의 리스트, 게시글 보기 기능
          * 예외) 방문자의 로그 남기기, 글을 읽은 횟수 증가 기능
      * POST 방식은 **수행하는 것** 으로, 서버의 값이나 상태를 바꾸기 위한 용도이다.
          * Ex) 게시판에 글쓰기 기능
  2. 웹에서 모든 리소스는 Link할 수 있는 URL을 가지고 있어야 한다.
      * 어떤 웹페이지를 보고 있을 때 다른 사람한테 그 주소를 주기 위해서 주소창의 URL을 복사해서 줄 수 있어야 한다.
      * 즉, 어떤 웹페이지를 조회할 때 원하는 페이지로 바로 이동하거나 이동시키기 위해서는 해당 링크의 정보가 필요하다.
      * 이때 POST 방식을 사용할 경우에 값(링크의 정보)이 Body에 있기 때문에 URL만 전달할 수 없으므로 GET 방식을 사용해야한다. 그러나 글을 저장하는 경우에는 URL을 제공할 필요가 없기 때문에 POST 방식을 사용한다.

<!-- * 클라이언트에서 서버로 데이터를 전송하려면 GET이나 POST 방식밖에 없다. -->

> - [https://blog.outsider.ne.kr/312](https://blog.outsider.ne.kr/312)
> - [https://hongsii.github.io/2017/08/02/what-is-the-difference-get-and-post/](https://hongsii.github.io/2017/08/02/what-is-the-difference-get-and-post/)
> - [https://www.w3schools.com/tags/ref_httpmethods.asp](https://www.w3schools.com/tags/ref_httpmethods.asp)

#### :small_orange_diamond:쿠키, 세션

#### :small_orange_diamond:DNS

#### :small_orange_diamond:REST와 RESTful의 개념

#### :small_orange_diamond:소켓(Socket)이란
<!-- * 소켓(Socket)은 TCP/IP를 이용하는 API로 소프트웨어로 작성된 통신의 접속점이다. -->


#### :small_orange_diamond:Socket.io와 WebSocket의 차이

> - [https://d2.naver.com/helloworld/1336](https://d2.naver.com/helloworld/1336)

#### :small_orange_diamond:Frame, Packet, Segment, Datagram

---
## Reference
> - []()


## :house: [Home](https://github.com/Do-Hee/tech-interview)
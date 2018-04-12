# http_Actually_work
HTTP (Hyper Text Transfer Protocol)

## 프로토콜이란?

컴퓨터나 전자기기 통신장비등이 메세지를 주고 받는 양식과 규칙. 특수한 계층구조를 가지고 있다.
응용계층: 메세지, 데이터
표현계층: 메세지, 데이터
세션 계층: 메세지, 데이터
전송 계층: 세그먼트
네트워크 계층: 패킷, 데이터그램
데이터링크 계츠이 프레임
물리 계층: 비트


## http 프로토콜 스터디

간략한 구조 : 브라우저 주소창에 주소를 입력하게 되면 서버는 사이트정보를 사용자 브라우저로 보내서 사용자 브라우저가 사이트를 화면에 표현한다.
전송되는 정보는 미디어(오디오/비디오), 이미지, 텍스트, css, 자바스크립트, 폰트등이 있다. 형태는 패킷 형태로 전송된다.

이때 TCP/IP 계층 순서로 네트워크에 접근하게 된다.

### TCP/IP란?

(transmission control porotocol / internet protocol)

#### three-way handshake

TCP는 장치들 사이에 논리적인 접속을 성립(establish)하기 위하여 three-way handshake를 사용한다.
TCP 3 Way Handshake는 TCP/IP프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에
먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.

1. Client에서 Server에 연결 요청을 하기위해 SYN('synchronize sequence numbers') 데이터를 보낸다.

2. Server에서 해당 포트는 LISTEN(포트가 열린 상태로 연결 요청 대기 중)상태에서 SYN 데이터를 받고 SYN_RCV(SYN 대기상태)로 상태가 변경된다.
   요청을 정상적으로 받았다는 대답(ACK)과 Client도 포트를 열어달라는 SYN 을 같이 보낸다.
   
3. Client에서는 SYN+ACK 를 받고 ESTABLISHED(포트 연결 상태)로 상태를 변경하고 서버에 요청을 잘 받았다는 ACK 를 전송한다.
   ACK를 받은 서버는 상태가 ESTABLSHED(포트 연결 상태)로 변경된다.


#### 4-way Handshaking (세션 종료 하기 위한 과정)

1. Client에서 연결을 종료하겠다는 FIN플래그를 전송한다.


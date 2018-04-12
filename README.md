# http_Actually_work
HTTP (Hyper Text Transfer Protocol)

## 프로토콜이란?

컴퓨터나 전자기기 통신장비등이 메세지를 주고 받는 양식과 규칙. 특수한 계층구조를 가지고 있다.

### OSI 계층 구조
7. 응용계층: 메세지, 데이터              Protocol => HTTP, DNS, DHCP, FTP, SSH
6. 표현계층: 메세지, 데이터              Protocol => JPEG, MPEG
5. 세션 계층: 메세지, 데이터             Protocol => SSH 
4. 전송 계층: 세그먼트                  Protocol => TCP, UDP
3. 네트워크 계층: 패킷,데이터그램 (라우터)   Protocol => IP
2. 데이터링크 계층: 프레임(bit의 모음) (브리지, 스위치)
1. 물리 계층: 비트 (허브, 리피터)


## http 프로토콜

웹사이트가 클라이언트에서 열리는 과정
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
   요청을 정상적으로 받았다는 대답(ACK)과 Client도 포트를 열어달라는 SYN을 같이 보낸다.
   
3. Client에서는 SYN+ACK 를 받고 ESTABLISHED(포트 연결 상태)로 상태를 변경하고 서버에 요청을 잘 받았다는 ACK 를 전송한다.
   ACK를 받은 서버는 상태가 ESTABLSHED(포트 연결 상태)로 변경된다.


#### 4-way Handshaking (세션 종료 하기 위한 과정)

1. Client에서 연결을 종료하겠다는 FIN플래그를 전송한다. 그리고 FIN_WAIT_1로 대기한다.
2. server는 FIN플래그를 받아 해당 포트를 CLOSE_WAIT로 바꾸고 client에게 ACK를 보낸 며 연결된 app를 close한다. client는 FIN_WAIT_2로 대기한다.
3. app이 정상적으로 close되면 server는 FIN플래그를 client에 보내고 LAST_ACK가 된다.
4. FIN_WAIT_2에서 server의 FIN플래그를 받으면 TIME_WAIT가 되고 서버에 확인했다는 ACK를 보낸다. server는 최종 ACK를 받고 자신의 포트를 CLOSE로 닫는다.


### 핸드 쉐이크 끝나고...

4은 클라이언트에서 서버에 웹페이지를 요청한다.
5는 서버가 수락을 한다.
6부터는 나머지 정보를 패킷 형태로 전송된다..


### HTTP 프로토콜 과정과 구조

HTTP 프로토콜은 클라이언트가 request를 만들어 서버로 전송하고 서버는 request를 해석하여 response를 클라이언트에 보낸다.
HTTP 프로토콜의 데이터 형식은 크게 HEADER와 BODY로 구성되어있다. HEADER에는 서버가 인식할 수 있는 약속된 형식을 따라야함.


#### Request-header 구조

GET / HTTP/1.1 : HTTP전송 방법과 프로토콜 버전
Host: 요청하는 서버 주소 (api.github.com)
Origin: 요청하는 DNS (https://github.com)
User-Agent: OS/브라우저 정보 (Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36)
Accept: 클라이언트 이해 가능한 컨텐츠 타입 (*/*)
Accept-Language: 클라이언트 인식 언어 (en-US,en;q=0.9,ko;q=0.8)
Accept-Encoding: 클라이언트 인코딩 방법 (gzip, deflate, br)
Connection: 전송 완료후 접속 유지 정보 (keep-alive)
Upgrade-Insecure-Requests:신호를 보낼때 데이터 암호화 여부
Content-Type: 클라이언트에게 반환되어야하는 컨텐츠 유형 (application/json)
Content-Length: 본문크기 (964409)
Referer: 요청 직접하는 위치 (https://github.com/arusantimo/crytoCurrency)

#### Response-header 구조

Status: HTTP/1.1 200 ok : 프로토콜 버전과 응답상태
Access-Control-Allow-Origin: 서버에 타 사이트의 접근을 제한하는 방침 (*)
Cache-Control:  웹페이지 컨텐츠를 캐싱하지 않도록 설정 (no-cache)
Connection: 전송 완료후 접속 유지 정보 (keep-alive)
Content-Length:바이트 단위를 가지는 개체 본문의 크기를 나타냅니다. (5)
Content-Encoding: 미디어 타입을 압축한 방법 
Content-Type: 클라이언트에게 반환되어야하는 컨텐츠 유형 (application/json; charset=utf-8)
Date: 헤더가 만들어진 시간 (Thu, 12 Apr 2018 09:08:31 GMT)
ETag: 버전의 리소스를 식별하는 식별자
Keep-Alive: 연결에대한 타임아웃과 요청 최대 개수 정보
Last-Modified: 웹 시간을 가지고 있다 수정되었을때만 데이터 변경 ( 캐시연관 )
Server: 웹서버로 사용되는 프로그램 이름 (GitHub.com)
Set-Cookie: 쿠키 정보 
Transfer-Encoding: 인코딩 형식 지정
X-Frame-Options: frame/iframe/object 허용 여부 (deny)
Strict-Transport-Security: HTTP 대신 HTTPS만을 사용하여 통신해야한다고 웹사이트가 브라우저에 알리는 보안 기능. (max-age=31536000; includeSubdomains; preload)
Content-Security-Policy: 스크립트를 허용할 URL(신뢰할 수 있는 URL) 을 헤더에 설정하는 옵션보안 정책 (default-src 'none')
X-Content-Type-Options: (컨텐츠 스니핑을 하지 못하도록 설정) nosniff
X-XSS-Protection: 웹브라우저의 내장 XSS Filter를 사용하도록 하는 옵션 (1; mode=block)


#### 클라이언트의 처리과정
html 문서의 다운로드후 JS, CSS, IMAGE 파일등을 다운 받는다. 이러한 과정을 앞서 과정처럼 모두 처리하면 너무 오래걸리기 때문에
Keep-Alive를 이용해서 클라이언트 연결을 유지한다.






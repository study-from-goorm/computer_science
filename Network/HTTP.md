## HTTP(HyperText Transfer Protocol)
인터넷에서 데이터를 주고받을 수 있는 규약

### HTTP 동작
![](https://velog.velcdn.com/images/tme2685/post/f279b15e-70ee-4c8e-b2d7-b0902c02df07/image.png)

요청(request) -> 응답(response)

클라이언트와 서버의 분리 이유?

각자의 역할에 집중할 수 있기 때문

### HTTP 특징
* HTTP 메시지는 HTTP 서버와 HTTP 클라이언트에 의해 해석이 된다.
* TCP/ IP를 이용하는 응용 프로토콜이다.
* HTTP는 연결 상태를 유지하지 않는 비연결성 프로토콜이다. (이러한 단점을 해결하기 위해 Cookie와 Session이 등장하였다.)
* HTTP는 연결을 유지하지 않는 프로토콜이기 때문에 요청/응답 방식으로 동작한다.

### HTTP 무상태성
* 상태유지(stateful)
![](https://velog.velcdn.com/images/tme2685/post/82f6623a-ab44-47e8-aab8-ea820fed1f1b/image.png)
서버가 클라이언트의 상태를 보존한다.


* 무상태(stateless)
![](https://velog.velcdn.com/images/tme2685/post/60939115-64b0-4cde-a07b-a996a80ca8d9/image.png)
서버가 클라이언트의 상태를 보존하지 않는다.
>무상태 환경에선 회원 정보를 서버가 아닌 클라이언트가 토큰 형태로 들고 있으면서
>
>서버와 통신할때 실어 보내 인증하는 식이다.
>
>하지만 상태유지(Stateful)보다 데이터를 많이 사용한다는 단점이 있다.


### HTTP 비연결성
* 연결을 유지하는 모델
![](https://velog.velcdn.com/images/tme2685/post/fc6f1c23-b076-45f8-993d-9a65cd467ad6/image.png)

연결을 유지한다면, 서버와 클라이언트의 연결은 서로의 네트워킹 요청이 없더라도 계속해서 유지된다.

자원이 계속해서 사용된다. 


* 연결을 유지하지 않는 모델
![](https://velog.velcdn.com/images/tme2685/post/3defb1f0-f08c-46bc-94b3-1cf606164d8f/image.png)

연결을 유지하지 않는다면, 서버의 자원을 효율적으로 사용할 수 있다.

그러나 연결을 계속 끊는다는 것은 TCP/IP 연결을 매번 새롭게 맺어야 하기 위해서 TCP 3 way handshake를 매번 해야한다.

이러한 문제는 지금 HTTP 지속 연결(Persistent Connections)로 문제 해결하고 있다.


## Request

### Request 종류
* GET : 자료를 **요청**할 때 사용
* POST : 자료의 **생성**을 요청할 때 사용
* PUT : 자료의 **수정**을 요청할 때 사용
* DELETE : 자료의 **삭제**를 요청할 때 사용

### Request 메세지
```
GET https://velog.io/@tme2685 HTTP/1.1								// 시작줄
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) ...			               // 헤더
Upgrade-Insecure-Requests: 1

...												///본문
```
첫 줄에 http method, 사이트 주소, http버전 순으로 나와있다.

둘째줄부터 헤더, 한줄띄우고 본문이 시작된다.


## Response

### Status Code
* 1XX (정보) : 요청을 받았으며 작업을 계속한다.
* 2XX (성공) : 요청이 성공적으로 처리되었다.
* 3XX (리다이렉션 완료) : 요청 완료를 위해 추가적으로 작업이 필요하다.
* 4XX (클라이언트 오류) : 클라이언트에 오류가 있음을 나타낸다.
* 5XX (서버 오류) : 서버에 오류가 있음을 나타낸다.

### Response 메세지
```
HTTP/1.1 200 OK								// 시작줄
Connection: keep-alive					                // 헤더
Content-Encoding: gzip												 
Content-Length: 35653
Content-Type: text/html;

<!DOCTYPE html><html lang="ko" data-reactroot=""><head><title...	// 본문
```
첫 줄에 http버전, status code, message 순으로 나와있다.

둘째줄부터 헤더, 한줄띄우고 본문이 시작된다.

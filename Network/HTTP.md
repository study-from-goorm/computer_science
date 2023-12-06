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

---
## HTTP/1.0
- HTTP/1.0은 수명이 짧은 연결, HTTP 요청은 자체 요청에서 완료
- 각 요청당 TCP Handshakerk 발생되며 한 연결당 하나의 요청을 처리하도록 설계
- 문제점 :
    - 연결할 때마다 TCP 연결로 인해 RTT의 증가

![](https://velog.velcdn.com/images/k-minsik/post/8462fa9f-9c21-42db-9c65-8cac388b071c/image.png)

> RTT(Round Trip Time, 왕복 지연시간) : 신호를 전송하고 해당 신호의 수신확인이 걸린 시간을 더한 값이자 어떤 메시지가 두 장치 사이를 왕복하는데 걸린 시간

---

## HTTP/1.1
- HTTP/1.0의 단점을 보완한 프로토콜, 크게 3가지 차이점
### 1. keep-alive default
- TCP 연결을 매 요청마다 하지 않고, 한번 해놓고 계속해서 요청을 주고 받을 수 있음
- 이는 keep-alive 옵션을 기본옵션으로 하면서 가능해짐

![](https://velog.velcdn.com/images/k-minsik/post/bb784421-eaa3-4a69-ba49-45e322bfb79d/image.png)

> keep-alive header :
> 	TCP연결을 유지하는 것을 알려주는 헤더로 연결유지시간인 timeout과 최대 요청수 max를 정함

    
### 2. 호스트 헤더
- HTTP/1.0은 서버가 하나의 호스트만 상대한다고 가정하기에 호스트 헤더를 포함하지 않음
    - 이 때문에 HTTP/1.0은 하나의 IP에 하나의 호스트만 가질 수 있었음
- 서버는 여러개의 호스트를 가질 수 있기에 HTTP/1.1에서는 요청시 호스트 헤더를 포함하도록 함

### 3. 대역폭 최적화
- HTTP/1.0은 파일은 다운로드 받다 연결이 끊기면 이어서 다운로드하는 것이 불가능
	> 10KB 파일을 다운로드 할 때, 5KB 까지 받고 나중에 다시 이어받기 불가능
- HTTP/1.1에서는 `Range:bytes=5000-` 라는 헤더를 추가해서 다운로드 재개 요청을 할 수 있음

### 4. 그 외 요청을 줄이기 위한 기술
- 이미지 스프라이트 (image sprite)
    - 수 많은 이미지를 하나의 이미지로 만들어 다운받고, 이를 통해 많은 이미지를 다운 받은 것 같은 효과
- 코드 압축
    - 코드를 압축해서 서빙
- 이미지 Base64 인코딩
    - 이미지 파일을 64진법으로 이루어진 문자열로 인코딩해 이미지 서버에 대한 HTTP요청을 없앰
    - 인코딩시 파일크기가 평균적으로 약 37% 커지는 단점

### 5. HTTP/1.1의 고질적인 문제
- 무거운 헤더
- HOL(Head Of Line Blocking) : 네트워크에서 같은 큐에 있는 패킷이 그 첫번째 패킷에 의해 지연될 때 발생하는 성능 저하 현상


---

## HTTP/2
- 2009년 구글이 HTTP/1.1의 한계를 극복하기 위해 SPDY 프로토콜 개발
- 2015년 SPDY 기반 HTTP/2 프로토콜 개발

### 1. 바이너리 포맷 계층
- 애플리케이션 계층과 전송 계층 사이에 바이너리 포맷 계층을 추가
- HTTP 1.0은 일반 텍스트 메세지를 전송하고 줄바꿈으로 데이터를 나눴다면 2.0은 0/1로 이뤄진 바이너리 데이터로 변경하고 더 작은 메세지가 프레임으로 캡슐화 돼서 전송

![](https://velog.velcdn.com/images/k-minsik/post/f1701c6c-1fc7-45f4-a893-15a87b73687c/image.png)

### 2. 멀티 플렉싱
- 단일 TCP연결의 여러 스트림에서 여러 HTTP 요청과 응답을 비동기적으로 보낼 수 있음, 이를 통해 HOL을 해결
- 2.0에서는 리소스를 작은 프레임을 나누고 이를 스트림으로 프레임을 전달
    - 각각의 프레임은 스트림ID, 해당 크기를 나타내는 프레임이 추가
    - 때문에 작게 나눠서 다운로드 되더라도 결과적으로 응답데이터는 올바른 순서로 재조립 가능

![](https://velog.velcdn.com/images/k-minsik/post/d001de93-cf9c-4785-abd8-087fc2f6367f/image.png)


### 3. 서버 푸시
- 서버가 리소스를 클라이언트에 푸시 가능
- html을 요청했을 때, css가 포함되어야한다면 서버가 알아서 css도 같이 보내줌

![](https://velog.velcdn.com/images/k-minsik/post/501a01a6-42fd-45aa-a1e3-d455d7b0612f/image.png)

### 4. 헤더 압축
- HTTP/1.1에는 무거운 헤더가 있음
- 2.0에서는 중복되는 헤더를 제외하고 공통 필드로 헤더를 재구성하며 중복되지 않은 헤더값은 허프만 인코딩 압축 방법으로 압축해 전송
> 허프만 인코딩 : 문자열을 문자 단위로 쪼개 빈도수를 세어 빈도가 높은 정보는 적은 비트수를 사용해 표현하고, 빈도가 낮은 정보는 비트 수를 많이 사용하여 전체 데이터 표현에 필요한 비트양을 줄이는 알고리즘
### 5. 우선 순위
- 서버에서 원하는 순서대로 우선순위를 정해 리소스를 전달할 수 있음

---

## HTTP/3
- HTTP/2는 여전히 TCP를 사용하므로 초기 연결에 대한 RTT로 인한 지연시간이 존재
- HTTP/3은 QUIC라는 계층 위에서 돌아가며, TCP기반이 아닌 UDP 기반으로 돌아가며, HTTP/2에서 장점이었던 멀티플렉싱 등을 가지고 있으며 초기 연결 설정시 지연시간 감소라는 대표적 특성을 지님
![](https://velog.velcdn.com/images/k-minsik/post/08370314-cf97-4a35-8486-b8c8901271b8/image.png)
>QUIC(Quick UDP Internet Connections) : 구글에 의해 개발된, 새로운 인터넷 전송 프로토콜

- HTTP/2는 3-RTT가 필요했지만, HTTP/3은 QUIC로 인해 1-RTT만 필요하다는 장점을 지님
- HTTP/2의 경우 TCP 3-handshake 1-RTT, TLS1.2-handshake 2-RTT가 필요
- HTTP/3의 경우 TLS1.3-handshake로 한번에 클라이언트와 서버간의 연결로 1-RTT, 암호화 통신 모두 다 구축
![](https://velog.velcdn.com/images/k-minsik/post/3ae30bbd-f8f4-4a05-a66d-bc0d185be50c/image.png)


- 전송된 패킷이 손실 되었다면 수신측에서 에러를 검출하고 수정하는 방식이며 열악한 네트워크 환경에서도 낮은 패킷 손실률을 자랑하는 순방향 오류 수정 메커니즘(FEC, Forward Error Correction)이라는 특징을 지님





> 출처 및 참고 : https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EB%A9%B4%EC%A0%91-cs-%ED%8A%B9%EA%B0%95#
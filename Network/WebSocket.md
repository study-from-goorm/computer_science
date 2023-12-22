# WebSocket (웹소켓)

브라우저와 서버 간 양방향, 실시간 통신을 지원하는 프로토콜
- OSI 참조 모델 7계층에 위치하며 TCP에 의존
- HTML5 표준 기술

<br/>

### 특징

- **전이중통신** (양방향 통신, Full-Duplex Communication) 지원
    - 서버와 클라이언트는 각 주체가 요청, 응답 없이 능동적으로 메시지를 보낼 수 있다.
- **실시간 데이터 전송**  
    → 실시간 채팅, 주식 트레이딩 등 데이터 교환이 지속적으로 이뤄져야 하는 서비스에 적합  

<br/>

## 웹소켓 이전의 실시간 & 양방향 통신 방식
### 1. HTTP Polling (Short Polling)
- 일정한 주기에 따라 반복적으로 서버에 Request를 보내는 방법
- setTimeout, setInterval 등을 사용
    <br/>
![short-polling](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*YiWBVCm1Ge7LklMsOcZi2g.png)

    #### 한계
- 받을 응답이 없는 상황에서도 불필요한 요청과 네트워크 연결을 생성해 서버의 부담이 증가한다.
- 클라이언트가 많아졌을 경우 또한 서버의 부담이 급증한다.
- 사실상 실시간이라고 보기 어렵다. (일정 주기마다 요청)
- <u>HTTP 오버헤드</u>가 발생한다.  
    : Request, Response 헤더 정보가 불필요하게 크기 때문에 오히려 데이터량이나 처리 시간이 증가하는 현상  
<br/>

### 2. HTTP Long Polling
- 서버 측에서 긴 시간 접속을 열어두는 방식
- 일정 주기마다 HTTP 요청을 보내되, 서버에서 이벤트가 발생해 응답이 제공되거나 timeout이 발생할 때까지 연결이 유지된 상태로 기다린다.
- Short Polling에 비해 낮은 HTTP 오버헤드 발생률, 그러나 여전히 헤더가 불필요하게 크다.
    <br/>
![long-polling](https://miro.medium.com/v2/resize:fit:720/format:webp/1*JyLiDASqEXBs3ZjvldUrEQ.png)

    #### 한계
- 실시간 채팅 구현에 비효율적 : 만약 사용자가 채팅을 적게 하는 경우에도 Long polling은 timeout 이후 계속해서 주기적으로 연결을 진행함.
- 클라이언트로 응답하는 이벤트들의 시간 간격이 짧은 경우 polling 방식과 차이가 없음
- 다수의 클라이언트에게 동시에 이벤트가 발생될 경우, 다수의 클라이언트가 동시에 서버로 접속을 시도하며 서버 부담이 급증함.  
<br/>

### 3. Streaming
- 서버 이벤트 발생 시 응답을 전송하되, 연결을 종료하지 않고 유지하는 방식
- Polling 방식에 비해 불필요한 재요청이 줄어들어 효율적
- 연결 시간이 길어질수록 연결 유효성 관리에 대한 부담이 발생.  
<br/>

![streaming](https://miro.medium.com/v2/resize:fit:720/format:webp/1*iuCFQozwVymbDfe95GqeuQ.png)

<br/>

---

## Web Socket 동작 방식
![websocket](https://blog.kakaocdn.net/dn/cmqBIY/btqKBOBCLJS/yKS7Ci7bq5DTki4DuJRlYk/img.png)

### 1. Opening Handshake
- 예시 : ZEP 구름 유니버스 채팅 기능
```
// Request Header

GET /hub/chat HTTP/1.1
Host: sts-live-zep-webchatserver-0.zep.us
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: ...
Sec-WebSocket-Extensions: permessage-deflate; client_max_window_bits
Sec-WebSocket-Version: 13
Origin: https://zep.us
```

> * **`Upgrade`**: 프로토콜 전환을 위해 사용하는 헤더, 웹소켓 요청시 반드시 websocket이라는 값을 갖는다.
> * **`Connection`**: 현재 전송이 완료된 후 네트워크 접속을 유지할 것인지에 대한 정보. 웹소켓 요청시 항상 Upgrade 값을 갖는다.  
>   - Upgrade와 Connection 헤더 모두 다른 값을 갖는 경우 cross-protocol attack으로 간주하여 웹소켓 접속을 중지시킨다. 
> * **`Sec-WebSocket-Key`**: 유효한 요청인지 확인하기 위한 키값
> * **`Sec-WebSocket-Protocol`**: 사용하고자 하는 하나 이상의 웹소켓 프로토콜 지정 (선택)
> * **`Sec-WebSocket-Extensions`**: 웹소켓 프로토콜 기능 확장시 (브라우저에 의해 자동 생성됨)
> * **`Sec-WebSocket-Version`**: 클라이언트가 사용하고자 하는 웹소켓 프로토콜 버전  

<br/>

- 클라이언트에서 핸드쉐이크 요청(HTTP Upgrade)을 전송하고, 이에 대해 핸드셰이크 응답을 받는데, 이 때 응답코드는 **`101 Switching Protocols`** 이다.  

<br/>

```
101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: ...
```  

> * **`Sec-WebSocket-Accept`**: 요청 헤더의 Sec-WebSocket-Key에 유니크 아이디를 더해 SHA-1로 해싱 및 base64로 인코딩한 결과  
=> 웹소켓 연결 개시를 알림

<br/>

### 2. Data Transfer
- 핸드쉐이크를 통해 ws 또는 wss 프로토콜로 전환해 웹소켓 연결이 수립되면 데이터 전송 파트가 진행된다.
- 데이터 전송 단위 : 메시지 (하나 이상의 프레임이 모여 구성됨)
<br/>

### 3. Closing Handshake
- 클라이언트, 서버 모두 연결 종료를 위한 컨트롤 프레임을 전송할 수 있다.
- 한쪽에서 Closing Handshake를 시작하라는 컨트롤 프레임을 전송하면, 이에 대한 응답으로 Close 프레임을 전송하고 웹소켓 연결을 종료한다.
- 연결 종료 이후 수신되는 모든 추가 데이터는 버려진다.  

<br/>

---
## Web Socket 장단점, 사용 예시

### 장점
- 적은 오버헤드
- 하나의 Connection만으로 데이터를 송수신할 수 있음
- 기존 HTTP 프로토콜은 요청한 클라이언트에게만 응답이 가능했으나, ws프로토콜을 통해 서버에서는 웹소켓 포트에 접속해있는 모든 클라이언트에게 이벤트 방식으로 응답할 수 있다.
- 최초 접속은 HTTP 요청으로 이뤄짐 : 기존 80, 443포트로 접속하므로 방화벽을 별도로 열지 않고 양방향 통신이 가능하며 CORS나 인증 등의 과정을 기존과 동일하게 가져갈 수 있다.

### 단점
- 프로그램 구현 시 복잡성
    - 웹소켓은 Stateful 프로토콜이기 때문에 비정상적으로 연결이 끊겼을 경우에 대한 적절한 대응이 필요하다.
- 서버와 클라이언트 연결을 유지하므로 비용 발생
- 오래된 버전의 웹 브라우저에서 지원하지 않는다.
    - **Socket.io** : 브라우저에 상관 없이 실시간 웹을 구현할 수 있는 Node.js 기반 WebSocket 라이브러리


### 사용 예시
- SNS 어플리케이션
- 멀티플레이어 게임
- 구글 Docs, Notion처럼 여러 명이 동시 접속 및 수정하는 서비스
- 증권 거래 정보 서비스
- 스포츠 업데이트 정보 서비스
- 화상 채팅
- 위치 기반 서비스
- 온라인 교육 서비스

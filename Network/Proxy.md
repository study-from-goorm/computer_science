## Proxy
![](https://velog.velcdn.com/images/tme2685/post/73250d90-70f9-4d4c-8b74-754e66f99875/image.png)

Spring Proxy, Proxy 패턴, Proxy Server 등 여기저기에서 들어본 표현이다.

이중 오늘 알아볼 것은 Proxy Server이다.

### Proxy Server
프록시 서버는 클라이언트와 서버 사이에서 중개자 역할을 하는 서버이다.

이 서버는 클라이언트의 요청을 받아서 서버에 전달하고, 서버의 응답을 다시 클라이언트에게 전달한다.


## Forward Proxy

일반적으로 말하는 프록시

ex) 

인터넷 속도를 향상시키기 위해 프록시 서버 설정

외국에서 접속하기 위해 프록시 설정

IP추적을 방지하기 위해 프록시 설정

<img width="737" alt="스크린샷 2023-11-30 오후 4 10 46" src="https://github.com/Seungmok1/frontend-board-project/assets/103080705/4d52a727-d081-4462-b3f9-74170096fc72">

### 특징
1. 캐싱
클라이언트가 요청한 내용을 캐싱한다.

* 전송시간을 절약한다.
* 불필요한 외부 전송을 줄여준다.
* 외부 요청을 감소시켜 네트워크 병목 현상을 방지한다.

2. 익명성
클라이언트가 보낸 요청을 숨겨준다.

우리가 요청을 했지만 마치 Forward Proxy가 요청한 것처럼 서버에게 전달한다.

서버가 받은 요청 IP는 프록시의 IP이다.

4. 웹 콘텐츠 필터링 및 접근 제어
서버에서 받은 응답이 적절하지 않을 때 대체 응답을 클라이언트에게 돌려준다.


## Reverse Proxy
<img width="744" alt="스크린샷 2023-11-30 오후 4 11 03" src="https://github.com/Seungmok1/frontend-board-project/assets/103080705/3a708fdf-3b1d-4326-95ed-394c171de3ff">

### 특징
1. 캐싱
클라이언트가 요청한 내용을 캐싱한다.(포워드 프록시와 동일)

2. 보안
서버 정보를 클라이언트로부터 숨긴다.
클라이언트는 서버를 직접 알지 못하고 리버스 프록시를 실제 서버라고 생각하고 요청하기 때문에 서버의 IP가 노출되지 않는다.

3. SSL 중앙화 관리

<img width="723" alt="스크린샷 2023-11-30 오후 4 11 13" src="https://github.com/Seungmok1/frontend-board-project/assets/103080705/de9d57f3-7141-48f2-a8e1-dc2a7091e3c5">

4. Load Balancing
해야할 작업을 나누어 여러 대의 서버가 분산 처리할 수 있도록 부하를 분산시켜준다.

### Load Balacer가 나온 배경
우리가 배포한 서비스가 알려져서 사용자가 점차 늘면 부하가 증가할 것이다. 이 과정이 계속 된다면 서버에 한계가 온다.

해결 방안

1. Scale Up
   
서버의 하드웨어 성능을 높이는 것 -> 비용이 많이 들고 한계가 있다.

<img width="611" alt="스크린샷 2023-11-30 오후 4 05 40" src="https://github.com/Seungmok1/frontend-board-project/assets/103080705/9e4a5b07-4bed-473a-abff-7d7d4fdaa3aa">

2. Scale out 
서버의 수를 늘려 여러 대의 서버가 나누어 일하는 것
클라이언트와 여러 대의 서버 사이에 Load Balancer를 두어 부하를 분산을 한다.

<img width="797" alt="스크린샷 2023-11-30 오후 4 09 54" src="https://github.com/Seungmok1/frontend-board-project/assets/103080705/a4782e9c-1169-4d87-92ac-a8d97669a8ac">

L4 : Transport Layer에서 Load Balancing

여러 클라이언트에서 요청하면 여러 대의 서버에게 나눠준다.

L7 : Application Layer에서 Load Balancing

https://velog.io/@tme2685 로 접근 시

https://velog.io/@tme2685/DNS-ARP 와 https://velog.io/@tme2685/Proxy 로 구분해서 담당 서버로 나눠준다.


### 포워드 프록시 vs 리버스 프록시
이 두 프록시 서버의 주요 차이점은 "서비스 대상"에 있다.

포워드 프록시는 내부 사용자를 위해 서비스하며, 사용자의 요청을 외부로 전달한다. 

반면, 리버스 프록시는 외부 요청을 받아 내부 서버로 전달하며, 주로 서버 측에서 사용된다. 

간단히 말해서, 포워드 프록시는 사용자 측에 초점을 맞추고, 리버스 프록시는 서버 측에 초점을 맞춘다.

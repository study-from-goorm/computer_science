동기, 비동기, 블로킹, 논블로킹은 프로그램이 시스템 리소스와 상호 작용하는 방식이다.

I/O 작업을 수행하거나, 네트워크 요청을 만들거나, 장시간 실행되는 계산을 수행할 때 사용된다.

### 동기(Synchronous)와 비동기(Asynchronous)
![](https://velog.velcdn.com/images/tme2685/post/bf0c46f1-23d5-403b-981c-fd410a1b7046/image.png)


- 동기
  
프로그램 실행이 다음 작업으로 넘어가기 전에 해당 작업이 완료될 때까지 기다린다.

디스크에서 파일을 읽고 내용을 반환하는 함수는 파일 전체를 읽을 때까지 반환하지 않고 기다린다.

호출한 함수는 호출된 함수의 상태를 확인한다.

![](https://velog.velcdn.com/images/tme2685/post/bbddcb9d-3d8f-451a-9b38-e42af851864b/image.png)
- 비동기
  
프로그램이 작업을 시작하고 작업이 완료되기를 기다리지 않고 다음 작업이 시작한다.

비동기 파일 읽기에서 함수는 즉시 반환되고, 파일의 내용은 사용 가능해지면 콜백 함수에 의해 처리된다.

### 블로킹(Block)과 논블로킹(Non-Blocking)
![](https://velog.velcdn.com/images/tme2685/post/9038c388-6ae6-4612-822a-1f298670978a/image.png)
- 블로킹
  
블로킹 작업에서는 특정 작업이 완료될 때까지 프로그램 실행이 중단된다.

일반적으로 동기처리에서 사용된다. 

제어권이 호출된 함수에게로 넘어간다.

- 논블로킹
  
논블로킹 작업은 작업이 완료될 때까지 기다리지 않고 실행을 계속할 수 있게 한다.

비동기 프로그래밍 모델에서 자주 사용된다.

제어권을 바로 돌려준다.

논블로킹 I/O를 사용하면 시스템은 I/O 작업이 완료되기를 기다리는 동안 다른 작업을 처리할 수 있으므로 자원 사용을 최적화할 수 있다.

---

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fda50Yz%2Fbtq0Dsje4ZV%2FlGe8H8nZgdBdgFvo7IczS0%2Fimg.png)

- 동기 & 블로킹
   많은 표준 라이브러리의 전통적인 I/O에 사용된다.
  
예를 들어, 파일을 읽어오는 메서드를 호출할 때 데이터가 읽힐 때까지 메서드 호출이 블로킹된다.

ex) 콘솔 창 입력

- 동기 & 논블로킹
 프로그램이 리소스를 사용 가능할 때까지 계속 확인하지만 대기하는 동안 다른 작업을 수행할 수 있는 바쁜 대기 루프에서 볼 수 있다.

ex) 파일 다운로드 중 웹 서핑

- 비동기 & 블로킹
   동기 & 블로킹과 성능적으로 차이가 없기에 잘 사용되지 않는다.
  
ex) Node.js + MySQL

- 비동기 & 논블로킹
   고성능 웹 서버 및 데이터베이스의 현대적인 I/O 작업에 사용한다.
  
   다른 작업을 기다리지 않고 자신의 작업을 처리하고, 다른 작업이 완료되면 콜백이 호출된다.
  
ex) 브라우저


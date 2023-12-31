# 프로세스와 스레드

## 1️⃣ 프로세스 (Process)

### 👉🏻 컴퓨터의 메모리에 올라와 실행되고 있는 프로그램, 작업(task)와 같은 의미

- 프로그램이 메모리에 올라가면 프로세스가 되는 인스턴스화가 일어나고, CPU의 스케쥴링 대상이 됨
- 싱글스레드 프로세스, 멀티스레드 프로세스로 나뉨

> 프로세스 제어 블록(Process Control Block, PCB) :   
> - PCB 는 특정 프로세스에 대한 중요한 정보를 저장 하고 있는 운영체제의 자료구조이다. 운영체제는 프로세스를 관리하기 위해 프로세스의 생성과 동시에 고유한 PCB 를 생성 한다. 프로세스는 CPU 를 할당받아 작업을 처리하다가도 프로세스 전환이 발생하면 진행하던 작업을 저장하고 CPU 를 반환해야 하는데, 이때 작업의 진행 상황을 모두 PCB 에 저장하게 된다. 그리고 다시 CPU 를 할당받게 되면 PCB 에 저장되어있던 내용을 불러와 이전에 종료됐던 시점부터 다시 작업을 수행한다.



### 👉🏻 프로세스의 데이터 구조
<p align="center"><img src="./assets/processDS.png" alt="mvc_model1"/></p>



## 2️⃣ 스레드 (Thread)

### 👉🏻 프로세스 내에서 실행되는 가장 작은 흐름의 단위

- 스레드 ID, 프로그램 카운터(PC), 레지스터 집합 그리고 스택으로 구성
- 프로세스는 여러개의 스레드를 가질수 있음
- 메모리 영역을 각각 생성하는 프로세스와는 달리 스레드는 코드, 데이터, 힙은 스레드끼리 서로 공유, 스택 영역은 각각 생성됨.

#### 🤔 스택을 스레드마다 독립적으로 할당하는 이유

- 스택은 함수 호출 시 전달되는 인자, 되돌아갈 주소값 및 함수 내에서 선언하는 변수 등을 저장하기 위해 사용되는 메모리 공간이므로 스택 메모리 공간이 독립적이라는 것은 독립적인 함수 호출이 가능하다는 것이고 이는 독립적인 실행 흐름이 추가되는 것이다. 따라서 스레드의 정의에 따라 독립적인 실행 흐름을 추가하기 위한 최소 조건으로 독립된 스택을 할당한다.

## 3️⃣ 멀티프로세싱 & 멀티스레딩

### 🖥️ 멀티프로세싱

#### 여러 개의 프로세스를 사용하여 여러 작업을 동시에 처리하는 기술, 프로세스는 독립적인 메모리 영역과 시스템 리소스를 가지고 있음

#### 👍🏻 장점
- 안정성 : 하나의 프로세스에 문제가 생겨도 다른 프로세스에 영향을 미치지 않음
- 보안 : 각 프로세스는 자신의 메모리 공간을 가지므로, 하나의 프로세스가 다른 프로세스의 메모리에 접근하는 것이 기본적으로 제한
- CPU 활용 : 멀티코어 또는 다중 프로세서 시스템에서, 멀티프로세싱은 여러 CPU/코어에서 프로세스를 병렬로 실행할 수 있게 해서 자원을 효율적으로 활용할 수 있습니다.

#### 👎🏻 단점
- 자원 소비 : 각 프로세스는 독립적인 메모리 공간과 시스템 리소스를 가지고 있기 때문에, 많은 양의 시스템 리소스를 소비할 수 있음
- 통신 복잡성 : 프로세스 간 통신(IPC)을 통해 수행되며, 이는 상대적으로 복잡하고 큰 비용을 지불 함

> IPC(Inter-Process Communication) :
> - 프로세서스끼리 데이터를 주고받고 공유데이터를 관리하는 메커니즘. 공유메모리, 파일, 소켓, 파이프, 메세지 큐가 있음  
>   - ex) 서버와 HTTP 통신해서 html 등의 파일을 가져오는 것도 IPC 라고 함 

### 🖥️ 멀티스레딩

#### 하나의 프로세스 내에서 여러 스레드를 사용하ㅕ 작업을 동시에 처리하는 기술, 모든 스레드는 프로세스의 메모리 영역을 공유

#### 👍🏻 장점
- 자원 공유 : 스레드들은 메모리와 파일 등의 리소스를 공유하기 때문에, 시스템 리소스 요구량이 상대적으로 낮음
- 빠른 컨텍스트 스위칭 : 스레드 간의 컨텍스트 스위칭은 프로세스 간의 스위칭보다 훨씬 빠르며, 자원을 덜 사용함.
- 향상된 응답성 : 한 스레드가 블록되거나 긴 작업을 처리하는 동안, 프로세스는 다른 스레드를 계속 실행할 수 있어 응용 프로그램의 응답성이 향상됨
  
#### 👎🏻 단점
- 동기화 : 스레드들이 리소스를 공유하기 때문에, 동기화 문제를 처리해야 함
- 안정성 문제 : 한 스레드에서 문제가 발생하면 전체 프로세스에 영향을 줄수 있음

---
## ⭐️ 프로세스 vs 스레드
|  |프로세스|스레드|
|:---:|:---:|:---:|
|메모리|각 프로세스 마다 할당(코드, 데이터, 스택, 힙)|프로세스 내 스택을 제외한 메모리 영역을 공유|
|공유|서로 격리되어 있어 프로세스간 IPC 통신을 해야함|스레드는 격리 되어있지 않아 그냥 통신할 수 있어 프로세스보다 빠름|
|비용|생성과 종료에 많은 시간이듬(메모리)| 프로세스보다 적음 |
|멀티|프로세스간 영향을 끼치지 않음|한 스레드가 다른 스레드에게 영향을 미쳐 프로세스에도 영향이 갈수 있음|


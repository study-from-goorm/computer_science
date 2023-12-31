# 6장 메모리와 캐시 메모리
## 1. RAM 특징과 종류
### RAM
> RAM 특 : 저장한 명령어와 데아터가 모두 날아감 => 휘발성 저장 장치
> + 비휘발성 저장 장치 : 전원이 꺼져도 저장된 내용이 유지됨
#### 1) DRAM(Dynamic RAM)
##### 정의
+ 저장된 데이터가 점차 사라지는 RAM
##### 장점
+ 소비전력이 낮음
+ 쌈
+ 집적도가 높아 대용량으로 용이
> 집적도 : 더 작고 뺵빽하게 만들 수 있다
##### 단점
+ 일정 주기로 데이터를 재활성화 해야함
#### 2) SRAM(Static RAM)
##### 정의
+ 저장된데이터가 변하지 않는 RAM
+ 보통 캐시 메모리에서 사용
##### 장점
+ 속도가 빠름
+ 데이터 재활성화 필요 없음
##### 단점
+ 집적도가 낮음
+ 소비 전력 큼
+ 비쌈

| 구분      | DRAM            | SRAM        |
| --------- | --------------- | ----------- |
| 재충전    | 필요            | 불필요      |
| 속도      | 느림            | 빠름        |
| 가격      | 저렴            | 비쌈        |
| 집적도    | 높음            | 낮음        |
| 소비 전력 | 적음            | 높음        |
| 사용 용도 | 주기억장치(RAM) | 캐시 메모리 |

#### SDRAM(Synchronous Dynamic RAM)
##### 정의
+ 동기화된 발전된 형태의 DRAM
+ 클럭타이밍에 맞춰 CPU.와 정보를 주고받을 수 있음
##### 장점
+ 속도가 빠름
+ 데이터 재활성화 필요 없음
##### 단점
+ 집적도가 낮음
+ 소비 전력 큼
+ 비쌈
#### 3) DDR SDRAM
##### 정의
+ 최근 가장 흔히 쓰는 RAM
+ 대역폭을 넓혀 속도를 빠르게 만든 SDRAM

> 대역폭 : 데이터를 주고받는 길의 너비
##### 장점
+ 속도가 빠름
+ 데이터 재활성화 필요 없음
##### 단점
+ 집적도가 낮음
+ 소비 전력 큼
+ 비쌈

## 2. 메모리의 주소 공간   
### 1>주소
#### 1) 물리주소
##### 정의
- 메모리가 사용하는 주소
- 정보가 실제로 저장된 하드웨어상의 주소
#### 2) 논리주소
- CPU와 실행 중인 프로그램이 사용하는 주소
- 실행중인 프로그램 각각에게 부여된 0번지부터 시작되는 주소
- 물리주소와 얼마나 떨어져있는지 표현하는 주소라고 생각
![](https://i.imgur.com/gjJm2qR.png)

> CPU와 메모리가 상호작용하려면 논리주소 / 물리주소간의 변환이 이루어져야함
> 이를 해결해주는 것이 **MMU**임

### 2> MMU
##### 정의
- 논리주소와 물리 주소 간의 변환을 해주는 장치
- CPU가 발생 시킨 논리주소에 **베이스 레지스터** 값을 더하여 물리주소로 변환

![](https://i.imgur.com/Tcw2U9q.png)

**베이스 레지스터** : 프로그램의 가장 첫 물리 주소를 저장하는 곳
### 3> 메모리 보호 기법
> 메모장 프로그램의 물리주소가 1000~1999번지에 있다고가정
> 
> 인터넷 브라우저는 2000~2999번지
> 
> 게임은 3000~3999번지에 있다고 가정

> CPU가 인터넷브라우저 1100번지에 데이터를 삭제하라고할 때 문제가 생김 
> 
> ![](https://i.imgur.com/nRACz5U.png)


#### 1) 한계 레지스터
##### 정의
- 다른 프로그램의 영역을 침범할 수 있는 문제를 보호하는 레지스터
##### 특징
- 논리 주소의 최대 크기를 저장
- 베이스 값 <= 프로그램 물리 주소 범위 < 베이스 + 한계 레지스터값
![](https://i.imgur.com/VInICiH.png)


## 3. 캐시 메모리
### 캐시메모리란
> - CPU는 메모리를 빈번하게 사용함
> - 하지만 메모리에 접근하는 시간이 느림
> -->이를 극복하기위한 저장장치임

### 저장 장치 계증구조
##### 정의
- CPU에 얼마나 가까운지 계층적으로 나눈 구조
	- 저장 장치는 다음과 같은 명제를 따름
	- 1. CPU와 가까울수록 저장장치는 빠르다
	- 2. 속도가 빠를수록 저장용량이 작고 비싸다
![](https://i.imgur.com/DInXe4w.png)


### 캐시메모리
##### 정의
- CPU와 메모리 사이에 위치함
- 레지스터보다 용량이 크고 메모리보다 빠름
- SRAM기반 저장장치
- 코어와 가까운 순으로 L1, L2, L3캐시가 있음
#### 1) L1 캐시
- CPU코어 내부에 위치
- 가장 빠르고 비쌈
#### 2) L2 캐시
- CPU코어 내부에 위치
- 중간속도 중간 가격 중간 용량
#### 3) L3 캐시
- CPU코어 외부에 위치
- 가장 느리고 싸며 저장용량이 큼

![](https://i.imgur.com/TRRpZGY.png)


> **분리형 캐시**
> L1의 속도를 빠르게 하기위 위해 명령어 Or 데이터만을 저장하는 각각의 캐시로 분리하는 것

![](https://i.imgur.com/lfhO0YL.png)

### 참조 지역성의 원리

- **캐시 히트** : 캐시 메모리 내 데이터가 CPU에서 활용될 경우

- **캐시 미스** : 캐시 메모리가 예측을 틀려 메모리에서 필요한 데이터를 직접가져와야하는 경우

- **캐시 적중률** : 캐시가 히트되는 비율 -> (캐시 히트 횟수 / (캐시히트 + 캐시미스))
##### 정의
- CPU가 메모리에 접근할 때의 주된 경향을 바탕으로 만들어진 원리

##### 1. 시간 지역성
- **최근에 접근**한 메모리 공간에 다시 접근하려는 경향
```c
#include<stdio.h>

int main(void){
	int num = 2;
	for(int i = 1; i <= 9; i++){
		printf("%d X %d = %d\n", num, i, num * i*)
	}
	return 0;
}
```
> 위 코드에 구구단을 출력하는 과정에서 num와 i가 여러번 사용됨
##### 2. 공간 지역성
- **접근한 메모리 공간 근처**를 접근하려는 경향

- 워드 프로세서 프그램을 실행할 때는 워드 프로세서 프로그램이 모여있는 공간 근처를 활용할것임
  

![](https://i.imgur.com/b0YBDI3.png)

# 보조기억장치
## 1. 다양한 보조 기억 장치
![](https://i.imgur.com/Yv0yIJP.png)

### 1) 하드디스크(자기디스크)
#### 정의
- 자기적인 방식으로 데이터를 저장하는 보조 기억 장치=>자기디스크라고도 부름
#### 구성요소
##### 플래터
- 실질적으로 데이터가 저장되는 곳
##### 스핀들
- 플래터를 회전시키는 구성 요소
- RPM : 분당 회전수 (스핀들이 플래터를 돌리는 속도)


![[../../img/Pasted image 20231130125613.png]]

##### 헤드
- 데이터를 읽고 쓰는 구성 요소
##### 디스크 암
- 헤드를 원하는 위치로 이동시키는 부품
![](https://i.imgur.com/SbPtoTS.png)

#### 데이터 저장 원리
##### 플래터의 구성 요소
- **트랙**
-> 동심원으로 플래터를 나누었을때 하나의 원

- **섹터**
-> 트랙의 하나의 조각


![](https://i.imgur.com/5Y5KbAX.png)

 - **실린더**
-> 여러 겹의 플래터 상에서 같은 트랙이 위치한 곳을 모아 연결한 논리적 단위
-> 같은 트랙끼리 연결한 원통 모양 공간
-> 연속된 정보는 한 실린더에 기록된다.

>EX **두개의 플래터**를 사용하는 하드에 **네 개의 섹터**에 걸쳐 데이터를 저장할때는 **1번째 플래터 윗면 뒷면**, **2번째 플래터 윗면 뒷면**에 데이터를 저장

![](https://i.imgur.com/FliLE5b.png)


##### 데이터 접근 시간
###### 탐색 시간
- 접근하려는 데이터가 저장된 트랙까지 헤드를 이동시키는 시간
- ![](https://i.imgur.com/DKJ0PJ8.png)

###### 회전 지연
- 헤드가 있는 곳으로 플래터를 회전시키는 시간
![](https://i.imgur.com/bkw20xG.png)

###### 전송 시간
- 하드 디스크와 컴퓨터 간에 데이터를 전송하는 시간
![](https://i.imgur.com/FcDN7WJ.png)


![](https://i.imgur.com/YtpmPls.png)



![](https://i.imgur.com/kjetx5w.gif)
### 2) 플래시 메모리
##### 정의
- 전기적으로 데이터를 읽고 쓸 수 있는 반도체 기반의 저장 장치
![](https://i.imgur.com/rC9Rd0j.png)

> 플래시 메모리는 NAND, NOR플래시 메모리가 잇는데 대용량으로 사용되는 것은 NAND플래시 메모리임

#### 셀
- 플래시 메모리에서 데이터를 저장하는 가장 작은 단위
- 이 셀이 모여서 **MB GB TB**가 됨
##### SLC
- 한 셀에 1비트를 저장할 수 있는 플래시
- 빠른 입출력
- 긴 수명
- 비쌈
![](https://i.imgur.com/MIcv6iE.png)

##### MLC
- 한 셀에 2비트를 저장할 수 있는 플래시
- 4 개의 정보 표현
- 느린 입출력
- 수명이 짧음
- 저렴함
![](https://i.imgur.com/CcGn9k0.png)

##### TLC
- 한 셀에 3비트를 저장할 수 있는 플래시
- MLC보다 느린 입출력
- MLC보다 짧은 수명
- 저렴함
![](https://i.imgur.com/DHp5uhx.png)

![](https://i.imgur.com/xCpYNsL.png)


#### 셀이 모인 단위
- 셀이 모인 단위 => 페이지
- 
- 페이지가 모인 단위 => 블록
- 
- 블록이 모인 단위 => 플레인
- 
- 플레인이 모인 단위 => 다이

![](https://i.imgur.com/TUGTKEE.png)

#### 페이지의 상태

##### Free 
- 어떠한 데이터도 저장하고 있지 않아 새로운 데이터를 저장할 수 있는 상태
##### Vaild
- 이미 유효한 데이터를 저장하고 있는 상태
- 플래시 메모리는 덮어쓰기가 불가능 => Valid상태인 페이지에는 새 데이터를 저장 불가능함
##### InVaild
- 유효하지 않는 데이터(쓰레기 값)을 저장하는 상태


#### 플레시 메모리 동작 과정
- c를 저장하는 단계
- 빈공간에 C를 저장함

![](https://i.imgur.com/UipxK37.png)

- 여기서 C와 B는 그대로 둔 채 A를 수정하려고함

- 기존 A는 쓰레기값이 되고 새로운 A'데이터가 저장됨

- 그러면 쓰레기값이 저장하고 있는 공간은 용량을 차지해서 낭비가 발생됨

=> 
#### 가비지 컬랙션 기능
- 유효한 페이지를 새로운 블록으로 복사
- 기존 블록삭제

![](https://i.imgur.com/DG8u94P.png)


## RAID의 정의와 종류

![](https://i.imgur.com/zQbRZoe.png)

### RAID
##### 정의
- 여러개의 물리적 보조기억장치를 하나의 논리적 보조기억장치처럼 사용하는 기술
- 데이터의 안정성, 높은 성능을 위해 만들어짐
- ![](https://i.imgur.com/UK1ePEg.png)

### RAID의 종류
##### RAID 레벨
- RAID를 구성하는 방법
#### RAID 0
##### 정의
- 보조기억장치를 단순히 나누어 구성하는 방식
![](https://i.imgur.com/ziHuMBi.png)

##### 저장 방식
- 각 하드 디스크가 번갈아 가며 데이터를 저장
- 저장되는 데이터가 하드디스크 개수만큼 나누어서 저장
- **스트라입** : 줄무늬처럼 분산되어 저장된 데이터
- **스트라이핑** : 분산하여 저장하는 것

![](https://i.imgur.com/tpzngaK.png)

##### 장점
- 대용량 장치 4TB한개를 쓰는 것보다 읽고 쓰는 속도가 이론상 4배나 더 빠름


##### 단점
- 저장된 정보가 안전하지 않음
![](https://i.imgur.com/SVB7H36.png)


#### RAID 1
##### 정의
- 복사본을 만들어 저장하는 방식 => **미러링**이라고 부름
![](https://i.imgur.com/ybZR78y.png)



##### 장점
- RAID 0보다 안전하고 복구가 간단함


##### 단점
- 복사본이 만들어지는만큼 용량이 작아짐


#### RAID 4
##### 정의
- 오류 검출 & 복구용 정보를 저장한 장치를 두는 구성방식
- **패리티 비트** : 오류를 검출하고 복구하기 위한 정보
> 원래 패리티 비트는 오류 검출만 가능하고 복구는 불가능함
> RAID에서는 패리티 값으로 오류 수정도 가능함
![](https://i.imgur.com/z7vg43l.png)


##### 단점
- 새로운 데이터가 저장될 때마다 패리티를 저장하는 디스크에 데이터를 쓰게 됨
- 패리티를 저장하는 장치에 병목현상이 생김

![](https://i.imgur.com/IUIUVQW.png)


#### RAID 5
##### 정의
- 패리티 정보를 분산하여 저장하는 방식

![](https://i.imgur.com/lN2sTlc.png)

##### 장점
- RAID 4 의 병목현상을 해결함

#### RAID 6

- 서로 다른 두 개의 패리티를 두는 방식
- RAID 4, 5보다 조금더 안전한 구성
- 쓰기 속도는 RAID 5 보다 느림
![](https://i.imgur.com/GWQ1BZ1.png)



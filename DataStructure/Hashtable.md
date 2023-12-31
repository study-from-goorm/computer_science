# Hash Table
## 정의
해싱을 사용하여 데이터를 저장하는 자료 구조

BST(Binary Search Tree)나 Array에 비해 굉장히 빠른 속도로 탐색, 삽입, 삭제 가능

해시 함수를 사용하여 변환한 값을 색인(Index)으로 삼아 키(Key)와 데이터(Value)를 저장하는 자료 구조

![image](https://github.com/study-from-goorm/computer_science/assets/148074385/a835ccb9-6f44-4fa9-ba4d-da16210607fe)

**해시 테이블의 시간 복잡도는 O(1)이다.**

하지만 반드시 1인 것은 아니다.

적재율*이 1 초과인 해시 테이블의 경우 반드시 충돌 발생한다.

![image](https://github.com/study-from-goorm/computer_science/assets/148074385/49fc4b1a-bb21-46c6-908a-1134e5cc23f6)


만약, 충돌이 발생하지 않다고 할 경우 해시 테이블의 탐색, 삽입, 삭제 연산은 모두 O(1)에 수행 되지만 충돌이 발생할 경우 탐색과 삭제 연산이 최악에 O(K)만큼 걸리게 된다.

이는 같은 인덱스에 모든 키 값과 데이터가 저장된 경우 충돌이 전부 발생했음을 뜻한다. 

따라서, **충돌을 최대한 줄여서 연산 속도를 빠르게 하는 것**이 해시 테이블의 핵심인데 이에 중요하게 작용하는 것이 해시 알고리즘이다.

해시 알고리즘이 견고하지 못하게 되면 해시 함수로 도출된 값들이 같은 경우에 빈번하게 발생하게 되므로 잦은 충돌로 이어지게 되는 것이다.

*Load Factor 적재율 : 해시 테이블의 크기(N) 대비 키의 개수(K) -> K/N


## 충돌 완화 방법 : 해시 테이블의 구조 개선/ 해시 함수 개선


## 1. 해시 테이블의 구조 개선

### 1) Chaining
   충돌이 발생했을 때 이를 동일한 Bucket에 저장하는데 이를 연결 리스트 형태로 저장하는 방법이다.
   
   체이닝을 통해 해시테이블을 구현했을 때의 시간 복잡도
   
   삽입의 경우 연결 리스트에 추가하기만 하면 되니까 상수 시간인 O(1)이 걸리지만
   
   삭제의 경우 최악일 때 키 값의 개수인 K에 대해 O(K)가 걸리게 된다.
   
   하지만 최악의 경우 보다는 시간복잡도를 적재율을 이용해서 평균으로 표현하는 것이 일반적
 
![image](https://github.com/study-from-goorm/computer_science/assets/148074385/f19c804c-6e20-4f75-81ba-d8d29c775218)

### 2) Open Addressing
   동일한 주소에 다른 데이터가 있을 경우 다른 주소도 이용할 수 있게 하는 기법
   ![image](https://github.com/study-from-goorm/computer_science/assets/148074385/169809d6-7054-4c19-a058-578ffb2a3319)

### 2-1) Linear Probing(선형탐사)
 가장 기본적인 충돌해결기법으로 위에서 설명한 기본적인 동작방식
 바로 인접한 인덱스에 데이터를 삽입해가기 때문에 데이터가 밀집되는 클러스터링(Clustering) 문제가 발생하고 이로 인해 탐색과 삭제가 느려지게 된다.

 ![image](https://github.com/Hyejin724/computer_science/assets/148074385/b4319182-4088-4651-8cb6-2e63c0e82481)

### 2-2) Quadratic Probing(제곱탐사)
 1^2, 2^2, 3^2 로 탐색하는 방식으로 선형 탐사에 비해 더 폭넓게 탐사하기 때문에 탐색과 삭제에 효율 적이다.
 하지만 초기 해시값이 같을 경우의 탐사는 클러스터링 문제가 발생한다.

![image](https://github.com/Hyejin724/computer_science/assets/148074385/4ee06382-bc5c-460e-a420-aadef73460e8)

### 2-3) Double Hashing (이중해싱)
 선형 탐사와 제곱탐사에서 발생하는 클러스터링 문제를 모두 피하기 위해 도입된 것이다.
 처음 해시 값을 찾기 위해 해시 함수를 사용하고, 두번째 해시 함수는 충돌이 발생했을 때 탐사폭을 게산하기 위해 사용되는 방식이다.

### 비교
![image](https://github.com/Hyejin724/computer_science/assets/148074385/297fd299-47a0-4a35-8b01-54e048013dcc)

충돌 해결 기법들을 비교해보면 successful search는 찾고자 하는 데이터가 해시 테이블에 있는 경우이고,unsuccessful search는 없는 경우이다.

## 2. 해시 함수 개선

###   1) Division Method
      해시 테이블의 크기인 N을 아는 경우에 사용할 수 있다.
      해시 함수를 적용하고자 하는 값을 N으로 나눈 나머지를 해시값으로 사용하는 방법
      h(k) = k mod N / N은 소수를 사용하는 것이 좋다.
      
###   2) Multiplication Method
      0<A<1인 A에 대해서 구할 수있다.
      h(k) = N(kA mod 1)
      kA mod 1 : kA의 소수점 이하 부분, N에 곱하므로 0부터 N 사이의 값이 된다.
      N이 어떤 값이더라도 잘 동작하며, A를 잘 잡는 것이 중요하다.

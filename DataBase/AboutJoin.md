# 데이터베이스 조인의 원리 🌟

데이터베이스에서 조인(join)은 여러 테이블을 하나의 집합으로 결합하는 중요한 연산입니다. SQL에서 FROM 절에 여러 테이블이 나열될 때 조인이 수행됩니다.

조인의 세 가지 주요 기법 - NL Join, Sort Merge Join, Hash Join에 대해 알아보겠습니다!

## 1️⃣ 중첩 루프 조인 NL Join (Nested Loop Join)

NL Join은 중첩 for문과 같은 원리로 조건에 맞는 조인을 하는 방법입니다.

<img src ='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbE4hk%2FbtqBVNjxwmP%2FvoZYsGAKqSMRQt1KCq3CM1%2Fimg.jpg'>

### 🔄 작동 원리
1. 선행 테이블 (Outer Table): 조건을 만족하는 첫번째 행을 찾음
2. 후행 테이블 (Inner Table): 선행 테이블의 조인 키를 사용하여 후행 테이블에서 조인 수행
3. 반복 수행: 선행 테이블의 모든 조건을 만족하는 행에 대해 이 과정을 반복

> ex. course_name(Outer Table)과 player_name(Inner Table)과 같이 1:N의 관계에서 주로 사용

### 💡 특징
- 랜덤 액세스 방식 사용 (랜덤 접근에 대한 비용이 많이 발생하므로 대용량 테이블에서는 ❌)
- 결과 행이 적은 테이블을 선행 테이블로 선택하면 전체 작업 부담 감소
- 인덱스가 있을 경우, 인덱스를 통해 선행 테이블 액세스 가능
- 온라인 프로그램(OLTP : Online Transaction Processing)에 적합

## 2️⃣ 정렬 병합 조인 (Sort Merge Join)

Sort Merge Join은 조인 칼럼을 기준으로 데이터를 정렬하여 조인을 수행합니다.

(정렬작업이 PGA영역에서 실행되기 때문에 경합이 발생하지 않아 성능에 유리한 이점이 있음)

<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnBaNw%2FbtqBWDHuR25%2FtqADgyLgJsBzPnyrfNFTX0%2Fimg.jpg'>

### 🔄 작동 원리
1. 정렬 단계: 각 테이블에서 조인 키를 기준으로 행 정렬
2. 병합 단계: 정렬된 결과를 이용하여 조인 수행

### 💡 특징
- Table Random Access가 일어나지 않음 (테이블의 특정 레코드에 직접 접근하는 방식)
- 대량의 조인 작업 시, CPU 작업 위주로 처리하는 Hash Join이 성능상 유리
- 비동등 조인과 동등 조인 모두 가능
- 인덱스를 사용하지 않음 (Inner Table 쪽에 적절한 인덱스가 없어서 NL Join을 쓰기에 너무 비효율적일 때 사용)

## 3️⃣ 해시 조인 (Hash Join)

Hash Join은 해싱 기법을 이용하여 조인을 수행합니다. (PGA 영역에서 수행 되기에 빠름)

<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbW1ZnN%2FbtqBWqVUSnB%2F9N7UpCeKlj8WRj5GVT4KzK%2Fimg.jpg'>

### 🔄 작동 원리
1. 선행 테이블: 조인 키에 해시 함수 적용, 해시 테이블 생성
2. 후행 테이블: 해시 테이블과 조인 키를 이용하여 조인 수행

> ex. course_name(Outer Table)과 player_name(Inner Table)과 같이 1:N의 관계라고 생각하되 코스와 플레이어의 수가 많다고 생각하기

### 💡 특징
- 배치에서 쓰면 좋은 수행 원리이다 (대용량 데이터 처리)
- 동등 조인에 최적화 (비동등 조인 ❌)
- key 컬럼에 중복값이 없을수록 성능에 유리(해시함수가 적용되기 때문에)
- 해시 테이블은 메모리에 생성됨
- 결과 행이 적은 테이블을 선행 테이블로 사용하는 것이 좋음


---
```
* PGA(Program Global Area)는 데이터베이스 시스템, 특히 Oracle 같은 관계형 데이터베이스 관리 시스템(RDBMS)에서 사용되는 메모리 영역입니다.
```

##### 참고자료 https://www.youtube.com/watch?v=SVD5ldwVYpo
##### 사진출처 https://dev-mystory.tistory.com/74
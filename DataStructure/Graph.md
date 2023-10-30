# Graph
Node(정점)와 Edge(간선)로 이뤄져 각 node들이 연결되어 시각적으로 나타낼 수 있으며, 해당 노드 간의 관게를 설명하는 자료 구조

![image](https://github.com/study-from-goorm/computer_science/assets/148074385/13da9d18-95a4-4b02-b52b-04575053afca)

## 특징
1. 네트워크 모델
2. 2개 이상의 경로가 가능하다. -> 노드들 사이에 무방향/방향에서 양방향 경로를 가질 수 있다.
3. Self-Loop 뿐만 아니라 Loop/Circuit 모두 가능하다.
4. 부모-자식 관계 개념이 없다.
5. 간선의 유무는 그래프에 따라 다르다.

사용 예) 노드 간의 관계 파악으로 SNS 관계도 및 도로상의 차량 정보를 바탕으로 한 운송 서비스나 기타 경로 파악에도 사용되며, 
공간 데이터를 활용해 상권파악이나 기타등등의 다양한 산업에서 적용할 수 있다.

# Graph 종류
## 방향성과 무방향성

![image](https://github.com/study-from-goorm/computer_science/assets/148074385/2f267143-6bbf-4352-904d-58a245822cd3)

### Directed (방향성)
: 첫 노드부터 끝 노드까지 일련의 일관된 방향이 있는 경우 방향성으로 판단
- 일방향성 : 내부의 노드간 순환의 방향이 **한쪽**으로 순환
- 양방향성 : 내부의 노드간 순환의 방향이 **양쪽**으로 순환

### Undirected (무방향성)
: 노드 간 연결이 따로 방향성을 띄지 않고 연결되어 있는 모든 노드가 서로 상호 관계를 갖는다.

## 순환과 비순환

![image](https://github.com/study-from-goorm/computer_science/assets/148074385/7e4a6ffa-40ce-46f3-9a45-10abd02eef50)

### Cyclic(순환)
: 내부에서 방문했던 노드를 다시 방문하게 되는 경우
### Acyclic(비순환)
: 내부에서 재방문이 진행 안되는 방향으로 구성

## 연결과 비연결 그래프
### Connected Graph(연결 그래프)
: 모든 정점에 대해 항상 경로를 가지는 그래프

![image](https://github.com/Hyejin724/computer_science/assets/148074385/9ca8c64f-bf60-44bd-bfc8-bbe6233b4e45)

### Disconnected Graph(비연결 그래프)
: 정점들 사이에 간선이 존재하지 않아 경로가 없는 경우가 존재하는 그래프

![image](https://github.com/Hyejin724/computer_science/assets/148074385/7dfe7c1f-dfcd-4245-9b71-190b723b6286)

## Weighted Graph(가중치 그래프)
![image](https://github.com/Hyejin724/computer_science/assets/148074385/dfc21a88-45d0-4d00-804b-350ba3b0f89a)

: 간선에 비용또는 가중치가 할당된 그래프 (=네트워크)
예) 도시-도시 연결, 도로의 길이, 회로 소자의 용량, 통신망의 사용료 등
* 도로 지도의 경우, 두 곳의 최단 경로를 검색할 때에는 두 정점 간의 모든 경로에서 변의 가중치 합이 최소가 되는 경로를 찾는다.

## Complete Graph(완전 그래프)
![image](https://github.com/Hyejin724/computer_science/assets/148074385/25ac4787-94d2-4af9-82b6-02e28dae5ce9)
: 모든 정점이 서로 하나의 간선으로 연결되어 있는 그래프

**무방향 완전 그래프의 경우, 정점이 n개일 때, 간선의 수는 n*(n-1)/2이다.

## 희소와 밀집
### Sparse Graph(희소 그래프)
![image](https://github.com/Hyejin724/computer_science/assets/148074385/b3ab6787-0852-4cb7-8e63-b29f7e664072)

: 정점의 개수보다 간선 개수가 적은 그래프

### Dense Graph(밀집 그래프)
![image](https://github.com/Hyejin724/computer_science/assets/148074385/adccd9fc-7cda-44d0-b96b-a2c8549da0a8)
: 정점의 개수보다 간선 개수가 많은 그래프

다음 시간에

# 그래프의 구현
## 인접 행렬
## 인접 리스트(Adjacent List)


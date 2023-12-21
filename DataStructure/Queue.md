# 큐 (Queue)

> 선입선출(FIFO) 자료구조

> enqueue -> O(1), dequeue -> O(1)

### 활용되는 사례
- Cache 구현
- 프로세스 관리
- BFS 너비우선 탐색

## 구현방식

### Array Based
![array based queue](images/array-based-queue.png)

`dequeue`를 하게될 경우 이미 할당된 메모리 사이즈내에서 비효율성을 가지게 된다.

![circular queue](images/circular-queue.png)
![circular queue2](images/circular-queue-2.png)
![circular queue3](images/circular-queue-3.png)

- 이미 할당된 메모리 사이즈를 최대한 활용할 수 있다.
- 하지만, 이미 할당된 메모리 사이즈를 넘어서 `enqueue`할 경우 dynamic array 특징인 `resizing`해줘야 한다. O(n)

### Linked Based
- `Linked List`로 구현하는 방식
- `enqueue`, `dequeue`시 메모리를 새로 할당해서 연결한다.
- 메모리의 낭비는 없지만 메모리 할당시 전반적인 속도는 array based 방식보다 시간이 걸린다.

### Stack 2개를 이용해서 Queue 구현하기
- `enqueue` 구현하기
  - instack에 `push`
  - O(1)

-  `dequeue`를 구현하기 
   - outStack이 만약 비어있다면
   - instack pop 실행
   - outstack push 실행
   - outstack pop 실행
   - O(1), worst case: O(n)

![stack to queue](images/stack-to-queue.png)
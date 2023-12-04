## Linked List는 어떤 자료구조인가?

---

`노드`라는 구조체에 데이터값과 다음 Node 주소를 저장하는 자료구조

데이터가 메모리에 저장되는 방식은 비연속적인지만 논리적으론 연속적이다.

- 데이터를 추가되는 시점에 메모리를 할당하기때문에 메모리 낭비가 적다.
- 하지만 그만큼 주소정보가 들어가기때문에 데이터 하나당의 크기가 더 커지게 됨

- 중간 삽입, 삭제 O(1) 근데 사실 (n이기도 함)
- access O(n)

## Linked List 시간복잡도

- 조회 : `O(n)`
- 마지막 인덱스 추가삭제 : `O(n)`
- 중간 삽입, 삭제 : `O(1)`
- 탐색 : 어떤 숫자가 몇번째 인덱스에 있는지 `O(n)`

## ⭐️ Array List vs LinkedList

- 각 Operation 시간복잡도가 다르다.
- 데이터양이 얼마인지 미리 예상이 가능하고 조회를 많이 한다면 `Array`
- 데이터양이 불확실하고 삽입 삭제가 많다면 `Linked List`

## Array List vs LinkedList 메모리 할당되는 영역 비교

- Compile -> Runtime 과정

- Array는 Compile과정에 메모리 할당 `Stack 영역`
- Linked List는 Runtime과정에 메모리 할당 `Heap 영역`

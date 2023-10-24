# Tree Structure

앞서 언급했던 Array, Stack, Queue와 비롯하여 Linked List는 선형 구조이다.
트리 구조는 계층, 구조, 부모 관계를 갖는다.
트리에는 Root node, parent node, child node, Leaf(terminal node), internal node가 있다.
- Root node : 최상위 노드, 뿌리 노드
- 노드 A가 노드 B를 가리킬 때
  - Parent node :  A를 부모 노드라고 한다.
  - Child node : B를 자식 노드라고 한다.
- Leaf node(terminal node) : 자식 노드가 없는 노드를 잎 노드, 말단 노드라고 한다.
- Internal node : 잎 노드가 아닌 노드
  
![image](https://github.com/Hyejin724/computer_science/assets/148074385/ee4b96fc-80b2-48a5-82f6-8dc941184c6f)

## Binary Tree(이진 트리)
 : child node가 최대 2개까지만 붙는다.
 
   *Ternary tree : child node가 최대 3개까지 붙는다.
 
## BST(Binary Search Tree)
 : 왼쪽과 오른쪽 노드 값을 비교하였을 때, 오른쪽에 큰 값을 두는 것이 특징.
 
![image](https://github.com/Hyejin724/computer_science/assets/148074385/bde291ec-145c-4996-acf7-0e7a6a382ac6)


## Full Binary Tree
: 모든 노드가 0 혹은 2개의 child node를 가진 형태

![image](https://github.com/Hyejin724/computer_science/assets/148074385/66bf4c43-25d1-437f-b12d-50746fedf6fe)

## Complete Binary Tree
: 마지막을 제외한 모든 레벨에서 노드들이 왼쪽부터 존재하는 형태

![image](https://github.com/Hyejin724/computer_science/assets/148074385/111bfa3b-65fe-44e0-8fd9-8fe614adb800)


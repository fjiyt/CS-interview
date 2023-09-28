# 트리

<aside>
💡 node와 edge로 이루어진 자료구조


</aside>

## 특징

- 사이클이 존재할 수 없다. → 사이클이 있으면 트리가 아니고 그래프
- 루트노드가 하나인 사이클이 없는 그래프
- 모든 노드는 자료형으로 표현이 가능하다
- 루트에서 한 노드로 가는 경로는 유일한 경로뿐이다.
- 노드의 개수가 N개면, 간선은 N-1개

## 용어

- root : 최상위 노드
- edge : 두 노드 사이의 링크 또는 연결선
- parent : 자식 노드에 대한 간선이 있는 노드
- child : 부모 노드가 있는 노드
- leaf : 자식노드가 없는 노드
- height : 단말 노드까지의 가장 긴 경로의 길이
- depth : 루트 노드까지의 경로 길이

# 트리 순회 방식 (root를 언제 방문하는지)

## 깊이우선탐색(DFS)

1. 전위 순회

   root-왼쪽-오른쪽

2. 중위 순회

   왼쪽-root-오른쪽

3. 후위 순회

   왼쪽-오른쪽-root

```java
public class Tree {
    int count;
    public Tree() {
        count = 0;
    }

    public class Node{
        Object data;
        Node left;
        Node right;

        // 생성시 매개변수를 받아 초기화하는 방법으로 선언
        public Node(Object data)
        {
            this.data = data;
            left = null;
            right = null;
        }

        public void addLeft(Node node)
        {
            left = node;
            count++;
        }

        public void addRight(Node node)
        {
            right = node;
            count++;
        }

        public void deleteLeft() {
            left = null;
            count--;
        }

        public void deleteRight() {
            right = null;
            count--;
        }
    }

    public Node addNode(Object data) {
        Node n = new Node(data);
        return n;
    }

    public void preOrder(Node node) {
        if(node==null) return;
        System.out.print(node.data + " ");
        preOrder(node.left);
        preOrder(node.right);
    }

    public void inOrder(Node node) {
        if(node==null) return;
        inOrder(node.left);
        System.out.print(node.data + " ");
        inOrder(node.right);
    }

    public void postOrder(Node node) {
        if(node==null) return;
        postOrder(node.left);
        postOrder(node.right);
        System.out.println(node.data+" ");
    }
}
```

## 너비우선탐색(BFS)

- 레벨 순회

→ Queue를 이용한다.

```java
private void printLevelOrder(Node node) {
	Queue <Node> queue = new LinkedList <> ();
	queue.add(node);

	while(!queue.isEmpty())
	{
		Node current = queue.poll();
		System.out.println(current.element);

		if(current.left!=null) queue.add(current.left);
		if(current.right != null) queue.add(current.right);
	}
}
```

# 이진탐색트리

- 정렬 규칙 + 이진트리
- 왼쪽 하위 트리 < 루트 , 루트 < 오른쪽 하위 트리

![Untitled](Tree/Untitled.png)

- 일반적으로 이진탐색 트리는 중복 요소를 허용하지 않지만, 허용할 경우에는 어느 한쪽 또는 양쪽에 있을 수 있음
- 중복 요소는 별도의 해시맵에 저장하거나 카운터를 통해 트리 구조에 직접 저장 가능
- 예시 ) Java의 TreeSet의 경우 이진탐색트리로 구현되어있다.

## 균형 및 불균형 이진트리

<aside>
💡 균형 이진 트리
- 삽입 및 검색 연산에 O(logn) 시간을 보장하는 이진트리
- 왼쪽 하위 트리와 오른쪽 하위 트리의 높이 차이 1 이하


</aside>

![Untitled](Tree/Untitled%201.png)

## 레드블랙트리

### 규칙

- 모든 노드는 빨간색 or 검은색
- 루트 노드는 항상 검은색
- 모든 단말 노드(NIL)는 검은색 (NIL : null leaf, 자료를 갖지 않고 트리의 끝을 나타내는 노드)
- 빨간색 노드의 양쪽 자식 노드는 모두 검은색 (== 빨간 노드가 연속으로 나올 수 없다)
- 한 노드에서 NIL 노드로의 모든 경로에는 동일한 수의 검은색(블랙) 노드가 있습니다.

![Untitled](Tree/Untitled%202.png)

## AVL 트리

### 규칙

- 하위 트리의 높이는 최대 1만큼 다를 수 있다.

- 노드 n의 균형 계수 BN은 -1,0,1이며 높이 h의 차이로 정의됨

  BN = h(right_subtree(n) - left_subtree(n))

  BN = h(left_subtree(n) - right_subtree(n))

![Untitled](Tree/Untitled%203.png)

### 시간복잡도

모든 연산 (삽입, 삭제, 최솟값 검색, 최댓값 검색) : O(logn)

# 완전이진트리(Complete Binary Tree)

- 마지막을 제외한 모든 레벨이 완전히 채워진 이진 트리
- 부모, 왼쪽자식, 오른쪽 자식 순으로 채워지는 트리
- 완전 이진 트리의 높이는 항상 O(logn)

![Untitled](Tree/Untitled%204.png)

# 정이진트리 (Full Binary Tree)

- 모든 노드에 2개의 자식이 있거나 아예 없는 이진트리

![Untitled](Tree/Untitled%205.png)

# 포화이진트리 (Perfect Binary Tree)

- 정이진트리 + 완전이진트리

![Untitled](Tree/Untitled%206.png)

# 힙

- 완전 이진트리
- 부모노드의 키값과 자식노드의 키값 사이에는 대소관계가 성립한다.
  - 형제사이에는 대소관계가 정해지지 않음

## 최대힙

- 부모 키값 > 자식 노드 키값
- 가장 큰 값이 루트노드에 있음

![Untitled](Tree/Untitled%207.png)

## 최소힙

- 부모 키값 < 자식노드 키값
- 가장 작은 값이 루트노드에 있음

![Untitled](Tree/Untitled%208.png)

## 힙 표현

- 힙은 완전 이진트리
- 힙은 일반적으로 배열로 표현

### 속성

- 노드 i의 부모노드 인덱스 : ⌊i/2⌋
- 노드 i의 왼쪽 자식 노드 인덱스 : 2*i
- 노드 i의 오른쪽 자식 노드 인덱스 : 2*i +1

## Heapify

이진트리에서 힙 속성을 유지하는 작업

위에서 아래로 내려가면서 작업을 함

### 순서

1. 요소 값과 자식 노드 값을 비교합니다.
2. 만약 자식 노드 값이 크다면 왼쪽 오른쪽 자식 중 가장 큰 값으로 교환합니다.
3. 힙 속성이 유지 될 때까지 1,2번 과정을 반복합니다.

![Untitled](Tree/Untitled%209.png)

# 2022.10.17(월)

# 08-1 트리의 개요

## 트리

계층적 관계를 ‘표현’하는 자료구조

예) 컴퓨터의 디렉터리 구조, 기업 및 정부의 조직도

## 트리 관련 용어

- 노드: 트리의 구성요소에 해당하는 A~I와 같은 요소
- 간선: 노드와 노드를 연결하는 연결 선
- 루트 노드: 트리 구조의 최상위에 존재하는 A와 같은 노드
- 단말 노드(leaf node): 아래로 또 다른 노드가 연결되어 있지 않은 D, F, H, I와 같은 노드
- 내부 노드(비단말 노드): 단말 노드를 제외한 모든 노드로 A, B, C, E, G와 같은 노드

- 노드 A는 노드 B, C의 부모 노드
- 노드 B, C는 노드 A의 자식 노드
- 노드 B, C는 부모 노드가 같으므로, 서로가 서로에게 형제 노드

## 이진 트리와 서브 트리

서브 트리: 큰 트리에 속하는 작은 트리

**이진 트리(재귀적)**

루트 노드를 중심으로 두 개의 서브 트리로 나뉘어진다.

나뉘어진 두 서브 트리도 모두 이진 트리여야 한다.

+ 노드가 위치할 수 있는 곳에 노드가 없다면, 공집합 노드가 존재하는 것으로 간주한다.

## 포화 이진 트리와 완전 이진 트리

**포화 이진 트리**

모든 레벨이 꽉 차 있다.

**완전 이진 트리**

노드와 위에서 아래로, 왼쪽에서 오른쪽의 순서대로 채워진 이진트리


# 08-2 이진 트리의 구현

배열과 연결 리스트를 이용하여 구현 가능

배열 기반 이진 트리는 연결 리스트 기반 이진 트리에 비해 탐색이 용이하고 빠름

## 이진 트리의 ADT

```python
def __init__(self): # 트리 초기화

def is_empty(self): # 트리가 비어 있으면 True(1), 그렇지 않으면 False(0) 반환

def treesize(self): # 노드 개수

def rootnode(self): # 루트 노드 반환

def parent(self,v): # 특정 노드의 부모 노드 반환

def children(self,v): # 특정 노드의 자식 노드 반환

def addNode(self,v,data,location): # 트리에 노드 추가
```

## 이진 트리의 구현

```python
class Node:
  def __init__(self,data,L=None,R=None,parent=None):
    self.data = data
    self.L = L
    self.R = R
    self.parent = parent

class tree:
  def __init__(self):
    self.root = None
    self.n=0

  def isEmpty(self):
    return self.root==None
  
  def treesize(self):
    print(self.n)
    return self.n
  
  def rootnode(self):
    return self.root.data
  
  def parent(self,v):
    if v == self.root:
      print("Root Node")
    else:
      return v.parent.data
  
  def children(self,v):
    return v.L.data,v.R.data

  def isInternal(self,v): # 내부노드인지
    if v.L != None or v.R != None:
      return True
    else: 
      return False
  
  def isExternal(self,v): # 단말노드인지
    if v.L == None and v.R == None:
      return True
    else:
      return False
  
  def isRoot(self,v):
    if self.root == v:
      return True
    else:
      return False
  
  def setElements(self,v,e):
    tmp = v.data
    v.data = e
    print(f"Succesly set element v.data : {tmp}=> {e}")
  
  def addNode(self,v,data,location):
    if location =='L':
      v.L = Node(data,None,None,v)
      self.n+=1
    elif location == 'root':
      self.root = Node('Root')
      self.n+=1
    else:
      v.R = Node(data,None,None,v)
      self.n+=1
```


# 2022.10.18(화)
# 08-3 이진 트리의 순회

- 전위 순회: 루트 노드를 먼저 방문
- 중위 순회: 루트 노드를 중간에 방문
- 후위 순회: 루트 노드를 마지막에 방문

## 순회의 재귀적 표현

- 중위 순회
    
    ```python
    def inorder(self, n):
    	if n != None:
    		if n.left:
    			self.inorder(n.left)
    		print(n.item, end='') # 노드 방문
    		if n.right:
    			self.inorder(n.right)
    ```
    
- 전위 순회
    
    ```python
    def preorder(self, n):
    	if n != None:
    		print(n.item, end='') # 노드 방문
    		if n.left:
    			self.inorder(n.left)
    		if n.right:
    			self.inorder(n.right)
    ```
    
- 후위 순회
    
    ```python
    def postorder(self, n):
    	if n != None:
    		if n.left:
    			self.inorder(n.left)
    		if n.right:
    			self.inorder(n.right)
    		print(n.item, end='') # 노드 방문
    ```
    

# 08-4 수식 트리의 구현

## 수식 트리

이진 트리를 이용해서 수식을 표현해 놓은 것


루트 노드에 저장된 연산자의 연산을 하되, 두 개의 자식 노드에 저장된 두 피연산자를 대상으로 연산을 한다.

중위 표기법의 수식→ 후위 표기법의 수식→ 수식 트리

- 수식 트리의 구성과정에서 피연산자는 무조건 스택으로 옮긴다
- 연산자를 만나면 스택에 쌓여있는 두 개의 피연산자를 꺼내어 자식 노드로 연결한다.
- 자식 노드를 연결해서 만들어진 트리는 다시 스택으로 옮긴다.

```Python
import re

def postfix_convert(infix):
    stk = [] # 스택
    cal = []
    expression = re.sub('([\+\-\*\/\(\)])', '\g<1>', infix)
    print("Postfix: ", end="")

    for x in expression.split():
        if x == '(':
            stk.append(x)
        elif x == '+' or x == '-':
            if '+' in stk or '-' in stk or '*' in stk or '/' in stk:
                pop_stk = stk.pop()
                if pop_stk == '(':
                    stk.append(pop_stk)
                    stk.append(x)
                else:
                    stk.append(pop_stk)
                    print(stk.pop(), end=" ")
                    cal.append(pop_stk)
                    stk.append(x)
            else:
                stk.append(x)
        elif x == "*" or x == '/':
            if '*' in stk or '/' in stk:
                print(stk.pop(), end=" ")
                cal.append(stk.pop())
                stk.append(x)
            else:
                stk.append(x)
        elif x == ")":
            while stk:
                p = stk.pop()
                if p == "(":
                    continue
                else:
                    print(p, end=" ")
                    cal.append(p)
        else:
            print(x, end=" ")
            cal.append(x)
    while stk:
        pop_stk2 = stk.pop()
        print(pop_stk2, end=" ")
        cal.append(pop_stk2)
    return cal

class Node(object):
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def create_expression_tree(infix):
    postfix = postfix_convert(infix)
    print("\n")
    stack = []
    cal_stack = []
    operator_precedance = {'(', ')', '+', '-', '*', '/'}

    for char in postfix:
        if char not in operator_precedance:
            node = Node(char)
            stack.append(node)
            cal_stack.append(node)
        else:
            node = Node(char)
            right = stack.pop()
            left = stack.pop()
            node.right = right
            node.left = left
            stack.append(node)
            print(char, "-> [child:", node.left.value, ", silbling:", node.right.value, "]")
            print()
            cal_right = cal_stack.pop()
            cal_left = cal_stack.pop()
            # 사칙연산 계산
            if char == "+":
                cal = float(cal_left.value) +float(cal_right.value)
                cal_node = Node(cal)
                cal_stack.append(cal_node)
            elif char == "-":
                cal = float(cal_left.value) - float(cal_right.value)
                cal_node = Node(cal)
                cal_stack.append(cal_node)
            elif char == "*":
                cal = float(cal_left.value) * float(cal_right.value)
                cal_node = Node(cal)
                cal_stack.append(cal_node)
            elif char == "/":
                cal = float(cal_left.value) / float(cal_right.value)
                cal_node = Node(cal)
                cal_stack.append(cal_node)

    print("root --> [", stack.pop().value, "]")
    print("\n계산결과 :", cal_stack.pop().value)

create_expression_tree("((3*4)+(6-8))")
```

# 2022.10.19(수)

# 09-1 우선순위 큐의 이해

## 우선순위 큐

들어간 순서에 상관없이 우선순위가 높은 데이터가 먼저 나온다.

- enqueue 우선순위 큐에 데이터를 삽입하는 행위
- dequeue 우선순위 큐에서 데이터를 꺼내는 행위

## 우선순위 큐의 구현 방법

1. 배열 기반 구현
    
    데이터 삽입, 삭제 시 데이터를 한 칸씩 이동하는 연산을 수반한다
    
    삽입의 위치를 찾기 위해 배열에 저장된 모든 데이터와 우선순위 비교를 해야 할 수도 있다
    
2. 연결 리스트 기반 구현
    
    삽입의 위치를 찾기 위해 배열에 저장된 모든 데이터와 우선순위 비교를 해야 할 수도 있다
    
3. 힙 이용

## 힙(Heap)의 소개

이진 트리이되 완전 이진 트리

모든 노드에 저장된 값은 자신 노드에 저장된 값보다 크거나 같아야 한다.


# 2022.10.21(금)
# 09-2 힙의 구현과 우선순위 큐의 완성

## 힙에서의 데이터 저장 과정(최소 힙 기준)

1. 새로운 데이터는 우선순위가 가장 낮다는 가정 하에 ‘마지막 위치’에 저장
2. 부모 노드와 우선순위를 비교하여 위치가 바뀌어야 한다면 바꿔준다
    
    <aside>
    💡 자식 노드의 데이터 우선순위 ≤ 부모 노드 데이터의 우선순위
    
    </aside>
    
3. 제대로 된 위치를 찾을 때까지 계속해서 부모 노드와 비교


## 힙에서의 데이터 삭제 과정

1. 루트 노드를 삭제
2. 마지막 노드를 루트 노드의 자리로 옮긴 후, 자식 노드와 비교를 통해 제자리를 찾아가게 함


## 성능 평가

1. 배열 기반
    
    데이터 저장의 시간 복잡도 **O(n)**
    
    데이터 삭제의 시간 복잡도 **O(1)**
    
2. 연결 리스트 기반
    
    데이터 저장의 시간 복잡도 **O(n)**
    
    데이터 삭제의 시간 복잡도 **O(1)**
    
3. 힙 기반
    
    트리의 높이에 해당하는 수만큼만 비교연산을 진행하면 된다
    
    데이터 저장의 시간 복잡도 **O(log2n**)
    
    데이터 삭제의 시간 복잡도 **O(log2n)**
    

## 배열 기반 힙

<aside>
💡 왼쪽, 오른쪽 자식 노드의 인덱스 값을 얻는 방법, 부모 노드의 인덱스 값을 얻는 방법

</aside>

- 왼쪽 자식 노드의 인덱스 값       부모 노드의 인덱스 값 * 2
- 오른쪽 자식 노드의 인덱스 값   부모 노드의 인덱스 값 * 2 + 1
- 부모 노드의 인덱스 값               자식 노드의 인덱스 값 / 2

- **heapq 사용 x**
    
    ```python
    import sys
    input = sys.stdin.readline
    
    heap = [float('inf')] # 배열의 빈 부분을 0 대신 무한으로 채워넣는다
    capacity = 0 # 배열 용량
    
    def push(heap, n):
        global capacity
        # heap의 자리가 부족할 경우 배열을 2배로 늘려나간다
        if len(heap)-1 == capacity:
            heap = heap + [float('inf')]*len(heap)
        
        capacity += 1
        heap[capacity] = n
        
        # above heapify
        tn = capacity
        while(tn > 1):
            if heap[tn] < heap[tn//2]:
                temp = heap[tn]
                heap[tn] = heap[tn//2]
                heap[tn//2] = temp
                tn//=2
            else:
                break
        return heap
    
    def pop(heap):
        global capacity
        if capacity == 0: # heap이 비어 있으면
            return 0
        p = heap[1]
        heap[1] = heap[capacity]
        heap[capacity] = float('inf')
        
        # below heapify
        tn = 1
        while(capacity > tn*2):
            if heap[tn*2] == float('inf') and heap[tn*2+1] == float('inf'):
                break
               
            if heap[tn] > min(heap[tn*2], heap[tn*2+1]): # 부모노드가 자식 노드보다 크면
                temp = heap[tn]
                if heap[tn*2] < heap[tn*2+1]: # 왼쪽 자식노드가 작으면
                    heap[tn] = heap[tn*2]
                    heap[tn*2] = temp
                    tn *= 2
                else: # 오른쪽 자식노드가 작으면
                    heap[tn] = heap[tn*2+1]
                    heap[tn*2+1] = temp
                    tn = tn*2+1
            else:
                break
        capacity -= 1
        return p
        
    
    for i in range(int(input())):
        x = int(input())
        if x:
            heap = push(heap,x)
        else:
            print(pop(heap))
    ```
    
- **heapq 사용**
  ```python
  import sys
  import heapq
  input = sys.stdin.readline

  def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
      heapq.heappush(h, value)
    
    # 힙에 삽입된 모든 원소를 차례대로 꺼냄
    for i in range(len(h)):
      result.append(heapq.heappop(h))
    return result

  n = int(input())
  arr = []

  for i in range(n):
    arr.append(int(input))

  h = heapsort(arr)

  for i in range(n):
    print(h[i], end=' ')
  ```
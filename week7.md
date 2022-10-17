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
# 2022.10.04(화)

# 04-1 연결 리스트의 개념적인 이해

## 연결 리스트

연결 기반의 리스트

배열은 메모리의 특성이 정적이어서 메모리의 길이를 변경하는 것이 불가능하다.

연결 리스트는 메모리의 동적 할당 가능

malloc 함수와 free 함수를 통해 메모리 동적 할당을 하는 C 언어와는 달리 파이썬은 메모리의 할당과 해제가 파이썬 인터프리터에 의해 자동으로 관리된다.

특정 데이터를 찾기 위한 순차 탐색에 있어 탐색 속도가 배열에 비해 느리다.

- 노드
    - 필요할 때마다 바구니를 하나씩 마련해서 그곳에 데이터를 저장하고 이들을 배열처럼 서로 연결
    - ‘데이터를 저장할 장소’와 ‘다른 변수를 가리키기 위한 장소’가 구분되어 있다

```python
# 노드 객체
class Node:
    def __init__(self, item):
        self.data = item
        self.next = None

# 연결 리스트 객체
class LinkedList:
    def __init__(self):
        self.head = Node('head')
        
    def find(self, item):
        cur_node = self.head
        while cur_node.data != item:
            cur_node = cur_node.next
        return cur_node
    
    def insert(self, pos, newNode):
        new_node = Node(newNode)
        cur_node = self.find(pos)
        new_node.next = cur_node.next
        cur_node.next = new_node

    def show(self):
        cur_node = self.head
        while cur_node.next is not None:
            print(cur_node.data, end=' -> ')
            cur_node = cur_node.next
        print(cur_node.data)

    def find_previous(self, item):
        cur_node = self.head
        while (cur_node.next is not None) and (cur_node.next.data != item):
            cur_node = cur_node.next
        return cur_node

    def remove(self, item):
        prev_node = self.find_previous(item)
        if prev_node.next is not None:
            prev_node.next = prev_node.next.next
        
a = LinkedList()
a.insert('head', '1')
a.insert('1', '2')
a.insert('2', '3')
a.insert('3', '4')
a.show()

a.remove('2')
a.remove('4')
a.show()
```

# 04-2 단순 연결 리스트의 ADT와 구현

## 정렬 기능이 추가된 연결 리스트의 ADT

```python
def __Init__(self): # 초기화
def getAt(self, pos): # 특정 값이 어디에 있는지 찾음
def insert(self, pos, newNode): # pos 위치에 값 삽입
def popAt(self, pos): # pos 위치의 값 반환 후 삭제
def sortList(self, head: Node)->Node: # 정렬
```

💡 새 노드를 추가할 때, 리스트의 머리와 꼬리 중 어디에 저장할 것인가

**머리에 추가할 경우**

장점 → 변수 tail 불필요

단점 → 저장된 순서를 유지하지 않는다.

**꼬리에 추가할 경우**

장점→ 저장된 순서가 유지된다.

단점 → 변수 tail 필요

tail의 관리를 생략하기 위해 머리에 추가

## 더미 노드 기반 연결 리스트


유효한 데이터를 지니지 않는 그냥 빈 노드

리스트 맨 앞에 위치하므로, head가 항상 더미 노드를 가리키고 있다.

더미 노드에 데이터는 저장되어 있지 않다.

**더미 노드가 없는 경우,** 리스트가 비어 있으면 head.next와 같은 참조가 불가능하므로 리스트가 비어 있는 경우와 그렇지 않은 경우로 나누어 연산을 구현해야 한다.

**더미 노드를 추가한다면,** NULL 값을 가질지언정 항상 head.next의 참조가 가능하므로 경우를 나누지 않고 일관되게 연산을 구현할 수 있다

```python
class DummyLinkedList:
```

# 04-3 연결 리스트의 정렬 삽입의 구현

```python
def sortList_(head: Node)->Node:
    p = head
    lst: list= []
		while p:
        lst.append(p.data)
        p = p.next
		
		lst.sort()
		
		p = head
		for i in range(len(lst)):
        p.data = lst[i]
        p = p.next
		return head
```

- lst에 연결 리스트의 요소들을 넣고 내장함수 `sort()` 를 이용해 정렬해준다
- `p = head` 로 연결 리스트를 초기화한 다음, 리스트에 저장된 요소들을 연결 리스트로 이어준다.

# 2022.10.05(수)

# 05-1 원형 연결 리스트

## 원형 연결 리스트

마지막 노드가 첫 번째 노드를 가리켜서 연결의 형태가 원을 이루는 구조의 연결 리스트


노드를 리스트의 머리에 추가하든지 꼬리에 추가하든지 비슷하다.

포인터 변수 head가 무엇을 가리키는지의 차이만 있다.

## 변형된 원형 연결 리스트

하나의 포인터 변수가 꼬리를 가리키게 한 원형 연결 리스트

꼬리를 가리키는 포인터 변수 하나만 있어도 머리 또는 꼬리에 노드를 간단히 추가할 수 있다.

꼬리를 가리키는 변수 👉 tail

머리를 가리키는 변수 👉 tail.next

```python
class CList:
    class Node:
        def __init__(self, item, link):
            self.item = item
            self.next = link

    def __init__(self):
        self.tail = None
        self.nodeCount = 0

    def is_empty(self):
        return self.nodeCount == 0

    def insert(self, item):
        new = self.Node(item, None)
        if self.is_empty(): # 연결리스트가 비어 있는 경우
            new.next = new
            self.tail = new
        else:
            new.next = self.tail.next
            self.tail.next = new
        self.nodeCount += 1

    def delete(self):
        if self.is_empty():
            print('Underflow')
        x = self.tail.next
        if self.nodeCount == 1: # 연결리스트에 노드가 1개인 경우
            self.tail = None
        else:
            self.tail.next = x.next
        self.nodeCount -= 1
        return x.item

    def show(self):
        if self.is_empty():
            print('리스트 비어 있음')
        else:
            first = self.tail.next
            p = first
            while p.next != first: # 첫 노드를 다시 방문하면 루프 중단
                print(p.item, '-> ', end='')
                p = p.next
            print(p.item)

c = CList()
c.insert('1')
c.insert('2')
c.insert('3')
c.insert('5')
c.show()

c.delete()
c.show()
```


# 05-2 양방향 연결 리스트

## 양방향 연결 리스트

하나의 노드가 자신의 왼쪽과 오른쪽 노드를 동시에 가리키는 구조

- 장점

이전 노드의 주소를 알고 있으므로 마지막 노드를 삭제하는 경우 그 전 노드(previous)를 알기 위해 처음부터 탐색할 필요 없이 바로 삭제할 수 있다.

- 단점

링크를 한 개 더 가지므로 복잡하다.

# 2022.10.06(목)

# 06-1 스택의 이해와 ADT 정의

## 스택의 이해

먼저 들어간 것이 나중에 나온다

후입선출(LIFO, Last-In First-Out) 방식의 자료구조

예) 쌓아 올려진 상자더미, 쟁반 위에 쌓인 접시

## 스택 ADT의 정의

```python
def __init__(self): # 스택 초기화

def is_empty(self): # 스택이 빈 경우 True(1)를, 그렇지 않은 경우 False(0)를 반환

def push(self, item): # 스택에 데이터를 저장

def pop(self): # 마지막에 저장된 요소를 삭제하고 반환

def show(self): # 스택에 있는 데이터 보여줌
```

배열과 연결 리스트를 이용하여 구현할 수 있다.

# 06-2 스택의 배열 기반 구현

삽입과 삭제가 일어나는 끝은 Top, 반대편 끝은 Bottom

- push: Top을 위로 한 칸 올리고, Top이 가리키는 위치에 데이터 저장
- pop: Top이 가리키는 데이터를 반환하고, Top을 아래로 한 칸 내림

파이썬은 배열을 리스트로 제공함

```python
s = []
for i in range(5):
	s.append(i)
print(s)
print(s.pop())
print(s.pop())
print(s)
```
# 06-3 스택의 연결 리스트 기반 구현

```python
class Node:
    def __init__(self, item, next):
        self.item = item
        self.next = next

class Stack:
    def __init__(self):
        self.last = None

    def is_empty(self):
        if self.last == None:
            return True
        else:
            return False

    def push(self, item):
        self.last = Node(item, self.last)

    def pop(self):
        item = self.last.item
        self.last = self.last.next
        return item

    def show(self):
        if self.is_empty():
            print('스택 비어 있음')
        else:
            l=[]
            cur_node = self.last
            while cur_node.next is not None:
                l.append(cur_node.item)
                cur_node = cur_node.next
            l.append(cur_node.item)
            print(list(reversed(l)))

s = Stack()
for i in range(5):
    s.push(i)
s.show()
print(s.pop())
print(s.pop())
s.show()
```

# 06-4 계산기 프로그램 구현

## 수식의 표기법: 중위, 전위, 후위

중위 표기법(infix notation) 예) 5 + 2 / 7

전위 표기법(prefix notation) 예) + 5 / 2 7

후위 표기법(postfix notation) 예) 5 2 7 + /

- 전위 표기법이나 후위 표기법의 수식은 연산자의 배치순서에 따라서 연산 순서가 결정됨
    
    → 이 두 표기법의 수식을 계산하기 위해서 연산자의 우선순위를 알 필요가 없다.
    
- 소괄호도 삽입되지 않음
    
    →소괄호에 대한 처리도 불필요하다.
    

<aside>
💡 계산기 사용자가 중위 표기법의 수식을 입력하면 그 수식을 전위나 후위 표기법의 수식으로 변환

</aside>

## 중위 표기법을 후위 표기법으로 바꾸는 방법

1. 중위 표기법의 수식을 후위 표기법의 수식으로 바꾼다.
    1. 피연산자는 그냥 옮긴다.
    2. 연산자는 스택으로 옮긴다.
    3. 연산자가 스택에 있다면 우선순위를 비교하여 처리방법을 결정한다.
        1. 스택에 위치한 연산자의 우선순위가 높다면, 스택의 연산자를 거내 변환된 수식이 위치한 자리로 옮긴다. 새 연산자는 스택으로 옮긴다.
        2. 스택에 위치한 연산자의 우선순위가 낮다면, 스택에 위치한 연산자의 위에 새 연산자를 쌓는다.
        3. ( 연산자는 ) 연산자가 등장할 때까지 쟁반에 남아서 소괄호의 경계를 구분하는 도구로 사용되어야 한다. ( 연산자의 우선순위는 어떤 사칙 연산자들보다 낮다.
    4. 마지막까지 스택에 남아있는 연산자들은 하나씩 꺼내서 옮긴다.
2. 후위 표기법으로 바뀐 수식을 계산하여 그 결과를 얻는다.

```Python
def get_token_list(expr): # 연산을 쪼개서 리스트에 입력
    temp = []
    result = []
    num = str()

    for i in expr:
        if i == "+" or i =="-" or i == "*" or i == "/" or i == "(" or i == ")":
            for j in temp:
                num = num + j
            if num != "": # 공백 들어가는 것 방지
                result.append(float(num))
            result.append(j)
            temp = []
            num = ""
        else: # 두자리 이상 숫자는 문자열 덧셈으로 처리
            temp.append(i)
    for k in temp:
        num += k
    result.append(float(num))
    return result

def infix_to_postfix(prob, opStack, outStack):
    for i in prob:
        if i == "*" or i == "/" or i == "(": # 우선순위가 높은 연산자는 그냥 들어감
            opStack.push(i)
        elif i == "+" or i =="-":
            if opStack.len_stack() == 0: #opStack에 하나도 없으면 그냥 추가함
                opStack.push(i)
            else:
                for j in range(opStack.len_stack()): # 우선순위가 낮은 게 들어오면 높은 연산자를 opStack에 빼버림
                    if opStack.top() == "*" or opStack.top() == "/":
                        outStack.append(opStack.top())
                        opStack.pop()
                    opStack.push(i)
        elif i == ")": # 여는 괄호가 나올 때까지 ㅔㅐㅔ
            while (opStack.top() != "("):
                outStack.append(opStack.top())
                opStack.pop()
            opStack.pop()
        else: # 연산자가 아닌 경우 outStack에 추가
            outStack.append(i)
    while (opStack.len_stack() != 0):
        outStack.append(opStack.top())
        opStack.pop()

def compute_postfix(outStack):
    temp = Stack()

    for i in outStack:
        if i != "+" or i != "-" or i!= "*" or i != "/": # 연산자가 아니면 temp에 넣음
            temp.push(i)
        else:
            operand1 = temp.top()
            temp.pop()
            operand2 = temp.top()
            temp.pop()
            if (i == "+"):
                temp.push(operand2+operand1)
            elif (i == "-"):
                temp.push(operand2-operand1)
            elif (i == "+"):
                temp.push(operand2*operand1)
            elif (i == "+"):
                temp.push(operand2/operand1)
    return temp.pop()
```

# 2022.10.07(금)

## [Python][백준 1110번] 더하기 사이클
### 나의 풀이
```Python
# N%10*10+(N//10+N%10)%10 중복
import sys
N = int(sys.stdin.readline())
new = N%10*10+(N//10+N%10)%10
cycle = 1 
n = 0
while new != N:
    n = new
    new = n%10*10+(n//10+n%10)%10
    cycle += 1
print(cycle)
```
```Python
import sys
N = int(sys.stdin.readline())
cycle = 0
new = 0
n = N
while new != N:
    new = n%10*10+(n//10 + n%10)%10
    cycle += 1
    n = new
print(cycle)
```
N%10*10+(N//10+N%10)%10처럼 두 번 중복되는 코드를 하나로 줄였다.
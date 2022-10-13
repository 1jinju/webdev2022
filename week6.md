# 2022.10.11(화)

## [Python][백준 4673번] 셀프 넘버

### 틀린 풀이
```Python
# 시간초과
lst=[]
for j in range(1, 10001):
    n = j
    while n <= 10000:
        lst.append(n+sum(list(map(int, str(n)))))
        n=n+sum(list(map(int, str(n))))
        
for i in range(1, 10001):
    if i not in lst:
        print(i)
```

### 맞은 풀이
```Python
lst = []
def solution(n):
    return n + sum(list(map(int, str(n))))

for i in range(1, 10001):
    if solution(i) <= 10000:
        lst.append(solution(i))

for i in range(1, 10001):
    if i not in lst:
        print(i)
```
while 문을 없애서 시간복잡도를 줄였다.

# 2022.10.12(수)

## [Python][백준 1065번] 한수

### 나의 풀이
```Python
def solution(n):
    lst = []
    count = 0
    if n < 100:
        count = n 
    else:
        count += 99
        for i in range(100, n+1):
            lst = list(map(int, str(i)))
            if ((lst[2]-lst[1]) == (lst[1]-lst[0])):
                count += 1
    return count
```
입력 안 받아서 틀렸다.

```Python
def solution(n):
    lst = []
    count = 0
    if n < 100:
        count = n 
    else:
        count += 99
        for i in range(100, n+1):
            lst = list(map(int, str(i)))
            if ((lst[0]-lst[1]) == lst[1]-lst[2]):
                count += 1
    return count

n = int(input())
print(solution(n))
```

# 2022.10.13(목)

## [Python][백준 4344번] 평균은 넘겠지
### 나의 풀이
```Python
import sys
n = int(input())
for i in range(n):
    lst = list(map(int, sys.stdin.readline().split()))
    count = 0
    for j in range(1, lst[0]+1):
        if lst[j]>((sum(lst)-lst[0])/lst[0]):
            count += 1
    print("{:.3f}".format(count/lst[0]*100), '%', sep='')
```
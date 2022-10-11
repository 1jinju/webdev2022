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

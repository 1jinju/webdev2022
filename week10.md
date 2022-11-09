# 2022.11.07(월)

## [Python][백준 10809번] 알파벳 찾기

```Python
s = input()
alpha = []
for i in range(97, 123):
    alpha.append(chr(i))
    
for i in alpha:
    if i in s:
        print(s.index(i), end=' ')
    else:
        print(-1, end=' ')
```

# 2022.11.08(화)
## [Python][백준 2675번] 문자열 반복
```Python
t = int(input())
lst = []
for i in range(t):
    s = input().split()
    lst = list(s[1])
    for i in range(len(lst)):
        lst[i] = lst[i] * int(s[0])
    lst = ''.join(lst)
    print(lst)
    lst = []
```
# 2022.11.09(수)
## [Python][백준 8958번] OX퀴즈
```Python
import sys
n = int(input())
count = 0
score = 0
for i in range(n):
    count = 0
    score = 0
    a = sys.stdin.readline()
    for j in a:
        if j == "O":
            count += 1
        else:
            score += count*(count+1)//2
            count = 0   
    print(score)
```
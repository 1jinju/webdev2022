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
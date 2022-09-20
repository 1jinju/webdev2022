# 2022.09.19(월)

## [Python][프로그래머스 Lv.2] 이진 변환 반복하기

### 나의 풀이
```Python
def solution(s):
    re = 0
    zero = 0
    while s != "1":
        zero += s.count("0")
        s = s.replace("0","")
        s = str(bin(len(s))[2:])
        print(s)
        re += 1
    return [re, zero]
```
처음엔 재귀로 풀려다가 안 돼서 반복문으로 풀었다.
재귀를 쓸 때엔 함수의 인자와 return 값의 구조가 비슷해야 한다는 것을 알게 되었다.

s.count("0")로 문자열 s 안의 0의 개수를 zero에 더해주고,
replace 함수로 s의 모든 0을 제거한다.
s의 길이을 2진법으로 변환한 후 문자열로 바꾼다. - str(bin(len(s)))
그런데 bin 함수를 사용해서 2진법으로 변환하면 앞에 0b가 붙으므로 문자열 슬라이싱을 해주었다.

위 과정을 s가 1이 될 때까지 반복해주었다.

### 나의 풀이

```Python
def solution(s):
    a, b = 0, 0
    while s != '1':
        a += 1
        num = s.count('1')
        b += len(s) - num
        s = bin(num)[2:]
    return [a, b]
```
0, 1로만 이루어진 문자열이므로 len(s)에서 문자열 내 1의 개수를 빼면 사라질 0의 개수가 나온다.
나머지는 비슷하다.


# 2022.09.20(화)

## [Python][백준 2525번] 오븐 시계

### 틀린 풀이
```Python
h, m = map(int, input().split())
c = int(input())
count = 0

while c > 60:
    c %= 60
    count += 1

c_hour = count

if h+c_hour < 24 and m+c < 60:
    print(h+c_hour, m+c, sep=' ')
elif h+c_hour >= 24 and m+c < 60:
    print(h+c_hour-24, m+c, sep=' ')
elif h+c_hour >= 24 and m+c >= 60:
    print(h+c_hour-23, m+c-60, sep=' ')
else:
    if h+c_hour+1 >=24:
        print(h+c_hour-23, m+c-60, sep=' ')
    else:
        print(h+c_hour+1, m+c-60, sep=' ')
```
c를 60으로 나눈 몫을 c_hour에 저장하고, 60으로 나눈 나머지를 c에 저장했어야 했는데 잘못 풀었다.

### 맞은 풀이
```Python
h, m = map(int, input().split())
c = int(input())

minute = m+c

while minute >= 60:
    minute -= 60
    h += 1
if h >= 24:
    print(h-24, minute)
else:
    print(h, minute)
```
minute이 60보다 작을 때까지 계속 60을 빼주고, 빼줄 때마다 h에 1을 더해준다.
위의 풀이보다 보기 편해졌다. 
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

# 2022.09.21(수)
## 01-1 자료구조에 대한 기본적인 이해

### 자료구조

- 자료구조:  데이터를 표현하고 저장하는 방법
- 자료구조의 분류
    - 선형구조
        - 리스트
        - 스택
        - 큐
    - 비선형구조
        - 트리
        - 그래프
    - 파일구조
        - 순차파일
        - 색인파일
        - 직접파일
    - 단순구조
        - 정수
        - 실수
        - 문자
        - 문자열

### 자료구조와 알고리즘

- 알고리즘
    
    표현 및 저장된 데이터를 대상으로 하는 문제의 해결 방법
    
    <aside>
    💡 자료구조가 결정되어야 그에 따른 효율적인 알고리즘 결정 가능
    
    </aside>


## 01-2 알고리즘의 성능분석 방법

### 시간복잡도와 공간복잡도

- 공간복잡도: 메모리 사용량에 대한 분석결과
- 시간복잡도
    
    속도에 해당하는 알고리즘의 수행시간 분석결과
    
    처리해야 할 데이터의 수 n에 대한 연산횟수의 함수 T(n)을 구성
    

### 순차탐색 알고리즘의 시간복잡도

```c
for (i = 0; i < len; i++) { 
	if (ar[i] == target)
		return i;
}
```

탐색 알고리즘에서의 핵심은 동등비교를 하는 비교연산에 있다.

- 최선의 경우
    
    찾고자하는 값이 맨 앞에 있는 경우
    
- 최악의 경우
    
    $$
    T(n)=n
    $$
    
    찾고자 하는 값이 배열의 맨 마지막에 저장되어 있거나 아예 저장되어 있지 않은 경우
    
    알고리즘 성능을 판단하는데 중요
    
- 평균적인 경우

$$
T(n)=n*3/4
$$

     탐색 대상이 배열에 존재하지 않을 확률 50%라고 가정

탐색 대상이 존재하지 않는 경우의 연산 횟수: n

탐색 대상이 존재하는 경우의 연산 횟수 n/2

계산하기 어려움

### 이진 탐색 알고리즘

정렬된 데이터가 아니면 적용이 불가능하다

1. 배열의 중앙에 찾는 값이 저장되어 있는지 확인한다.
2. 찾는 값이 배열의 중앙에 있는 값보다 크면 탐색의 범위를 배열의 왼쪽 부분으로 제한한다.
3. 찾는 값이 배열의 중앙에 있는 값보다 작으면 탐색의 범위를 배열의 오른쪽 부분으로 제한한다
    
    2, 3번👉탐색의 대상을 반으로 줄임
    
- 이진 탐색 알고리즘의 구현

```c
int BSearch(int ar[], int len, int target) {
	int first = 0;
	int last = len - 1;
	int mid;
	while (first <= last) { // 탐색의 대상이 존재함
		mid = (first + last) / 2;
		if (target == ar[mid]) {
			return mid;
		}
		else {
			if (target < ar[mid])
				last = mid - 1;
			else
				first = mid + 1;
		}
		return -1;
}
```

- 최악의 경우
    
    $$
    T(n)=log 2 (n)
    $$
    
    n이 1이 되기 까지 2로 나눈 횟수가 k회, 비교연산 k회 진행
    
    데이터가 1개 남았을 때 마지막을 비교연산 1회 진행
    
    👉T(n)=k+1
    
    👉n*(1/2)^k=1이므로 k=log2(n)
    

### 빅오표기법

함수 T(n)에서 가장 영향력이 큰 부분이 어딘가를 따지는 것  
$$  
O(1)<O(logn)<O(n)<O(nlogn)<O(n^2)<O(n^3)<O(2^n)
$$  

# 2022.09.22(목)
## 02-1 함수의 재귀적 호출의 이해
### 재귀

- 재귀함수: 함수가 호출되면 해당 함수의 복사본을 만들어서 실행하는 구조

```c
void Recursive(int num) {
	if (num <= 0) // 재귀의 탈출 조건
		return;
	printf("Recursive call! %d \n", num);
	Recursive(num-1);
}
```

### 팩토리얼

$$
n! = n*(n-1)*(n-2)*...*2*1
$$

(n-1)! = (n-1) * (n-2) * (n-3) * ... * 2 * 1

$$
n! = n*(n-1)!
$$

| f(n) | n * f(n-1) | n ≥ 1 |
| --- | --- | --- |
|  | 1 | n = 0 |

```c
int Factorial(int n) {
	if (n == 0) // 탈출조건
		return 1;
	else
		return n * Factorial(n-1);
}
```


## 02-2 재귀의 활용

### 피보나치 수열

앞의 것 두 개를 더해서 현재의 수를 만들어가는 재귀적인 형태를 띠는 대표적인 수열

| fib(n) | 0 | n=1 |
| --- | --- | --- |
|  | 1 | n=2 |
|  | fib(n-1) + fib(n-2) | otherwise |

```c
int Fibo(int n) {
	if (n == 1)
		return 0;
	else if (n == 2)
		return 1;
	else
		return Fibo(n-1) + Fibo(n-2);
}
```
재귀함수는 많은 수의 함수 호출을 동반

### 이진 탐색 알고리즘의 재귀적 구현

- 동일한 패턴 반복(재귀적인 성격)
    1. 탐색 범위의 중앙에 목푯값이 저장되었는지 확인
    2. 저장되지 않았다면 탐색 범위를 반으로 줄여서 다시 탐색 시작
- 탈출조건
    
     탐색 범위의 시작위치 first가 탐색 범위의 끝 last보다 커지는 경우
    

```c
int BSearchRecur(int ar[], int first, int last, int target) {
	int mid;
	if (first > last)
		return -1;
	mid = (first + last) / 2;

	if (ar[mid] == target)
		return mid;
	else if (target < ar[mid])
		return BSearchRecur(ar, first, mid-1, target)
	else
		return BSearchRecur(ar, mid+1, last, target)
}
```

---

## 02-3 하노이 타워

하나의 막대에 쌓여 있는 원반을 다른 하나의 원반에 그대로 옮기는 방법

원반은 한 번에 하나씩만 옮길 수 있다.

옮기는 과정에서 작은 원반의 위에 큰 원반이 올려져서는 안 된다.

### 반복 패턴(재귀적으로 구성)

1. 작은 원반 n-1개를 A에서 B로 이동
2. 큰 원반 1개를 A에서 C로 이동
3. 작은 원반 n-1개를 B에서 C로 이동

탈출조건: 이동해야 할 원반의 수가 1개인 경우

👉 원반 n개를 이동하는 문제는 결국 원반 1개를 이동하는 매우 쉬운 문제로 세분화

```c
void HanoiTowerMove(int num, char from, char by, char to) {
	if (num == 1) {
		printf("원반1을 %c에서 %c로 이동 \n", from, to);
	}
	else{
		HanoiTowerMove(num-1, from, to, by)
		printf("원반 %d을(를) %c에서 %c로 이동 \n", num, from, to);
		HanoiTowerMove(num-1, by, from, to);
	}
}
```

- 파이썬

```python
def HanoiTowerMove(num, fr, by, to):
    if num == 1:
        print("원반 1을 %c에서 %c로 이동" %(fr, to))
    else:
        HanoiTowerMove(num-1, fr, to, by)
        print("원반 %d을(를) %c에서 %c로 이동" %(num, fr, to))
        HanoiTowerMove(num-1, by, fr, to)

HanoiTowerMove(3, 'A', 'B', 'C')
```
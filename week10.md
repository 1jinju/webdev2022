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

# 2022.11.10(목)

## 컴퓨터일반 5장
### 저급언어와 고급언어

- 저급 언어(Low Level Language)
    - 하드웨어 지향의 컴퓨터 내부 표현에 가까운 언어로, 기계어와 어셈블리어로 구분된다.
    - 기계어(Machine Language): 2진수 형태의 0과 1로 작성하며 컴퓨터가 직접 이해할 수 있는 언어
    - 어셈블리어(Assembly Language): 기계어 명령을 간단한 기호로 표현한 언어, 기계어보다 사용하긴 편하지만 기계어인 0과 1의 집합을 문자나 기호로 바꾼 것이어서 언어 형태에 익숙한 사람이 아니면 사용하기 어렵다
- 고급 언어(High Level Language)
    - 저급 언어의 단점을 해결하기 위해 개발된 언어, 사람이 이해하기 쉬운 일상 언어와 기호를 사용해 프로그램을 작성한다
    - 저급 언어보다 자연어에 가까운 구문 규칙을 갖고 있어 이식성이 높다
    - 예) C, 자바, 파이썬, 포트란, 코볼, 파스칼, C++ 등

### 컴파일러와 인터프리터

- 컴파일러(Compiler)
    - 프로그램 전체 소스코드를 기계어로 한번에 번역해 실행 파일을 만든 뒤 프로그램을 실행하는 방식
    - 소스 전체를 개체 파일로 번역하는 과정은 컴파일이라고 부른다.
    - C, 자바 등이 컴파일러 방식을 사용
    - 소스 코드에서 미리 오류를 찾아내므로 실행했을 때 문제가 생길 일이 없음 → 최적화된 작업이 가능하며 실행속도가 빠르다
- 인터프리터(Interpreter)
    - 소스코드를 한 행씩 읽어 가며 번역과 실행을 동시에 수행하는 방식
    - 프로그램이 실행 중일 때 고급 언어로 작성된 소스코드 명령어(Statement)를 하나씩 번역하는 것
    - 파이썬, 자바스크립트 등이 인터프리터 방식을 사용
    - 컴파일러 방식보다 속도가 느리지만, 즉각적인 피드백이 가능

# 2022.09.05(월)
## 분산 대 탈중앙화

- 블록체인은 탈중앙화 시스템

<img src="./img/분산과 탈중앙화.png">

- 분산 시스템
    - 여러 서버가 일을 나눠 처리함으로써 작업의 효율성이나 서비스의 가용성을 높이는 것
    - 중앙 서버 하나만 고장나도 모든 서비스가 중단되는 것을 방지하여 가용성을 높임
- 탈중앙화 시스템
    - 여러 서버가 동일한 일을 중복해 처리
    - 더 많은 자원과 시간이 투입되지만, 일을 중복하기 때문에 효율성이 극도로 저하됨
    - 일의 결과에 대한 신뢰도 향상
    - 네트워크 내의 모든 노드가 동등
        - 특정 역할을 수행하는 서버가 없음 → 해커가 공격대상으로 삼을 만한 목표가 사라짐
        - 대다수의 노드를 점령해야만 네트워크를 사유화할 수 있으므로 그러한 시도로부터 비교적 자유로움

## 암호 화폐, 가상 화폐, 거래소 등

### 디지털 화폐 대 암호 화폐

- 디지털 화폐: 유통 화폐를 디지털화한 것
- 암호 화폐
    - ‘실험적 가상 화폐 중 익명성을 보장하기 위한 기술이 들어가 있는 것’을 지칭하던 말
        
        → 비트코인의 등장 이후 예외 없이 ‘블록체인을 기반으로 만들어진 실험적 화폐를 가리키는 의미’로 고착돼 사용
        
    - 절대적인 익명성을 가짐

### 암호 화폐 대 토큰

- 암호 화폐
    - 자발적인 네트워크가 형성된 후 충분한 채굴자 집단을 구성해 지속적인 채굴 노동을 제공해야 운영할 수 있음
    - 네트워크를 운영할 참여자를 모집하고 일정 이상의 채굴 집단을 형성해 안정성을 확보하는 것이 힘듦
    
    <img src="./img/암호 화폐.jpg">
    
- 토큰
    - 이더리움의 스마트 컨트랙트를 사용하면 별도의 네트워크를 구성하지 않고도 암호 화폐를 새로 발행할 수 있음
    - 스마트 컨트랙트를 이용해 발행한 암호 화폐
    - ERC-20, ERC-721 등의 표준

## 노드, 피어, 트랜잭션

<img src="./img/네트워크의 그래프식 표현.jpg">

- 노드
    - 그래프상에서 둥근 원으로 표현된 각 꼭짓점
    - 컴퓨터를 의미함
- 피어
    - 노드 중 가지를 통해 서로 직접 연결된 노드들

> 노드: A, B, C, …
피어: A-C, A-B, E-C, E-F, …
> 

- 트랜잭션
    - 정의된 이벤트가 발생하는 것
    - 비트코인에서의 이벤트: 비트코인을 주고받는 거래
    - 이더리움에서의 이벤트: 이더리움을 주고받거나 스마트 컨트랙트로 정의한 어떤 행위를 호출하는 것

## 블록

<img src="./img/블록 구조.png">

- 블록은 일반적으로 블록 헤더, 블록 데이터, 블록 검증 데이터로 이루어진다.
- 블록 헤더는 블록 번호, 블록 생성 시각, 블록 데이터의 해시값, 그리고 이전 블록 헤더의 해시값을 포함한다.
- 블록 데이터는 다수의 트랜잭션을 포함한다.
- 블록 검증 데이터는 블록을 생성하는 개체의 공개키와 전자 서명 값을 포함한다.

## 블록체인의 기본 작동 원리

<img src="./img/트랜잭션의 처리 방식.jpg">

- 중앙화 시스템
    - A는 은행에 접속한 후 계좌 이체 요청서를 작성하고 은행 서버에 제출
    - 은행 중앙 서버에 의해 안전하게 저장
    - 누가 거래를 기록하고 저장할 것인지 정해져 있음
- 블록체인
    - 중앙서버가 존재하지 않으므로 누가 처리할 것인지 정해져 있지 않고 매번 바뀜
    - 브로드캐스팅 또는 가십 프로토콜: 블록체인에서는 기본적으로 모든 거래 내역서를 전체 참여자에게 알려야 함

# 2022.09.06(화)
## Vincent Driessen의 브랜칭 모델

<img src="./img/git-flow.png">

Vincent Driessen의 브랜칭 모델에는 5개의 브랜치가 사용된다.

- master
- develop
- feature
    - 새로운 기능 개발이나 버그 수정을 위한 일련의 코드 수정이 이뤄지는 브랜치다. 이 브랜치에서 개발자 혼자 작업을 할 수도 있고, 특정 기능 개발을 위한 여러명의 개발자들이 공동으로 작업할 수도 있다.
    - feature 브랜치에서 작업된 내용은 최종적으로 PR을 거쳐 develop 브랜치에 병합(Merge)된다.
- release
- hotfix

## **git-flow 사용법**

```python
$ git clone [repo url]

//git 저장소를 git-flow에 맞게 초기화
$ git flow init -d

//develop 브랜치에서 feature/[기능 이름] 브랜치를 만들고 이동
$git checkout -b feature/[기능 이름] develop

//기능 개발 완료 후(develop ← feature 병합 후 브랜치 삭제)
$ git flow feature finish <branch_name>

//원격 저장소 반영
$ git push origin master
```

<aside>
💡 소스트리 사용

[0원으로 현업 환경을 설정해보자! Git Flow(Sourcetree) (tistory.com)](https://hucet.tistory.com/89#:~:text=git%20flow%20%EB%A5%BC%20%EC%B4%88%EA%B8%B0%ED%99%94%20%ED%95%98%EA%B8%B0%20%EC%9C%84%ED%95%B4%EC%84%A0%20%EC%95%84%EB%9E%98%20%EA%B8%B0%EB%8A%A5%EC%9D%84,%EC%A0%80%EC%9E%A5%EC%86%8C%20%EC%B4%88%EA%B8%B0%ED%99%94%EB%A5%BC%20%EC%8B%A4%ED%96%89%ED%95%98%EB%A9%B4%20%EC%95%84%EB%9E%98%EC%99%80%20%EA%B0%99%EC%9D%B4%20develop%20%EB%B8%8C%EB%9E%9C%EC%B9%98%EA%B0%80%20%EC%83%9D%EC%84%B1%EB%90%A9%EB%8B%88%EB%8B%A4.)

</aside>


# 2022.09.07(수)
## [Python][프로그래머스 Lv.1] 예산
### 나의 풀이

```Python
def solution(d, budget):
    answer = 0
    d.sort()
    for i in range(len(d)):
        budget -= d[i]
        if budget >= 0:
            answer += 1
        else:
            return answer
    return len(d)
```
sort() 함수는 리스트를 오름차순으로 정렬해주는 함수이다.

budget에서 d[i]를 뺀 후 0보다 크거나 같으면 예산이 부족하지 않아 부서에 물품 지원이 가능한 것이므로 answer에 1을 더해주고, 0보다 작으면 answer를 return해준다.

for 문을 다 돌았는데도 return되지 않으면 모든 부서의 물품을 구매해준 것이므로 부서 d의 길이를 return해준다.

### 다른 사람의 풀이

```Python
def solution(d, budget):
    d.sort()
    while budget < sum(d):
        d.pop()
    return len(d)
```

sort()로 정렬해준 후 d의 합이 budget보다 작거나 같아질 때까지 d에서 pop해준다.

d의 합이 budget보다 작거나 같아지면 while 문을 빠져나와 d의 길이를 return해준다.


보기 좋지만, 신청한 부서가 많고 예산이 적으면 부담이 되는 코드이다.
sum()이 반복되어 시간 복잡도가 O(n^2)이므로 매번 원소 값을 하나씩 빼는 (O(n)) 풀이가 나을 것 같다.


# 2022.09.08(목)
## [Python][프로그래머스 Lv.1] 콜라츠 추측

### 나의 풀이
```Python
def solution(num):
    answer = 0
    while num != 1:
        if num % 2 == 0:
            num /= 2
        else:
            num = num * 3 + 1
        answer += 1
        if answer == 500:
            return -1
    return answer
```
조건에 맞게 짝수이면 2로 나눠주고, 홀수이면 3을 곱한 후 1을 더해주는 작업을 num이 1이 될 때까지 반복하였다.
while 문을 반복하다가 answer이 500이 되면 -1을 return해준다.

 

### 다른 사람의 풀이
```Python
def collatz(num):
    for i in range(500):
    	if num == 1:
            return i
        num = num / 2 if num % 2 == 0 else num*3 + 1   
    return -1
```
for 문을 통해 500번 반복하는데, num이 1이면 i를 return하고 그렇지 않으면 위의 작업을 해주는 식이다.
500번 반복이 끝나도 1이 되지 않으면 -1을 return해준다.

 

```Python
def collatz(num):
    for i in range(500):
        num = num / 2 if num % 2 == 0 else num*3 + 1
        if num == 1:
            return i + 1
    return -1
```
이게 원래 코드였는데 i+1을 return하는 게 별로인 것 같아서 if 문을 위로 올려 i를 return하게 하였다.

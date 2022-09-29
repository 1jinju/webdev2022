# 2022.09.27(화)

# 1-1. 공간 혁명과 임베디드 시스템

## 1. 새로운 시대와 변화

### <거시적(크게) 관점의 사회 변화>

- 산업(공장, 제조) 사회에서 스마트(온라인, 지능적) 사회로
- 4차산업혁명(대량생산에서 맞춤생산)
- 디지털 트랜스포메이션(의자→안마기)

### <미시적(좁게) 관점의 사회 변화>

- 하드웨어에서 소프트웨어 중심
- 오프라인에서 온라인 중심
- 소유에서 공유(Socar, o2o(offline to online))

## 2. 공간 개념의 변화

### <현재 제 3공간(임베디드 기반 스마트 공간) 시대 도래>

- 인류는 공간개척의 노력과 그 위에 꽃피운 공간혁명의 역사

1. **제 1, 2차 공간혁명**
    1. 인터넷 혁명 이전
    2. 인류발전 무대는 물리공간 중심이었음
    
    
2. **제 3차 공간혁명(사이버 공간)**
    1. 인터넷 혁명 이후(AIR)
    2. 또 하나의 생존 공간인 “전자공간”을 획득함
        
3. **제 4차 공간혁명(초 공간=스마트 공간)**
    1. “제 3 공간” 초 공간이며 스마트 공간 생성    
    2.  보이지 않는 컴퓨터에 의한 사물들의 지능화


### <제 4차 공간 혁명의 제 3 공간에서 임베디드 시스템>

- 기계나 기타 제어가 필요한 시스템 제어와 모니터링을 위해 특정 기능을 수행하는 컴퓨터 시스템
- 전체 장치의 일부분으로 구성되며 제어와 모니터링이 필요한 시스템을 위한 두뇌 역할을 하는 특정 목적의 컴퓨터 시스템
- 어떤 특정한 기능을 위해 특화된 시스템(1940-1990년, 현관문 OPEN)
- 특별한 목적으로 설계된 하드웨어를 제어하기 위한 시스템으로 그 내부에 컴퓨터가 내장된(embedded) 시스템

# 2022.09.28(수)

## [Python][백준 2480번] 주사위 세개

### 틀린 풀이
```Python
a, b, c = map(int, input().split())
max = a

def num_same(a, b, c):
	# 모두 다를 때
	if a != b and b != c and a != c:
		return 1
	# 두 개가 같을 때
	elif (a==b and b!=c) or (b==c and a!=c) or (a==c and b!=c):
		return 2
	# 모두 같을 때
	elif a==b and b==c:
		return 3
		
if num_same(a,b,c) == 1:
	if b > max:
		b = max
	if c > max:
		c = max
	print(max*100)
elif num_same(a,b,c) == 2:
	if (a==b and b!=c) or (a==c and b!=c):
		print(1000+a*100)
	elif b==c and a!=c:
		print(1000+b*100)
elif num_same(a,b,c) == 3:
	print(10000+a*1000)
```
max에 b를 집어넣어야 했는데 b에 max를 집어넣어서 틀렸다.

### 맞은 풀이
```Python
a, b, c = map(int, input().split())
max = a

def num_same(a, b, c):
	# 모두 다를 때
	if a != b and b != c and a != c:
		return 1
	# 두 개가 같을 때
	elif (a==b and b!=c) or (b==c and a!=c) or (a==c and b!=c):
		return 2
	# 모두 같을 때
	elif a==b and b==c:
		return 3
		
if num_same(a,b,c) == 1:
	if b > max:
		max = b
	if c > max:
		max = c
	print(max*100)
elif num_same(a,b,c) == 2:
	if (a==b and b!=c) or (a==c and b!=c):
		print(1000+a*100)
	elif b==c and a!=c:
		print(1000+b*100)
elif num_same(a,b,c) == 3:
	print(10000+a*1000)
```

# 2022.09.29(목)
# 03-1 추상 자료형

## 자료구조에서의 추상자료형

<aside>
💡 구체적인 기능의 완성과정을 언급하지 않고, 순수하게 기능이 무엇인지를 나열한 것

</aside>

구조체와 관련된 연산의 종류를 결정하는 것도 자료형 정의의 일부로 보아야 함

예) 지갑 구조체 + 그 구조체와 관련된 돈을 꺼내는 연산 ⇒ 자료형의 정의 완성


# 03-2 배열을 이용한 리스트의 구현

## 리스트

- 구현방법에 따라
    
    순차리스트: 배열 기반으로 구현
    
    연결리스트: 메모리의 동적할당 기반으로 구현
    
- 특성
    
    데이터를 나란히 저장한다.
    
    중복된 데이터 저장을 허용한다.
    

## 리스트의 ADT

```c
void ListInit(List *plist);
```

초기화할 리스트의 주소 값을 인자로 전달

리스트 생성 후 제일 먼저 호출되어야 함

```c
void LInsert(List *plist, LData data);
```

리스트에 데이터 저장

매개변수 data에 전달된 값 저장

```c
int LFirst(List *plist, LData *pdata);
```

첫 번째 데이터가 pdata가 가리키는 메모리에 저장됨

데이터의 참조를 위한 초기화

참조 성공 시 TRUE(1), 실패 시 FALSE(0) 반환

```c
int LNext(List *plist, LData *pdata);
```

참조된 데이터 다음 데이터가 pdata가 가리키는 메모리에 저장됨

순차적인 참조를 위해 반복적인 호출이 가능하다

참조를 새로 시작하려면 LFirst 함수를 호출해야 함

참조 성공 시 TRUE(1), 실패 시 FALSE(0) 반환

```c
LData LRemove(List *plist);
```

LFirst 또는 LNext 함수의 마지막 반환 데이터 삭제

삭제된 데이터는 반환됨

연이은 반복 호출을 허용하지 않음

```c
int LCount(List *plist);
```

리스트에 저장되어 있는 데이터 수 반환

- 데이터의 참조 방식

LFirst → LNext → LNext → LNext ...

데이터의 참조위치를 기록하여 LNext 함수를 호출할 때마다 다음에 저장된 데이터를 얻을 수 있다.

처음부터 참조를 새롭게 시작하기 위해서는 LFirst 함수가 필요하다.

## 리스트의 구현

- 헤더파일

```c
typedef struct __ArrayList {
	LData arr[LIST_LEN];
	int numOfData;
	int curPosition;
} ArrayList;

typedef ArrayList List;

void ListInit(List *plist); // 초기화
void LInsert(List *plist, LData data); // 데이터 저장

int LFirst(List *plist, LData *pdata); // 첫 데이터 참조
int LNext(List *plist, LData *pdata); // 두 번째 이후 데이터 참조

LData LRemove(List *plist); // 참조한 데이터 삭제
int LCount(List *plist); // 저장된 데이터의 수 반환
```

- 함수 정의

```c
void ListInit(List *plist) {
	(plist -> numOfData) = 0; // 리스트에 저장된 데이터 수 0
	(plist -> curPosition) = -1; // 현재 아무 위치도 가리키지 않음
}
```

```c
void LInsert(List *plist, LData data) {
	if (plist -> numOfData >= LIST_LEN) {
		puts("저장 불가능");
		return;
	}
	plist -> arr[plist->numOfData] = data; // 데이터 저장
	(plist -> numOfData)++;
}
```

```c
int LFirst(List *plist, LData *pdata) {
	if (plist -> numOfData == 0) // 저장된 데이터가 하나도 없다면
		return FALSE;
	(plist -> curPosition) = 0; // 참조 위치 초기화
	*pdata = plist -> arr[0];
	return TRUE;
}
```

```c
int LNext(List *plist, LData *pdata) {
	if (plist -> curPosition >= (plist -> numOfData) - 1) // 더는 참조할 데이터가 없다면
		return FALSE;
	(plist -> curPosition)++;
	*pdata = plist -> arr[plist->curPosition];
	return TRUE;
}
```

```c
LData LRemove(List *plist) {
	LData rdata = plist -> arr[rpos]; // 삭제할 데이터 임시 저장
	for (i = rpos; i < num - 1; i++) // 데이터 이동
		plist -> arr[i] = plist -> arr[i+1];
	(plist -> numOfData)--;
	(plist -> curPosition)--;
	return rdata;
}
```

중간에 데이터가 삭제되면 뒤의 데이터들을 한칸씩 앞으로 이동시켜 빈 공간을 메워야 한다.

## 리스트에 구조체 변수 저장하기

리스트에 저장한 데이터가 동적으로 할당된 구조체 변수의 주소 값이라면

👉 free 함수를 통한 메모리의 해제 과정을 거쳐야 함

## 배열 기반 리스트의 장점과 단점

- 장점
    
    데이터의 참조가 쉽다.
    
    인덱스 값을 기준으로 어디든 한 번에 참조가 가능하다.
    
- 단점
    
    배열의 길이가 초기에 결정되어야 하고, 변경이 불가능하다.
    
    삭제 과정에서 데이터 이동(복사)이 빈번히 일어난다.
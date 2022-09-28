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
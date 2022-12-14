# 2022.11.21(월)
## 마이크로 프로세서와 마이크로 컨트롤러
### 마이크로 프로세서
- 컴퓨터의 CPU에 해당, 고성능
- 메모리, 입출력 장치 필요
- 적은 수의 레지스터(주로 메모리작업)
- 예) PXA255 프로세서
### 마이크로 컨트롤러
- 임베디드 시스템에 이용
- 상대적으로 저성능
- 내부에 메모리와 입출력장치가 존재 -> 빠른 처리속도
- 많은 수의 레지스터
- 예) 8051 마이크로 컨트롤러(인텔 사, 8비트)

## 플래시메모리
- 전기적으로 데이터를 지우고 다시 기록할 수 있는 기억장치
- 비휘발성 메모리
- usb, SSD 응용

## 입력장치
- 프로그램이나 데이터를 컴퓨터가 인식할 수 있는 부호로 바꾸어 주기억장치로 보내는 장치
- 임베디드 시스템에서는 입력장치로, 센서가 주로 사용

# 2022.11.22(화)
## 출력장치
- 주기억장치에서 데이터를 처리한 결과를 외부에 명령이나 데이터로 전달하는 장치
- 다양한 구동체에 연결

## 임베디드 시스템과 호스트 컴퓨터 연결
### JTAG(Joint Test Access Group>
- 연결 케이블
1. jtag cable: pcb 테스트 목적/플래시메모리에 부트로드 탑재
2. parallel cable: jtag cable과 parallel cable 연결
3. serial cable: 9핀
4. ethernet cross cable: 파일 전송

## 임베디드 시스템의 입출력 장치 제어
### 1. 메모리 맵 방식
- ARM, MIPS, powerPC 등
- 프로세스가 I/O장치를 액세스할 때, 메모리의 일부를 입출력장치로 사용
### 2. I/O 맵 방식
- x63계열
- 메모리 영역과 별도의 I/O 영역이 존재함
- 메모리 번지와 I/O 번지를 구분하는 신호가 존재함

# 2022.11.23(수)
## 화소 점 처리
- 원 화소의 값이나 위치를 바탕으로 단일 화소 값을 변경하는 기술
- 다른 화소의 영향을 받지 않고 단순히 화소 점의 값만 변경하므로 포인트 처리(Point Processing)라고도 함
- 산술연산, 논리연산, 반전, 광도 보정, 히스토그램 평활화, 명암 대비 스트레칭 등의 기법이 있음

## 산술 연산
디지털 영상의 산술연산은 디지털 영상의 각 화소 값에서 임의의 상수 값으로 덧셈, 뺄셈, 곱셈, 나눗셈을 수행하는 것    
그레이 레벨 영상에서 화소 값이 작으면 영상이 어둡고, 화소의 값이 크면 밝음    
- 곱셈연산: 밝은 부분은 더욱 밝아지고, 어두운 부분은 약간 밝아져 영상 내 밝기에 커다란 차이가 생김 -> 선명도 증가
- 나눗셈연산: 최대 밝기와 최소 밝기의 차이가 작아짐

## 클래핑(Clamping) 기법
- 연산의 결과 값이 최소값보다 작으면 그 결과값을 최소값으로, 최대값보다 크면 결과 값을 최대값으로 하는 기법
- 8비트 그레이 영상에서 최소값은 0, 최댓값은 255이므로 음수는 0으로 설정하고, 255보다 큰 값은 255로 설정함

# 2022.11.24(목)
## 논리연산
참과 거짓을 판별하는 연산    
화소의 상수 값에서 AND, OR, XOR, NOT 등의 연산을 수행하여 디지털 영상에서 차폐, 특징 추출, 형태 분석을 함    
- AND 연산: 원하는 비트를 선택적으로 0으로 만듦(마스크 연산)
- OR 연산: 특정 비트를 선택적으로 1로 구성할 수 있음(선택적 세트 연산)
- XOR 연산(^): 입력이 서로 다를 때만 1을 출력하는 연산으로, 두 데이터를 비교하므로 비교 연산이라고도 함
- NOT 연산: 화소 비트를 반전시키는 일을 함

## 화소 점 처리 기법
- 명암변환: 밝기를 변경하는 것
- 널 변환: 단순히 입력화소를 출력화소로 변환(변화가 없음)
- 반전 변환: 각 화소의 값이 영상 내애 대칭이 되는 값으로 변환(0-255, 1-254)
- 감마 보정: 입력값을 조정하여 출력을 제대로 만드는 과정(감마값이 1보다 크면 영상이 어두워지고, 1보다 작으면 영상이 밝아짐)

## 경계값을 이용한 처리
디지털 영상의 화소 값을 주어진 경계 값으로 그룹화하여 결국 화소 값의 수를 감소시키는 처리 방법   
### 1. 포스터라이징
- 영상에서 화소에 있는 명암 값의 범위를 경계 값으로 축소
- 경계 값 8개로 8비트 그레이 레벨 영상을 포스터라이징 처리하면, 명암 값 256개가 명암 값 8개로 변경됨
### 2. 이진화(binarization)
- 경계 값을 이용해 값이 두 개만 있는 영상으로 변환해 주는 것
- 보통 그레이 레벨 영상을 이진 영상으로 변환할 때 사용

# 2022.11.14(월)

## 프로그래밍 언어의 전체 실행 과정

1. 사용자는 프로그래밍 언어로 소스코드를 작성해 소스파일을 만듦
2. 이 소스파일은 번역(컴파일 또는 인터프리터)을 거쳐 개체 파일(Object File)이 됨
    1. 개체 파일은 기계어로 되어 있지만 바로 실행할 수는 없다(프로그램을 실행하는 운영체제가 인식할 수 있는 형태로 다시 바꿔야 하기 때문에)
3. 링커 프로그램을 사용해 개체 파일을 실행 파일로 바꾸는 링킹 과정을 거침
4. 이렇게 작성된 프로그램은 컴퓨터 메인 메모리에 로드된다.(로더 과정)
5. 프로그램 실행

## 절차 지향 언어와 객체 지향 언어

- 절차 지향 언어(Procedure-oriented Language)
    - 프로그램을 작성할 때 실행 순서를 중심으로 설계하는 프로그램 작성 언어
    - 절차 지향 언어를 이용한 프로그램은 문제를 풀기 위한 명령어를 순차(절차)적으로 표현
    - 예) C, C++, 포트란, 베이직, 코볼 등/이외에도 초창기에 등장한 고급 언어
    - 데이터와 기능을 별도로 관리해, 기능을 호출한 뒤 데이터에 접근해 일을 처리
- 객체 지향 언어(Object-oriented Language)
    - 프로그램을 명령어의 목록으로만 보는 시각에서 벗어나, 독립된 단위의 객체(object)들의 집합으로 파악하는 언어
    - 데이터와 기능을 하나로 묶어 사용한다
    - 예) 자바, 파이썬, C++, C#(C++는 절차지향적인 특성도 있으면서 객체지향적인 특성도 있음)
    - 객체지향언어는 절차지향언어가 현실세계와 사용자의 요구에 유연하게 대처하지 못해 이를 보완하고자 개발됨
    - 기능과 데이터를 하나로 묶어 캡슐화한 후, 메시지를 전달해 일을 처리하므로 훨씬 효율적

# 2022.11.15(화)
## 임베디드 소프트웨어 정의
- 임베디드 시스템에 내장된 소프트웨어
- 시스템 소프트웨어: 운영체제(작은 메모리에서도 원활하게 동작해야 함), 미들웨어, 디바이스 드라이버, 개발도구, 컴파일러, 디버거
- 응용 소프트웨어: 데이터를 보존해야하는 경우에 플래시 메모리 사용할 수 있음

## 임베디드 소프트웨어 특성
하드웨어는 비용이 반복됨(비용은 생산량에 비례)   
소프트웨어는 1회용 설계 비용   
많은 기능이 소프트웨어로 구현되므로 소프트웨어 설계 비용이 증가될 것으로 예측됨   
### 1. 반응성
- 외부 사건에 반응하여 작업이 이루어짐
- 사건의 종류: 주기적 사건, 비주기적 사건   

### 2. 실시간
- 반응동작에 시간 제약이 있음
- 정해진 시간 범위 내에 처리해야하고 그렇지 못한 경우에 문제가 발생
- 경성(hard) 실시간 시스템: 처리작업이 데드라인을 넘기는 경우에 시스템에 심각한 영향을 주는 타임 크리티컬 속성을 갖는 시스템
- 연성(soft) 실시간 시스템: 데드라인을 넘겨도 시스템에 덜 문제가 되는 시스템/품질저하가 발생

## 사이버물리시스템(CPS) 
지능형 네트워크 도로 교차로   
예) 물류관리   

## 임베디드 시스템 유형 
- 스마트폰: 데스크탑 컴퓨팅과 유사 기능/소형, 경량, 저전력/ATM/비디오게임기
- 공장제어기기: 공기 속의 유해물질 측정기(특정목적을 수행하기 위해 사물의 상태 확인하고 측정)

## 임베디드 시스템 응용 제품
- 정보화기기: 휴대폰, 스마트폰
- 산업용장비: 로봇, 공장자동화
- 정보가전기기: 에어컨, 냉장고
- 제어장치: 가정자동화, 로봇제어, 공정제어

# 2022.11.16(수)
## 임베디드 정보 가전
- 가정 내 네트워크 구성에 따른 원격 제어, 정보 수집이 가능해짐
- 인터넷 냉장고, 인터넷 전자레인지, 세탁기 등
- Digital TV(부가적인 디지털 데이터): 양방향 티비, VOD 등

## 임베디드 정보화 기기
- PDA, 스마트폰 등: 무선랜 기능 내장으로 무선 네트워킹을 이용한 응용분야에 사용 가능/GPS 내장으로 위치기반 서비스 가능
- 임베디드 게임기기: xbox, 플스2
- 임베디드 사무용기기: 프린터, 스캐너, 복합기 등
- ATM/라우터, 게이트웨어/초음파진단기 등

## 임베디드 제어장치
#### 공장기계, 선박/항공기 
- 기계에 명령을 통해 실시간으로 상태를 조절하는 시스템 
- 예) 실시간 폐쇄 루프 피드팩 제어 기법 이용
#### 자동차의 엔진 및 각종 제어 기능: ECU(electric control unit)
#### 생산 로봇(conveyor belt)
#### 지능형 장난감 및 청소로봇(움직임 제어)
#### 신호처리기
- 대용량 데이터 처리
- 예) 비디오수신기, 레이다 신호 처리기

# 2022.11.17(목)

## 임베디드 시스템 하드웨어
- 응용 목적에 필요한 제한된 주변장치와 최소한 성능의 프로세서, 최소한의 메모리를 가진 하드웨어
- 마이크로프로세서, 기억장치, 센서, 구동기, 시스템에 필요한 특정한 장치

##  임베디드 시스템의 하드웨어 개발 과정
#### 1. 요구 기능과 성능 분석
#### 2. 하드웨어와 소프트웨어 규격 결정(사양)
#### 3. 하드웨어 모듈 결정
#### 4. 회로도 설계
- 예) PXA255 FPGA 보드 회로도   
#### 5. PCB(printed circuit board) 설계
- 부품을 구리배선으로 연결시켜 전자회로를 구성한 판
- 저항기, 콘덴서, 집적 회로 등의 전자부품을 인쇄 배선판의 표면에 고정
#### 6. 하드웨어 조립 및 시험

## 임베디드 하드웨어 구성 요소
- 임베디드 시스템 프로세서: 마이크로 프로세서, 마이크로 컨트롤러
- 메모리: 플래시 메모리, 램, 롬
- 입출력장치: RS-232C(직렬통신), USB
- 네트워크 장치: 이더넷, 와이파이

# 2022.12.05(월)

### 고정 분할
- 가장 간단한 메모리 할당 방법
- 메인메모리를 고정된 크기로 나눴다가 실행 중인 프로세스에 할당
- 분할된 메모리 구조를 유지하다 적당한 위치를 할당
- 나눠진 구역은 다른 프로세스가 침범하지 않도록 보호(상한 주소와 하한 주소값 저장)
- 작업량과 분할 공간의 크기가 일치하지 않아 빈 공간 발생 가능 = 단편화
- 내부 단편화: 작업물이 분할 공간에 있지만 공간의 크기가 커서 빈 공간 발생
- 외부 단편화: 분할 공간의 크기가 작업량보다 작아서 빈 공간 됨

### 메모리 할당 기법
- 최초 적합(First Fit): 프로그램 크기보다 큰 분할 공간 중 처음 만나는 공간을 할당한다
- 최적 적합(Best Fit): 프로그램 크기보다 큰 분할 공간 중 가장 작은 공간을 할당한다
- 최악 적합(Worst Fit): 프로그램 크기보다 큰 분할 공간 중 가장 큰 공간을 할당한다

# 2022.12.06(화)
### 가변 분할
- 고정 분할의 단점 보완 위해 등장
- 고정 분할 공간의 경계를 없애고 작업량이 맞는 공간 할당
- 작업이 완료되면 빈 공간은 다시 모아 관리(= 압축)
- 그때그때 알맞은 크기로 공간을 분할해 할당

### 문맥 전환
- 여러 개의 프로세스가 시간별로 CPU를 나눠 사용하고, CPU 내부 메모리인 레지스터에 각자의 값을 저장해 사용함
- 프로세스가 실행 상태를 벗어나면 실행 상태인 프로세스가 사용하는 레지스터 값 등은 해당 프로세스의 PCB에 저장되고, 새롭게 실행 상태로 넘어온 프로세스의 값 등은 CPU에 적재됨

# 2022.12.07(수)

## 프레임 처리(Frame Processing)
- 두 개 이상의 서로 다른 영상을 포함한 영상 간의 연산을 바탕으로 새로운 화소 값을 생성하는 것
- 생성된 결과 영상의 각 화소는 입력 영상과 같은 위치에 생성됨

### 덧셈 연산을 이용한 프레임 처리
```cpp
void CImageProcessingDoc::OnFrameSum()
{
	CFile File;
	CFileDialog OpenDlg(TRUE);

	int i;
	unsigned char* temp;

	AlphaDlg dlg;
	double alpha;

	if (dlg.DoModal() == IDOK) { // 다이얼로그의 확인 버튼을 눌렀을 때
		alpha = dlg.m_alpha;

		m_Re_height = m_height;
		m_Re_width = m_width;
		m_Re_size = m_Re_height * m_Re_width;

		m_OutputImage = new unsigned char[m_Re_size];

		if (OpenDlg.DoModal() == IDOK) {
			File.Open(OpenDlg.GetFileName(), CFile::modeRead);
			// 덧셈연산을 수행할 새로운 영상을 얻기 위해
			// 열기 대화상자를 이용해 영상을 입력

			if (File.GetLength() == (unsigned)m_width * m_height) {
				m_InputImage2 = new unsigned char[m_size];
				// 입력 값 저장을 위한 배열 선언
				File.Read(m_InputImage2, m_size); // 선택된 파일을 읽어 배열에 저장
				File.Close();

				// 프레임 간에 픽셀 대 픽셀로 덧셈연산 실행
				for (i = 0; i < m_size; i++) {
					if (m_InputImage2[i] * alpha + m_InputImage2[i] * (1 - alpha) > 255)
						m_OutputImage[i] = 255;
					else
						m_OutputImage[i] = m_InputImage2[i] * alpha + m_InputImage2[i] * (1 - alpha);
				}
			}

			else {
				AfxMessageBox("Image size not matched");
				//영상의 크기가 다를 때는 처리하지 않음
				return;
			}
		}
	
	}
}
```
```cpp
void CImageProcessingView::OnFrameSum()
{
    CImageProcessingDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);
    pDoc->OnFrameSum();
    Invalidate(TRUE);
}
```

# 2022.10.31(월)

## 디지털영상처리

### 다운샘플링(Down Sampling)

디지털 영상을 축소하는 가장 간단한 방법
다운 샘플링은 원 영상의 값을 일정한 좌표 단위로 버리는 것

디지털 영상은 2차원이므로 수평축 샘플링과 수직축 샘플링이 모두 되어야 함

- 필요한 처리
    1. 영상의 크기를 줄여야 함 (너비, 높이) : 크기를 입력 받는 윈도우가 필요 → 다이알로그(Dialog)
    2. 줄인 영상을 담을 수 있는 메모리 필요
    3. 기존 영상의 픽셀 중에서 줄인 영상에 넣을 픽셀을 선별함

``` C++
void CImageprocessingSKDoc::OnDownSampling()
{
	int i, j;
	CDownSampleDlg dlg;
	if(dlg.DoModal() == IDOK) // 대화상자의 활성화 여부
	{
		m_Re_height = m_height / dlg.m_DownSampleRate;
		// 축소 영상의 세로 길이를 계산
		m_Re_width = m_width / dlg.m_DownSampleRate;
		// 축소 영상의 가로 길이를 계산
		m_Re_size = m_Re_height * m_Re_width;
		// 축소 영상의 크기를 계산
		m_OutputImage = new unsigned char [m_Re_size]; 
		// 축소 영상을 위한 메모리 할당
		for(i=0 ; i<m_Re_height ; i++){
			for(j=0 ; j<m_Re_width ; j++){
				m_OutputImage[i*m_Re_width + j] = m_InputImage[(i*dlg.m_DownSampleRate*m_width)+dlg.m_DownSampleRate*j];
				// 축소 영상을 생성
			}
		}
	}
}
void CImageprocessingSKView::OnDownSampling()
{
	CImageprocessingSKDoc* pDoc = GetDocument(); // Doc 클래스 참조
	ASSERT_VALID(pDoc);
	pDoc->OnDownSampling(); // Doc 클래스에 OnDownSampling 함수 호출
	Invalidate(TRUE); // 화면 갱신 (TRUE: 화면 배경색을 포함해서 재출력)
	// 화면 갱신 (FALSE: 배경색은 그냥 두고 그 이외의 부분 재출력)
}
```
```C++
void CImageProcessingView::OnDraw(CDC* pDC)
{
	CImageProcessingDoc* pDoc = GetDocument(); // Doc 클래스 참조
	ASSERT_VALID(pDoc);
	// TODO: add draw code for native data here
	int i, j;
	unsigned char R, G, B;
	// 입력 영상 출력
	for(i = 0 ; i<pDoc->m_height ; i++){
		for(j = 0 ; j<pDoc->m_width ; j++){
			R = pDoc->m_InputImage[i*pDoc->m_width+j];
			G = B = R;
			pDC->SetPixel(j+5, i+5, RGB(R, G, B));
		}
	}
	// 축소된 영상 출력
	for(i = 0 ; i<pDoc->m_Re_height ; i++){
		for(j = 0 ; j<pDoc->m_Re_width ; j++){
			R = pDoc->m_OutputImage[i*pDoc->m_Re_width+j];
			G = B = R;
			pDC->SetPixel(j+pDoc->m_width+10, i+5, RGB(R, G, B)); //m_width+5+m_re_height+5
		}
	}
}
```
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
# 2022.11.01(화)
## 업샘플링(Up Sampling)
영상을 확대할 때는 먼저 일정한 배열 간격으로 재배열해야 하는 것
단순 업 샘플링을 사용하여 영상을 확대하면 영상의 품질이 현저히 떨어짐
영상을 확대해도 선명한 품질을 얻고 싶다면 업 샘플링으로 얻은 데이터와 원본 영상의 데이터를 이용하여 보간(Interpolation)을 해야 함

- 필요한 처리
    1. 영상의 크기를 늘려야 함 (너비, 높이)
    2. 늘린 영상을 담을 수 있는 메모리 필요
    3. 기존 영상의 픽셀을 늘린 영상의 픽셀로 대치함

```C
void CImageprocessingSKDoc::OnUpSampling()
{
	int i, j;
	CUpSampleDlg dlg;
	if(dlg.DoModal() == IDOK){ // DoModal 대화상자의 활성화 여부
		m_Re_height = m_height * dlg.m_UpSampleRate;
		// 확대 영상의 세로 길이 계산
		m_Re_width = m_width * dlg.m_UpSampleRate;
		// 확대 영상의 가로 길이 계산
		m_Re_size = m_Re_height * m_Re_width;
		// 확대 영상의 크기 계산
		m_OutputImage = new unsigned char[m_Re_size];
		// 확대 영상을 위한 메모리 할당
		for(i=0 ; i<m_Re_size ; i++)
			m_OutputImage[i] = 0; // 초기화
		for(i=0 ; i<m_height ; i++){
			for(j=0 ; j<m_width ; j++){
				m_OutputImage[i*dlg.m_UpSampleRate*m_Re_width +	dlg.m_UpSampleRate*j]= m_InputImage[i*m_width + j];
			} // 재배치하여 영상 확대
		}
	}
}
void CImageProcessingSKView::OnUpSampling()
{
	CImageProcessingSKDoc* pDoc = GetDocument(); // Doc 클래스 참조
	ASSERT_VALID(pDoc);
	pDoc->OnUpSampling(); // Doc 클래스에 OnUpSampling 함수 호출
	Invalidate(TRUE); // 화면 갱신
}
```

# 2022.11.02(수)

## 양자화

표본화된 화소의 밝기나 색상을 정해진 몇 단계의 값으로 근사화 하는 과정
화소의 밝기나 색상이 숫자로 표현되어 화소는 양자화된 표본 값을 갖게 됨
밝기나 색상이 몇 단계로 표현되느냐는 양자화 비트(Quantization Bits)로 결정됨

```cpp
void CImageProcessingDoc::OnQuantization()
{
	CQuantizationDlg dlg;
	if(dlg.DoModal() == IDOK)
	// 양자화 비트 수를 결정하는 대화상자의 활성화 여부
	{
		int i, j, value, LEVEL;
		double HIGH, *TEMP;
		m_Re_height = m_height;
		m_Re_width = m_width;
		m_Re_size = m_Re_height * m_Re_width;
		m_OutputImage = new unsigned char[m_Re_size];
		// 양자화 처리된 영상을 출력하기 위한 메모리 할당
		TEMP = new double [m_size];
		// 입력 영상 크기(m_size)와 동일한 메모리 할당
		LEVEL=256; // 입력 영상의 양자화 단계(28=256)
		HIGH=256;
		value = (int)pow(2, dlg.m_QuantBit);
		// 양자화 단계 결정(예 : 24=16)
		for(i=0 ; i<m_size ; i++){
			for(j=0 ; j<value ; j++){
				if(m_InputImage[i] >=(LEVEL/value)*j &&	m_InputImage[i]<(LEVEL/value)*(j+1)){
					TEMP[i]=(double)(HIGH/value)*j; // 양자화 수행
				}
			}
		}
		for(i=0 ; i<m_size ; i++){
			m_OutputImage[i] = (unsigned char)TEMP[i];
			// 결과 영상 생성
		}
	}
}
```
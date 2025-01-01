# Chap4. 초기 데이터셋 준비하기

> 데이터 품질을 효과적으로 판단하고, 이 데이터를 벡터로 변환하고, 이 벡터 표현으로 데이터셋을 효율적으로 조사하고, 레이블을 부여하고, 이 분석을 통해 특성 생성 전략을 짜고...
>
> ⛰️**산 넘어 산**⛰️



<br/>

## 4.1 반복적인 데이터셋

- 머신러닝 제품을 가장 빠르게 만드는 방법 = **모델 구축과 평가를 빠르게 반복**
  - 데이터셋 자체가 모델 성공의 핵심 요소! → 데이터 수집, 준비, 레이블링 역시 *반복적* 과정

  - 작업의 대부분이 초기 데이터셋 선택 후 규칙적으로 업데이트하는 것
  
    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fwep5l%2FbtrmnmugBIE%2FVehYqTHxVMYi5wvCZktIFK%2Fimg.jpg" alt="img" style="zoom:30%;" />
  
    
  
- **데이터 과학 수행하기** ⭐
  - 사용할 데이터 가 모델이 예측하기 충분한 패턴을 담고 있는지 확인하기✅
  - 두드러진 편향이 내재되어 있는지 체크 ✅




<br/>

## 4.2 첫 번째 데이터셋 탐색하기

> 첫 번째 단계 = 데이터셋을 ***모으자***
>
> ❌완벽한 데이터셋을 찾으려 하지 말자❌
> ⭕예비 결과를 만들 수 있는 간단한 데이터셋을 찾자!⭕

#### 4.2.1 효율적으로 적게 시작하기

- 프로젝트를 시작할 때 데이터셋이 작으면 분석하고 이해하기 쉽다!
   → 더 나은 모델을 만드는 방법을 이해할 수 있다
- 캐글, 레딧, 크롤링, 스크래핑 등을 통해 대규모 공개 데이터셋 찾아 활용하기
- 데이터 조사할 때에는 *트렌드 식별* + 트렌드를 *자동으로 활용*할 수 있는 방법

<br/>

#### 4.2.2 통찰 vs 제품

- 데이터셋이 준비된 후에는 내용 탐색! 
   → 이 과정에서는 **분석 목적**과 **제품 개발 목적**의 차이를 유념할 것
  - 전자는 트렌드에서 *통찰을 얻는 것*, 후자는 트렌드를 사용해 *특성을 만드는 것*
  - EX. 부정한 웹사이트 로그인은 언제 어디서 발생할 확률이 높은가 ❓
  - EX. 로그인 시간과 IP 주소를 이용해 부정 로그인 계정을 막는 서비스를 만들자 ❗
- 제품 개발의 경우는 복잡도가 더 높음
  - 패턴을 미래에 얻을 데이터에 적용할 수 있는가? 
  - 훈련 데이터와 제품 시스템에서 얻을 데이터 사이의 차이는 어떻게 정량화할 것인가?

<br/>

#### 4.2.3 데이터 품질 기준

- 트렌드 감지 위해서는 품질 조사 필수!
- 고유한 편향과 이상치를 가짐  → 이해하는 데 필요한 도구가 다를 수 있다
  - 보편적인 기준은 없음
  - 처음 데이터셋을 다룰 때 주의할 공통적인 카테고리를 알아두자!

1. **데이터 포맷**
   - 깨끗한 입력과 출력으로 구성되어 있나❓
   - 추가적인 전처리/레이블링이 필요한가 ❓
   - EX. 광고 클릭율 예측 모델 → 데이터셋: 과저 일정 기간 동안의 모든 클릭 로그
     - 이 데이터셋을 한 사용자에게 보여진 광고/클릭 여부로 변환..
     - 평균 전환율을 나타내는 Column 의 경우 직접 계산하여 맞는지 확인 할 수 있을까? 
       (이미 전처리된 데이터셋)
     - 전처리 단계를 재현하고 검증하기 위한 필수 정보를 얻지 못할 수도 있다!

<br/>

2. **데이터 품질**
   - 데이터 품질을 이해하면 모델의 성능을 이해할 수 있다!
   - 데이터 품질이 나쁜 이유 → 값이 누락 / 부정확 / 오염 등등...
     - EX. 광고 클릭율 예측 모델 → 누락된 로그는 얼마나❓
     - EX. 자연어 텍스트 품질 평가 모델 →  이해할 수 없는 문자❓맞춤법 오류❓
     - 데이터의 잡음은❓ 기준에 레이블이 적합한가 ❓...
   - 누락된 레이블을 위해 초기 데이터셋을 직접 레이블링하거나 대체할만한 유사 레이블을 찾을 수 있지만 **사전에 품질을 알고 있는 경우**에만 사용할 수 있음

<br/>

3. **데이터 양과 분포**

   - 데이터가 충분하고, 특성값이 적절한 범위 안에 있는지 확인!

     - 대규모라면 *일부를 선택*해 분석 시작
     - 소규모라면 *편향*의 위험성 존재 →  수집/증식 통해 데이터 *다양성*을 높이자

     | 품질                       | 포맷                                                 | 양과 분포                                                 |
     | -------------------------- | ---------------------------------------------------- | --------------------------------------------------------- |
     | 관련된 특성이 비어 있나요? | 데이터에 얼마나 많은 전처리 단계가 필요한가요?       | 얼마나 많은 샘플을 갖고 있나요?                           |
     | 잘못 측정된 값이 있나요?   | 제품 시스템에서 동일한 방식으로 전처리가 가능한가요? | 클래스마다 몇 개의 품플이 있나요? 누락된 클래스가 있나요? |

     <br/>

   - EX. 이메일 전문 분야 자동 분류 모델

     - 소규모 데이터셋 → *데이터 생성전략*에 집중!

     - 9개 분야에 대한 공통 구성 요소를 템플릿화 →  수천 개의 샘플 생성

     - 단순 사무적 분류의 경우 7개 하위 클래스당 단 하나의 예시만 보유

       <img src="https://miro.medium.com/v2/resize:fit:786/format:webp/0*FxKeRFqR0p296PEn." alt="ㅇ" style="zoom:50%;" />

     - 유한 상태 문법(FSG)을 사용하여 인공 데이터 생성, 각 질문당 13,000에서 150만 개 이상의 *변형 생성* 가능

       <img src="https://miro.medium.com/v2/resize:fit:786/format:webp/0*mRNwqcJGAXz8C2K6." alt="ㅇㅇ" style="zoom:50%;" />

     - 더 높은 정확도를 달성하는 파이프라인 구현 가능!

   <br/>

   4. **머신러닝 에디터 데이터 조사해보기**
      - 데이터셋: Stack Exchange Dump (https://archive.org/details/stackexchange)











s



참고

https://deep-diver-csp.tistory.com/7

https://blog.insightdatascience.com/automating-customer-support-when-you-lack-data-e9975fd8a053
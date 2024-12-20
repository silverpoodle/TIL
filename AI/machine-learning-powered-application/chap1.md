# Chap1. 제품의 목표를 머신러닝 문제로 표현하기

## WHAT is Machine Learning?

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20230413160822/Maachine-Learning.webp" alt="image1" style="zoom:50%;" />



| 용어              | 설명                                                         | 주요 특징                                                    | 응용 사례                                                    |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **인공지능 (AI)** | 가장 광범위한 개념 <br />- 일반적으로 인간 지능이 필요한 작업을 수행하도록 설계된 시스템 | • 규칙 기반 시스템과 논리적 추론 포함<br>• ML과 딥러닝을 포괄하는 개념<br>• 기계에서 지능적 행동 구현에 중점 | • 자연어 처리<br>• 전문가 시스템<br>• 로봇공학<br>• 컴퓨터 비전<br>• 게임 (체스 AI 등) |
| **기계학습 (ML)** | AI의 하위 분야로,경험을 통해 학습하고 개선되는 시스템<br />- 명시적 프로그램 (explicit program)의 반대되는 개념 | • 통계적 기법을 사용하여 패턴 학습<br>• 훈련 데이터 필요<br>• 새로운 데이터로 예측 가능<br>• 의사결정트리, 랜덤 포레스트, SVM 등 다양한 알고리즘 포함 | • 스팸 탐지<br>• 제품 추천<br>• 신용카드 사기 감지<br>• 날씨 예측 |
| **딥러닝**        | 여러 층의 신경망을 사용하는 ML의 특수한 하위 분야            | • 다층 구조의 인공신경망 사용<br>• 대량의 데이터 필요<br>• 특징을 자동으로 학습 가능<br>• 비정형 데이터 처리에 탁월 | • 이미지 인식<br>• 음성 인식<br>• 언어 번역<br>• 자율주행 자동차<br>• 의료 진단 |

<br/>

## WHEN?

> 💡***경험적*으로 해결책을 정의할 수 *없는* 문제**
>
> 1. 제품의 목표 정의
> 2. 머신러닝 타당성 평가: 가능성이쓴 모델 고려, 간단한 것부터 시도!

- 강아지 / 고양이 감지 시스템
  → Explicit Programming(IF 문) ❌
  → 합성곱 신경망 (CNN) ⭕
- 세금 계산 시스템
  → 머신러닝 ❌ (정확한 정부 가이드라인에 따라야함!)
  → Explicit Programming ⭕ (단계별 명령을 통한)

<br/>

### MODEL

1. **지도 학습 (Supervised Algorithm)**

   - **레이블**: 데이터의 *일부분*, *이상적인* 출력
   - 레이블을 포함한 데이터셋 입력 → 레이블 매핑하는 방법 학습
   - 분류 (Classification), 회귀 (Regression)

   <img src="https://media.geeksforgeeks.org/wp-content/uploads/20231121154747/Supervised-learning.png" alt="image" style="zoom:50%;" />
   <br/> 

2. **비지도 학습 (Unsupervised Algorithm)**

   - 레이블 필요 X
   - 군집화 (Clustering), 연관규칙 (Association)

   <img src="https://media.geeksforgeeks.org/wp-content/uploads/20231121154719/Unsupervised-learning.png" alt="im2" style="zoom:50%;" />
   <br/>

   

3. **약지도 학습 (Weakly Supervised Algorithm)**

   - 정확히 원하는 출력은 아니지만 비슷하거나 일부 정보만 가진 레이블 사용

   <img src="https://velog.velcdn.com/images/kyyle/post/45f74c0e-3d92-4cf2-911c-ea230fe1ef49/image.png" alt="hi" style="zoom:50%;" />
   <br/>

4. **강화 학습 (Reinforcement)**

   - *상벌 패러다임*을 통해 각 작업의 피드백을 배우며 결과 도출
   - 정책 학습 (Policy Learning)

   <img src="https://www.ibm.com/content/dam/connectedassets-adobe-cms/worldwide-content/creative-assets/s-migr/ul/g/8f/5e/reinforcement-learning-figure-1.png" alt="te" style="zoom:15%;" />



<br/>

### CATEGORIZE

1. **분류 (Classification)**

   - 2개 이상의 카테고리로 데이터 포인트를 *분류*

     > 1. 이메일이 스팸인가? (YES / NO) → 스팸 필터
     > 2. 부정한 거래인가? (YES / NO) → 부정 거래 탐지 시스템
     > 3. 뼈가 골절 되었는가?  (YES / NO) → 컴퓨터 비전 모델

   - 하나의 범주에 속할 *확률 점수*를 출력하기 때문에 회귀와 비슷

     

2. **회귀 (Regression)**

   - 2개 이상의 카테고리로 데이터 포인트들의 연속적인 값을 *예측*

     > 1. 지역/방 개수 기반 주택 가격 예측
     > 2. 모델/주행 거리 등 데이터 기반 중고차 가격 모델 예측
     > 3. 주식 가치 예측 시스템

   <img src="https://miro.medium.com/v2/resize:fit:786/format:webp/1*W0YUVkHgI8KTKW1I8FLgEg.png" alt="vs" style="zoom:50%;" />

   - 시계열 데이터 (Time Series): 여러 개의 과거의 데이터 포인트들
   - 포캐스팅 (Forecasting): 일련의 연속된 데이터 포인트들
   - 이상치 탐지 (Anomaly Detection): 일반적이지 않은 데이터 감지
   - 특성 선택(Feature Selection) 과 특성 공학 (Feature Engineering) 을 통한 예측 성능 향상

   <br/>

3. **지식 추출 (Knowledge Extraction)**

   - 구조적 데이터 (Structured Data): *테이블* 형태로 저장
   - 비구조적 데이터 (Unstructured Data): 기타 데이터셋 (텍스트, 음악, 비디오 ..)
     - 비구조적 데이터 → 구조를 추출

   <img src="https://lawtomated.com/wp-content/uploads/2019/04/structuredVsUnstructuredIgneos.png" alt="db" style="zoom:25%;" />

   <br/>

   - 이미지 지식 추출

     - 객체 탐지 (Object Detection): Bounding Box 를 그리는 접근

     - 이미지 분할 (Image Segmentation): 이미지의 각 픽셀을 하나의 범주에 할당

       <img src="https://miro.medium.com/v2/resize:fit:640/1*pWoHu_uUDebBSSNmyMydLQ.png" alt="img" style="zoom:67%;" />

       <br/>

4. **카탈로그 구성 (Catalog Organization)**

   - 사용자에게 보여줄 *출력의 집합* 생성

     - 쇼핑몰에서 사용자가 관심을 보인 아이템과 관련된 제품 추천
     - 텍스트 입력/사진 입력을 통한 검색

   - 협업 추천 시스템 (Collaborative Recommendation System)

     <img src="https://miro.medium.com/v2/resize:fit:649/1*Z8p9PAqx2dFfEn76B6juAw.png" alt="t" style="zoom:50%;" />

   - 콘텐츠 기반 추천 시스템 (Content-Based Recommendation System)

     <img src="https://miro.medium.com/v2/resize:fit:792/1*P63ZaFHlssabl34XbJgong.jpeg" alt="d" style="zoom:35%;" />

     <br/>

5. **생성 모델 (Generative Model)**

   - 사용자 입력에 따라 새로운 데이터 생성
   - 다양한 형태의 출력 생성
   - 출력에 대한 제한이 적기 때문에 제품 시스템에 적합하지 않음
     - 번역, 요약, 자막 생성, 이미지 생성 등



<br/>

### DATA

1. **데이터 타입**
   - *입력을 출력에 매핑*하는 것 = `욕구의 단계 (Hierarchy of Needs)`
     - 정확히 찾으려는 매핑 데이터를 구하는 것
2. **데이터 가용성 (Data Availability)**
   - 레이블된 데이터셋: 예측하려는 타깃 값이 포함
   - 유사 레이블 데이터셋: 예측하려는 타깃과 연관된 레이블이 포함
   - 레이블 없는 데이터셋: 입력과 출력을 매핑할 레이블된 데이터셋 없음.
     - `직접 레이블` or `레이블 필요 없는 모델 사용`
   - 데이터가 아예 없음ㅋ (수집해야함): 힝.

<br/>

### PRACTICE

> 💡**더 나은 질문을 하도록 돕는 에디터를 만들어보자!**

1. **WHAT?**

   - 나쁜 질문💩 → 모델 → 좋은 질문🩵

     - 하나의 모델로 입력 → 출력 (END-TO-END Framework)

   - 데이터셋 구하기

     - 나쁜질문 + 좋은질문 데이터셋 존재 ❌
     - 직접 만들 돈 없다~ 💸

   - 모델 정하기

     - 문장 매핑 → *생성형 모델* (Sequence - to - Sequence = AutoRegressive Model)
       - 앞서 출력한 단어를 다음 출력을 만드는데 사용, 단순한 모델보다 훈련/추론 느림
       - 빠르게 실행될수 있도록 추가적인 엔지니어링 작업 필요
     - 많은 모델 파라미터 사용 → 훈련 속도 느림 → 재훈련 필요할 시 issue
       - 복잡도가 커지면 파이프라인 구축 시간 오래걸림, 유지보수 작업 늘어남
       - 간단하고 잘 이해할 수 있는 모델 선택 필요

     <br/>

2. **HOW?**

   - **알고리즘을 구현하기 전에 *알고리즘이 되어보자***! ~~(뭔말이야;;;;;)~~
     - 문제에 대한 최선의 자동화 방법을 이해하기 위해 *수동으로* 작업 해결 시도
       1. `데이터 없이` 사전 지식으로 텍스트 수정 유도
          ex. 신문기사 작성 가이드 참고, 편집자 tip
       2. 데이터셋에서 `개별 샘플과 트렌드`를 확인하고 모델링 전략에 활용
       3. 기존 연구를 통해 명확하게 글을 쓰는데 도움이 되는 몇 가지 속성 확인, 솔루션 제공
          - 단순한 문장
          - 어조
          - 구조적 특징
   - ***경험*에서 배워보자!**
     - 데이터셋을 모으고, 특성을 추출하고, 분류기 훈련
       1. 데이터셋
       2. 모델: 성능이 높은가? and 샘플을 분류하는데 사용되는 속성을 확인할 수 있는가?
       3. 응답 속도
       4. 구현의 용이성
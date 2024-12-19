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

   <img src="https://ietresearch.onlinelibrary.wiley.com/cms/asset/a035d68d-8ea1-47b7-bebc-7a5d3e87f3c1/cit212216-fig-0002-m.png" alt="hi" style="zoom:70%;" />
   <br/>

4. **강화 학습 (Reinforcement)**

   - 상벌 패러다임을 통해 각 작업의 피드백을 배우며 결과 도출
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

   - 시계열 데이터 (Time Series): 
   - 포캐스팅 (Forecasting): 

   <img src="https://miro.medium.com/v2/resize:fit:786/format:webp/1*W0YUVkHgI8KTKW1I8FLgEg.png" alt="vs" style="zoom:50%;" />
   <br/>

3. **지식 추출 (Knowledge Extraction)**

4. **카탈로그 구성 (Catalog Organization)**

5. **생성 모델 (Generative Model)**
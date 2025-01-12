# Chap4. 초기 데이터셋 준비하기

> 데이터 품질을 판단하고, 이 데이터를 벡터로 변환하고, 이 벡터 표현으로 데이터셋을 조사하고, 레이블을 부여하고, 이 분석을 통해 특성 생성 전략을 짜고...
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
      
        > - 얼마나 많은 데이터가 누락되었나요?
        > - 텍스트의 품질은 무엇인가요?
        > - 대답이 질문과 일치하나요?

```python
import xml.etree.ElementTree as ELT

def parse_xml_to_csv(path, save_path=None):
  """
  xml 덤프 파일을 열고 텍스트를 토큰화하여 CSV로 변환합니다.
  :param path: 포스트가 담긴 xml 문서 경로
  :return: 전처리된 텍스트의 데이터프레임
  """

  #파이썬 표준 라이브러리를 사용해 XML 파일 파싱
  doc = ELT.parse(path)
  root = doc.getroot()

  #각 행은 하나의 포스트입니다.
  all_rows=[row.attrib for row in root.findall("row")]

  #tdqm을 사용해 전처리 진행 과정을 출력합니다.
  for item in tqdm(all_rows):
    # HTML에서 텍스트를 디코딩합니다.
    soup =BeautifulSoup(item["Body"], features="html.parser")
    item["body_text"] = soup.get_text()

  #딕셔너리의 리스트에서 데이터프레임을 생성합니다.
  df = pd.DataFrame.from_dict(all_rows)
  if save_path:
    df.to_csv(save_path)
  return df

path = '/content/drive/MyDrive/machinelearning-powered-application/Posts.xml'
save_path = '/content/drive/MyDrive/machinelearning-powered-application/Posts.csv'
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250110153309166.png?raw=true" alt="image-20250110153309166" style="zoom:80%;" />

<br/>

```python
# 손쉬운 처리를 위해 타입을 바꿉니다
df["AnswerCount"] = df["AnswerCount"].fillna(-1)
df["AnswerCount"] = df["AnswerCount"].astype(int)
df["PostTypeId"] = df["PostTypeId"].astype(int)
df["Id"] = df["Id"].astype(int)
df.set_index("Id", inplace=True, drop=False)

# 포스트의 길이를 추가합니다.
df["full_text"] = df["Title"].str.cat(df["body_text"], sep=" ", na_rep="")
df["text_len"] = df["full_text"].str.len()

# 질문은 포스트 타입이 1입니다
df["is_question"] = df["PostTypeId"] == 1

# 열과 Null이 아닌 개수를 출력합니다
df.info()

# 질문과 답변만 관심 대상이므로 PostTypeId가 1 또는 2가 아닌 모든 행을 삭제
df = df[df["PostTypeId"].isin([1,2])]
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250110153803763.png?raw=true" alt="image-20250110153803763" style="zoom:67%;" />

<br/>

```python
# 몇 개의 질문과 답변을 출력하고 두 내용이 일치하는지, 읽을 수 있는지 확인
questions_with_accepted_answers = df[df["is_question"] & ~(df["AcceptedAnswerId"].isna())]
q_and_a = questions_with_accepted_answers.join(df[["body_text"]], on="AcceptedAnswerId", how="left", rsuffix="_answer")

# 모든 데이터를 출력하기 위해 이 옵션을 설정합니다
pd.options.display.max_colwidth = 500
q_and_a[["body_text", "body_text_answer"]][:3]
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250110154453454.png?raw=true" alt="image-20250110154453454" style="zoom:60%;" />

<br/>

```python
# 답변이 1개 이상 있는 질문들 필터링
received_answers = df[
    (df["is_question"]) &  # 질문인 행들만 선택
    (df["AnswerCount"] != 0)  # 답변 수가 0이 아닌 것들
]

# 채택된 답변이 있는 질문들 필터링
has_accepted_answer = df[
    (df["is_question"]) &  # 질문인 행들만 선택
    ~(df["AcceptedAnswerId"].isna())  # AcceptedAnswerId가 존재하는 것들
]

# 통계 출력
stats_message = "총 질문: {:,}개, 1개 이상의 답변을 가진 질문: {:,}개, 답변이 채택된 질문: {:,}개".format(
    len(df[df["is_question"]]),  # 전체 질문 수
    len(received_answers),       # 답변 받은 질문 수
    len(has_accepted_answer)     # 답변이 채택된 질문 수
)

print(stats_message)
```

![image-20250110154945794](https://github.com/silverpoodle/typora-images/blob/main/image-20250110154945794.png?raw=true)

<br/>

## 4.3 레이블링으로 데이터 트렌드 찾기

- **모델 입장**에서 어떤 종류의 구조를 선택할지 예상해보기
- 데이터셋에 대한 요약 통계 → **벡터화 기법**으로 빠르게 탐색 (**군집**을 활용)

### 4.3.1 요약 통계

- 클래스의 분포 차이 식별 → 성능 과대평가 방지
  - EX. 트위터 의견 긍정/부정 예측
    - 평균 단어 개수 파악 → 히스토그램 제작 → ❗부정 트윗의 단어수가 더 많다❗
      →  예측 변수 단어 개수 추가

```python
import matplotlib.pyplot as plt
from matplotlib.patches import Rectangle

# 중간 점수를 기준으로 높은 점수와 낮은 점수 구분
high_score = df["Score"] > df["Score"].median()

# 일반적인 길이의 텍스트만 선택 (2000자 미만)
normal_length = df["text_len"] < 2000

# 그래프 생성
plt.figure(figsize=(16, 10))
ax = plt.gca()

# 높은 점수 질문의 히스토그램 (주황색)
df[df["is_question"] & high_score & normal_length]["text_len"].hist(
    bins=60,
    density=True,
    histtype="step",
    color="orange",
    linewidth=3,
    grid=False,
    ax=ax
)

# 낮은 점수 질문의 히스토그램 (보라색)
df[df["is_question"] & ~high_score & normal_length]["text_len"].hist(
    bins=60,
    density=True,
    histtype="step",
    color="purple",
    linewidth=3,
    grid=False,
    ax=ax
)

# 범례 생성
handles = [Rectangle((0, 0), 1, 1, color=c, ec="k") for c in ["orange", "purple"]]
labels = ["High score", "Low score"]
plt.legend(handles, labels)

# 축 레이블 설정
ax.set_xlabel("Sentence length (characters)")
ax.set_ylabel("Percentage of sentences")

plt.show()
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250110155733270.png?raw=true" alt="image-20250110155733270" style="zoom:67%;" />

- 분포가 비슷하나, 긴 질문의 점수가 더 높은 경향이 있다 → *질문 길이가 점수 예측하는 것에 유효한 특성*

<br/>

### 4.3.2 효율적인 탐색과 레이블링

- 효율적으로 개별 데이터 포인트 확인하기: 벡터화 → 군집(Cluster) 알고리즘

  <img src="https://www.qualtrics.com/m/assets/wp-content/uploads/2023/09/cluster-graph-en-768x512.webp" alt="군집" style="zoom:50%;" />

  - 데이터셋을 개별 데이터 포인트를 *시각화할 수 있는 비지도 학습 방법*
    - 한 그룹 내 객체가 다른 그룹에 있는 객체보다 더 비슷하도록 모으는 작업
    -  각 클러 스터를 조사하고 클러스터 간의 유사도와 차이를 살펴보면 데이터셋에 내재된 구조를 식별
      -  데이터셋에 얼마나 많은 클러스터가 있나요? 
      - 클러스터마다 다르게 보이나요? 
      - 어떤 기준을 사용하나요? 
      - 다른 클러스터보다 더 조밀한 클러스터가 있나요? 
        그렇다면 모델이 조밀하지 않은 지역에서 잘 동작하지 않을 수 있습니다. 특성이나 데이터를 추가하면 이 문제를 해결하는 데 도움이 됩니다. 
      - 모든 클러스터가 모델링하기 어려운 데이터를 나타내나요? 
        일부 클러스터가 복잡한 데이터를 표현하는 것처럼 보인다면 기록해두었다가 모델의 성능을 평가할 때 다시 이 문제를 살펴보겠습니다.

<br/>

#### 벡터화(Vectorize)

- 원본 데이터를 벡터 표현으로 변환하는 과정

  - 정형 데이터를 해당 데이터의 원래 의미를 표현하는 **숫자 배열**로 변환
  
  ![ㅇ](https://noduslabs.com/wp-content/uploads/2018/07/lda-blei-topic-modeling-latent-dirichlet-allocation-510x280.jpg)

> **범주형 자료**: 범주를 서로 구분하는 이름에 해당하는 자료
> EX. 성별(남/여), 직종(서비스/전문/기술..), ....
>
> **연속형 자료**: 연속적인 수로 수량화가 가능한 자료
> EX. 온도, 키, 체중, 나이, ....

<br/>

#### 표 형식 데이터

- 범주형/연속형 모두 포함
  - 연속화: 스케일이 큼 → 작은 특성들을 무지하지 않도록 **정규화(normalization)** → **표준 점수(standard score)** , 평균이 0이고 단위 분산을 가지도록 특성 변환
  - EX. 색과 같은 범주형 특성 → **원-핫 인코딩 (one-hot encoding)** = 특성에 있는 고유한 값의 개수만큼 원소를 가진 리스트
    - 두 특성값 사이의 거리가 *항상 1*

<img src="https://blog.kakaocdn.net/dn/bUTJF4/btsqCbHRjw6/GKpv5KB62nC1csrDZqM4Rk/img.png" alt="ㅇㅇ" style="zoom:60%;" />

- **데이터 누수**: 모델의 성능이 갑자기 너무 좋아졌다..!? → 데이터 누수를 의심해보자..
  - *training data 이외의 유입된 정보*가 모델을 만들때 사용되었을 때!

<br/>

#### 텍스트 데이터

- 텍스트 벡터화의 가장 쉬운 방법 = 원-핫 인코딩 **카운트 벡터(count vector)** 사용!
  - 데이터셋 단어로 어휘 사전 제작 → 각 단어는 하나의 인덱스에 연결(0~N) → 문장/문단을 어휘 사전 크기의 리스트로 표현 (각 인덱스에 있는 숫자 = 문장에서 단어가 등장한 횟수) = **BoW (Bag of Words) 방식**

![ㅇ](https://miro.medium.com/v2/resize:fit:500/1*hLvya7MXjsSc3NS2SoLMEg.png)

- BoW 를 정규화한 버전인 TF-IDF (Term Frequency-Inverse Document Frequency) 사용!

  ```python
  #TfidfVectorizer 클래스 객체 생성
  #정규화되지 않은 CountVectorizer를 사용
  vectorizer TfidfVectorizer()
  
  #vectorizer를 데이터셋에 있는 질문에 훈련하면 벡터화된 텍스트의 배열이 반환
  bag_of_words = vectorizer.fit_transform(df[df["is_question"]]["Text"])
  ```

- Word2Vec, fastText 등 여러 텍스트 벡터화 방식 개발

- 각 단어 벡터를 학습하고, 주변 단어의 단어 벡터를 사용해 **빠진 단어를 예측**하는 모델을 훈련

  - 고려할 주변 단어의 개수 = **윈도 크기(window size)** 

  <img src="https://lovit.github.io/assets/figures/word2vec_logistic_structure.png" alt="ㅇㅇ" style="zoom:50%;" />



<br/>

#### 이미지 데이터

- 이미지 데이터는 **이미 벡터화**되어 있다! = 다차원 수치 배열이기 때문
  - EX.  3채널 RGB 이미지는 이미지 픽셀 높이에 너비와 3 (빨강, 초록, 파랑 채널)을 곱한 것과 길이가 같은 리스트로 저장
- **사전 훈련된 CNN 모델**을 활용하면 효과적인 이미지 표현 추출 가능
  - ImageNet, VGG 등 대규모 데이터셋으로 학습된 모델의 중간층 활용
  - 특히 분류층 직전의 층이 이미지의 의미적 특징을 잘 포착하는 벡터 생성
- 추출된 표현은 다양한 downstream 작업에 활용 가능
  - 원본 분류 작업 외의 다른 이미지 관련 태스크에도 적용 가능
  - 별도의 추가 학습 없이 바로 사용 가능한 장점

<img src="https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/2BTY0/btrxiFEcDxs/9wpPQFojK3KVTh4xIso5z1/img.png" alt="ㅋ" style="zoom:60%;" />

- **전이학습 (Transfer Learning)**: 하나의 데이터셋/작업에서 훈련한 모델을 다른 작업에 사용
  - 동일한 구조, 파이프라인, 훈련된 모델의 가중치 사용
  - 성능을 향상시키지만, 편향을 주의할 것!

<br/>

#### 차원 축소

<img src="https://blog.kakaocdn.net/dn/bI14Ul/btrrqcHxxBb/dZ7Omj6WHCEYjKs0ktHt21/img.png" alt="ㅊ" style="zoom:50%;" />

* **고차원 벡터의 시각화**를 위한 필수적인 기법
   * 데이터의 *주요 구조는 유지*하면서 *더 낮은 차원*으로 표현
* 주요 차원 축소 기법: t-SNE, UMAP
   * 고차원 데이터(문장, 이미지, 특성 벡터 등)를 2D로 시각화 가능
* 데이터에서 조사할 패턴을 찾는 데 유용
   * 데이터 포인트를 의미 있는 속성으로 색상 구분
     * 분류 문제: 레이블 기반 색상화
     * 비지도 학습: 특성값 기반 색상화
* **주의사항**
   * 차원 축소된 시각화는 근사 표현임
   * 발견된 패턴은 다른 방법으로 검증 필요
   * 군집 분석과 함께 활용하면 더 효과적

<br/>

#### 군집

<img src="https://i.sstatic.net/yzjvp.png" alt="ㄹ" style="zoom:80%;" />

* *데이터셋 조사와 모델 성능* 분석 & *문제점 발견과 흥미로운 데이터 포인트 식별*에 활용
   * 각 클러스터의 샘플 포인트 조사
   * 데이터의 트렌드 파악
   * 수동 레이블링 작업에 활용
* **군집 분석 방법**
   * k-means 같은 간단한 알고리즘 활용 → 클러스터 개수 등 하이퍼파라미터 조정
   * Elbow Method, Silhouette Graph 같은 도구 활용 → 데이터를 완벽하게 분리하는 것이 아니라, **모델이 어려움을 겪을 만한 영역을 식별**하는 것이 목적입
* **시각화와 분석**
   * 차원축소(UMAP 등)와 함께 활용하여 클러스터 시각화
   * 2D 시각화와 실제 군집이 항상 일치하지는 않음
   * 클러스터 정보를 특성으로 추가하여 모델 성능 향상 가능



<br/>

### 4.3.3 알고리즘이 되어보기..2(또..?;)

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250111194809527.png?raw=true" alt="image-20250111194809527" style="zoom:80%;" />

- 몇 개의 샘플에 모델이 만들어야 할 결과 레이블  → 정확도 검증  → 특성 발견! or 벡터화 전략 업데이트  →  레이블링 반복

  - 속도를 높이려면 클러스터마다 샘플 몇 개를 레이블링하며 얻은 분석 정보 활용
  - Bokeh 등 시각화 라이브러리를 사용해 그래프 확인하며 빠르게 레이블링 처리

  <img src="https://pbs.twimg.com/media/FgaKdpaaAAAGE9j.jpg:large" alt="b" style="zoom:30%;" />

<br/>

### 4.3.4  데이터 트렌드

* **트렌드의 유형**
   * 유용한 정보 (예: 짧은 트윗의 감성 분류 경향)
   * 데이터 수집 방식으로 인한 상관관계 없음
   * 편향된 샘플링으로 인한 왜곡된 패턴

* **트렌드 발견의 중요성**
   * 초기 프로토타입 단계에서 파악 필요
   * 인공적인 성능 향상 방지
   * 실제 환경에서의 성능 저하 예방

* **편향된 트렌드 해결 방법**
   * 추가 데이터 수집으로 대표성 향상
   * 편향된 특성 제거 (단, 상관관계로 인해 한계 존재)

* **트렌드 활용 방법**
   * 관련 특성 생성에 활용
   * 트렌드를 잘 포착하는 모델 선택

<br/>

## 4.4 데이터를 활용한 특성 생성과 모델링

### 4.4.1 패턴에서 특성 만들기

- 머신러닝은 패턴을 활용하기 위해 통계적 학습 알고리즘 사용

  - 단순한 패턴은 모델이 쉽게 감지할 수 있지만, 복잡한 문제일수록 더 정교한 패턴 분석이 필요
  - **특성 추가 생성** → 모델이 유용한 패턴을 감지

  <br/>

####  매달 마지막 주말에 대부분의 판매가 발생하는 온라인 상점, 달의 마지막 주말을 인식하는 모델을 만들어보자!

- **Unix 시간:** 
  - *시간을 가장 간단하게 표현*하는 방법, 1970.01.01 0시 0분 0초 부터 지금까지의 시간을 초로 나타냄
  - 2018년의 마지막 주말 →  *Unix. 1546041600 ~ 1546214399* 
  - 달마다 주말의 날짜와 유닉스 시간 범위가 다른데.. 모델이 패턴을 찾을 수 있을까..?🤔
    - ❗특성을 생성해 문제를 해결해보자❗

<br/>

- **요일과 일자 추출:** 
  - 명확하게 날짜를 표현하기 위해 요일과 일자를 별도의 속성으로 추출해보자!
  - 2018년의 마지막 주말 →  *일요일 (0), 일자(30일)*
  -  모델이 주말(0과 6)을 학습하기 쉽고, 월말에 높은 판매가 일어난다는 것도 감지
  - 단, 모델에 편향을 추가한다! → 금요일(5)이 월요일(1)보다 다섯 배 큼 → 이런 수치 기준은 표현 방식 때문에 발 생, 학습용을 부적절ㅜㅜ

<br/>

- **교차 특성(Feature Cross):** 

  -  간단히 두 개 이상의 특성을 **곱해서** 만드는 특성 → 여러 특성의 값을 **비선형**으로 조합하면 모델이 더 쉽게 판별

    <img src="https://miro.medium.com/v2/resize:fit:1400/0*8GYA3Ki2SpVkiOv0.png" alt="feature" style="zoom:37%;" />

<br/>

- **모델에게 정답 제공하기**:
  - 특성을 조합한 어떤 값이 예측에 특히 효과적이라는 사실을 안다면, 이런 특성이 연관성 있는 조합을 만들 때만 1이 되는 **새로운 이진 특성 생성**
  - 예상대로 마지막 주말을 예측할 수 있다면 모델이 이 특성을 활용하여 훨씬 더 높은 정확도 달성
  - 💡 복잡한 작업에서 고군분투하는 모델보다 간단한 작업에서 잘 동작하는 모델이 더 낫다💡



<br/>

### 4.4.2 머신러닝 에디터 특징



<br/>

## 4.5 로버트 먼로: 데이터를 찾고, 레이블링하고, 활용하는 방법

<img src="https://i.ytimg.com/vi/TkPkx7EYcR0/hq720.jpg?sqp=-oaymwEhCK4FEIIDSFryq4qpAxMIARUAAAAAGAElAADIQj0AgKJD&rs=AOn4CLDlPoCV4SaFSzxVA9ji-sbzueCnrA" alt="ro" style="zoom:50%;" />

- 머신러닝 프로젝트는 어떻게 시작?

  - **비즈니스 문제로 시작!**

- 시작할 때 얼마나 많은 데이터가 필요한가?

  - 대표적이고, 다양성을 가진 데이터셋 필요
  - 군집 알고리즘을 적용하고, 이상치를 살펴보기
  - 일반적인 경우, 희귀 범주에 속하는 샘플 1000개를 레이블링하면 잘 작동 (현재 모델링 방식을 유지할지 판단 지표)
  - 더 많은 데이터를 모을수록 정확도가 천천히 향상

- 데이터를 수집하고 레이블링 할 때 거치는 과정은?

  - **불확실성 기반 샘플링**

    - 모델이 가장 불확실한 샘플 식별
    - 결정 경계 근처의 유사 샘플 추가

    **오류 모델 활용**

    - 현재 모델의 실수를 레이블로 활용
    - 실패 가능성 높은 샘플 예측에 활용

    **레이블링 모델 활용**

    - 레이블된/안된 데이터로 이진 분류기 훈련
    - 기존 레이블 데이터와 가장 다른 샘플 식별

  - 모델이 유용한 것을 학습하고 있는지 검증하는 방법은?

    - **균형잡힌 데이터 수집**

      - 특정 영역에만 집중하는 것 지양
      - 다양한 케이스 포함 필요

      **검증 방법**

      - 테스트 세트는 반드시 랜덤 샘플링
      - 배포된 모델의 성능 모니터링
      - 불확실성 추적 및 비즈니스 지표와 연계

      **성능 저하 감지**

      - 사용 지표 모니터링
      - 훈련 세트 업데이트 시점 판단









참고

https://deep-diver-csp.tistory.com/7

https://blog.insightdatascience.com/automating-customer-support-when-you-lack-data-e9975fd8a053

https://noduslabs.com/cases/tutorial-lda-text-mining-network-analysis/
# Chap3. 엔드투엔드 파이프라인 만들기

> 실제로 작동하는 초기 프로토타입 시스템을 만드는 것이 모델 성능을 발전시킬 수 있는 최선의 방법!
>
> ⭕**실행가능한 소프트웨어**를 **점진적**으로 발전시키자⭕

<img src="https://blog.crisp.se/wp-content/uploads/2016/01/Making-sense-of-MVP-.jpg" alt="pipe" style="zoom:67%;" />

<br/>

## 3.1 가장 간단한 프로토타입

- ***추론파이프라인***을 통해 사용자가 모델의 결과가 어떻게 상호작용하는지 점검
- 모델 훈련 대신 간단한 규칙/경험법칙을 통해 시작
  - EX. HackerRank 코드 수행 측정 모델
    - 괄호 개수 확인하기  → Abstract Syntax Tres 로 더 복잡한 정보를 추출하는 모델링에 초점을 맞추는 직관을 얻은 첫 단계
  - EX. 나무 개수 카운트 모델 
    - 녹색 픽셀 비율 기반 나무 밀도 측정  → 우거진 숲에서는 적합하지 않음  → 밀집되어 있는 나무를 인식하는 파이프라인을 구축하는 첫 단계
- 전문가 지식 & 데이터 탐색을 통해 규칙 고안  → 초기 가정 검증, 반복 (빠르게)
- 입력 데이터  → 전처리  → 규칙 적용  → 결과 제공 파이프라인 생성 (**MVP**)
  - Web App, Terminal (Script), ....

<br/>

## 3.2 머신러닝 에디터 프로토타입

> ***일반적인 교정 권고 사항***을 활용 → 좋은 질문/나쁜 질문에 대한 규칙을 만들고, 사용자에게 보여주자!

```python
# 사용하게 될 함수들
input_text = parse_arguments()
processed = clean_input(input_text)
tokenized_sentences = preprocess_input(processed)
suggestions = get_suggestions(tokenized_sentences)

# 설치할 모듈
pip install argparse
nltk.download('punkt_tab')
pip install pyphen
```



<br/>

#### 3.2.1  데이터 파싱과 정제

```python
# 파싱
def parse_arguments():
    """
    간단한 명령줄 매개변수 파서
    :return: 수정할 텍스트
    """
    
    # ArgumentParser 객체 생성 - 프로그램의 인자를 처리하는 파서
    parser = argparse.ArgumentParser(
        description="수정할 텍스트를 입력 합니다"  # 프로그램 설명 추가
    )

    # 위치 인자(positional argument) 추가
    parser.add_argument(
        'text',                # 인자 이름
        metavar='input_text',  # 도움말에 표시될 인자 이름
        type=str              # 입력값을 문자열로 처리
    )

    # 입력받은 인자들을 파싱
    args = parser.parse_args()
    
    # 파싱된 text 인자 값 반환
    return args.text
```



<br/>

```python
# 정제
def clean_input(text):
    """
    텍스트 정제 함수
    :param text: 사용자가 입력한 텍스트
    :return: ASCII 이외의 문자를 제거한 정제된 텍스트
    """
    # ASCII 문자만 남기고 나머지는 제거
    # text.encode() : 문자열을 UTF-8 바이트로 인코딩
    # decode('ascii', errors='ignore') : 
    #     - ASCII로 디코딩하면서 ASCII가 아닌 문자는 무시
    #     - errors='ignore' 옵션으로 변환할 수 없는 문자 건너뜀
    return str(text.encode().decode('ascii', errors='ignore'))
```

```python
text = "Hello 안녕 World! 🌎"
cleaned = clean_input(text)
print(cleaned)  # 출력: Hello World!
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/pi1.png?raw=true" alt="ㅔㅑ1" style="zoom:80%;" />

<br/>

#### 3.2.2 텍스트 토큰화 (Tokenization)

> 단어 수준의 통계를 계산하기 위해 문장에서 단어를 식별
>
> - 공백/구두점 기준으로 입력 텍스트를 단어로 나눔 →  실제로 적용하기는 어려움
> - 💡**NLTK** (오픈 소스 라이브러리) 사용!

```python
def preprocess_input(text):
   """
   정제된 텍스트를 토큰화합니다
   :param text: 정제된 텍스트
   :return: 문장과 단어로 토큰화하여 분석에 투입할 준비를 마친 텍스트
   """
   # nltk.sent_tokenize(): 텍스트를 문장 단위로 분리
   # 마침표, 느낌표, 물음표 등을 기준으로 문장을 구분
   sentences = nltk.sent_tokenize(text)

   # 각 문장을 다시 단어 단위로 분리
   # nltk.word_tokenize(): 공백, 구두점 등을 기준으로 단어를 분리
   # 모든 문장에 대해 단어 토큰화 수행 (sentence in sentences = List Comprehension)
   tokens = [nltk.word_tokenize(sentence) for sentence in sentences]

   return tokens
```

```python
text = "Hello! How are you? I am doing well."
result = preprocess_input(text)
print(cleaned)
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/pi2.png?raw=true" alt="ㅔㅑ1" style="zoom:80%;" />

<br/>

#### 3.2.3 특성 생성하기

- 사용자에게 전달한 조언을 위한 규칙 생성
  - 자주 사용되는 동사, 연결어의 빈도 count
  - wh- 접속사를 카운트 (why what where who..)
  - Flesh 가독성 점수 계산

- 위 통계값을 모아 사용자에게 전달!!

```python
import pyphen

def compute_flesch_reading_ease(total_syllables, total_words, total_sentences):
    """
    요약 통계로부터 가독성 점수를 계산합니다.
    :param total_syllables: 입력 텍스트에 있는 음절 개수
    :param total_words: 입력 텍스트에 있는 단어 개수
    :param total_sentences: 입력 텍스트에 있는 문장 개수
    :return: A readability score: 점수가 낮을수록 더 복잡한 텍스트입니다.
    """
    return (
        206.85
        - 1.015 * (total_words / total_sentences)
        - 84.6 * (total_syllables / total_words)
    )


def get_reading_level_from_flesch(flesch_score):
    """
    https://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_tests 에서 가져온 임곗값
    :param flesch_score:
    :return: 플레시 점수에 대한 가독성 수준
    """
    if flesch_score < 30:
        return "매우 읽기 어려움"
    elif flesch_score < 50:
        return "읽기 어려움"
    elif flesch_score < 60:
        return "약간 읽기 어려움"
    elif flesch_score < 70:
        return "보통"
    elif flesch_score < 80:
        return "약간 읽기 쉬움"
    elif flesch_score < 90:
        return "읽기 쉬움"
    else:
        return "매우 읽기 쉬움"


def compute_average_word_length(tokens):
    """
    한 문장에 있는 단어의 길이를 계산합니다.
    :param tokens: 단얼 리스트
    :return: 리스트에 있는 단어의 평균 길이
    """
    word_lengths = [len(word) for word in tokens]
    return sum(word_lengths) / len(word_lengths)


def compute_total_average_word_length(sentence_list):
    """
    여러 문장에 대한 단어의 평균 길이를 계산합니다.
    :param sentence_list: 단어의 리스트로 구성된 문장 리스트
    :return: 문장 리스트에 있는 단어의 평균 길이
    """
    lengths = [compute_average_word_length(tokens) for tokens in sentence_list]
    return sum(lengths) / len(lengths)


def compute_total_unique_words_fraction(sentence_list):
    """
    고유한 단어의 비율을 계산합니다.
    :param sentence_list: 단어의 리스트로 구성된 문장 리스트
    :return: 문장에 있는 고유한 단어의 비율
    """
    all_words = [word for word_list in sentence_list for word in word_list]
    unique_words = set(all_words)
    return len(unique_words) / len(all_words)


def count_word_usage(tokens, word_list):
    """
    주어진 단어 리스트의 등장 횟수
    :param tokens: 한 문장의 토큰 리스트
    :param word_list: 탐색하려는 단어 리스트
    :return: 리스트에 등장하는 단어 횟수
    """
    return len([word for word in tokens if word.lower() in word_list])


def count_word_syllables(word):
    """
    단어에 있는 음절 횟수
    :param word: 하나의 단어 문자열
    :return: pyphen으로 구한 음절 개수
    """
    dic = pyphen.Pyphen(lang="en_US")
    # 음절 사이에 하이픈("-")을 추가한 단어를 반환합니다.
    hyphenated = dic.inserted(word)
    return len(hyphenated.split("-"))


def count_sentence_syllables(tokens):
    """
    문장에 있는 음절 개수를 셉니다.
    :param tokens: 단어와 구둣점의 리스트
    :return: 문장에 있는 음절 개수
    """
    # 토큰화 객체는 구둣점을 별도의 단어로 인식하기 때문에 여기서는 이를 필터링합니다.
    punctuation = ".,!?/"
    return sum(
        [
            count_word_syllables(word)
            for word in tokens
            if word not in punctuation
        ]
    )


def count_total_syllables(sentence_list):
    """
    문장 리스트에 있는 음절을 셉니다.
    :param sentence_list: 단어의 리스트로 구성된 문장 리스트
    :return: 문장에 있는 음절의 개수
    """
    return sum(
        [count_sentence_syllables(sentence) for sentence in sentence_list]
    )


def count_words_per_sentence(sentence_tokens):
    """
    문장에 있는 단어를 셉니다.
    :param sentence_tokens: 단어와 구둣점의 리스트
    :return: 문장에 있는 단어의 개수
    """
    punctuation = ".,!?/"
    return len([word for word in sentence_tokens if word not in punctuation])


def count_total_words(sentence_list):
    """
    문장 리스트에 있는 단어를 셉니다.
    :param sentence_list: 단어의 리스트로 구성된 문장 리스트
    :return: 문장에 있는 단어의 개수
    """
    return sum(
        [count_words_per_sentence(sentence) for sentence in sentence_list]
    )

def get_suggestions(sentence_list):
   """
   추천을 포함한 문자열을 반환합니다.
   :param sentence_list: 문장의 리스트. 각 문장은 단어의 리스트입니다.
   :return: 입력 텍스트를 개선하기 위한 추천사항들을 포함한 문자열
   """
   # 특정 단어들의 사용 빈도 계산
   told_said_usage = sum(
       count_word_usage(tokens, ["told", "said"]) 
       for tokens in sentence_list
   )
   
   but_and_usage = sum(
       count_word_usage(tokens, ["but", "and"]) 
       for tokens in sentence_list
   )
   
   # wh로 시작하는 부사들의 사용 빈도 계산
   wh_adverbs_usage = sum(
       count_word_usage(
           tokens,
           ["when", "where", "why", "whence", "whereby", "wherein", "whereupon"]
       ) for tokens in sentence_list
   )
   
   # 결과 문자열 생성 시작
   result_str = ""
   
   # 부사 사용에 대한 통계 추가
   adverb_usage = "told/said 사용: %d, but/and 사용: %d, wh-부사 사용: %d" % (
       told_said_usage,
       but_and_usage,
       wh_adverbs_usage
   )
   result_str += adverb_usage

   # 단어 길이와 다양성에 대한 통계 계산
   average_word_length = compute_total_average_word_length(sentence_list)
   unique_words_fraction = compute_total_unique_words_fraction(sentence_list)
   
   # 단어 통계 문자열 생성
   word_stats = "단어의 평균 길이: %.2f, 고유한 단어의 비율: %.2f" % (
       average_word_length,
       unique_words_fraction
   )
   result_str += "<br/>"  # HTML 줄바꿈 태그
   result_str += "\n"
   result_str += word_stats

   # 음절, 단어, 문장 수 계산
   number_of_syllables = count_total_syllables(sentence_list)
   number_of_words = count_total_words(sentence_list)
   number_of_sentences = len(sentence_list)
   
   # 기본 통계 문자열 생성
   syllable_counts = "%d개 음절, %d개 단어, %d개 문장" % (
       number_of_syllables,
       number_of_words,
       number_of_sentences
   )
   result_str += "<br/>"
   result_str += "\n"
   result_str += syllable_counts

   # Flesch Reading Ease 점수 계산 및 해석
   flesch_score = compute_flesch_reading_ease(
       number_of_syllables, 
       number_of_words, 
       number_of_sentences
   )
   
   flesch = "%.2f: %s" % (
       flesch_score,
       get_reading_level_from_flesch(flesch_score)
   )
   result_str += "<br/>"
   result_str += "\n"
   result_str += flesch

   return result_str
```

```python
# 예시 텍스트로 테스트
text = [
    ["I", "told", "him", "about", "the", "book"],
    ["He", "said", "it", "was", "interesting"],
    ["When", "and", "where", "did", "you", "read", "it"]
]

suggestions = get_suggestions(text)
print(suggestions)
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241228114008989.png?raw=true" alt="image-20241228114008989" style="zoom:80%;" />

<br/>

## 3.3 Workflow 테스트하기

#### 3.3.1 사용자 경험

- 모델의 품질과는 별개로 *사용성의 만족도* 확인 = *가장 바람직한 형태*로 결과를 제공하고 있는가

  - 제시한 결과가 유요한가 or 모델을 개선해야 하는가

  <br/>

#### 3.3.2 모델링 결과

- **선택한 측정지표**로 평가 반복
  - EX. 렌터카 검색 시스템 → [할인 누적 이득] 지표 사용 (가장 관련 있는 항목이 다른 것보다 먼저 반환될 시 높은 점수 부여하는 방식으로 순위 품질 측정) 
    - DCG5(5개 결과 중 유용한 추천이 적어도 하나는 있어야 한다) → 사용자가 출력 3개만 고려한다면❓ → DCG3
- **성능 병목** 찾기
  - 제품 부분: EX. 연구 논문 이미지로 콘퍼런스 통과 예측 모델 → 거절될 확률 **+** 논문 개선 조언
  - 모델 부분: EX. 신용 점수 예측 모델  → 특정 인종의 체납 가능성 높게 출력
    - 사용하는 훈련 데이터가 ***편향***  → 데이터 정제/증식 파이프라인 생성 해야함  → *모델 수정* 필요

<br/>



## 3.4 머신러닝 에디터 프로토타입 평가

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241229152957074.png?raw=true" alt="image-20241229152957074" style="zoom:67%;" />

<br/>

#### 3.4.1 모델

- 결과가 좋은 품질의 글쓰기와 관련 있는가?  → ❌
  - 복잡한 문장의 가독성 점수 = 전체 문단의 가독성 점수  → 추출된 속성값이 '좋은 글쓰기' 와는 관련 없음

#### 3.4.2 사용자 경험

- 반환된 정보가 너무 장황하고 관련성이 없음
  - 가독성 점수는 품질 지표이지만, *질문을 개선하는데는 도움이 되지 못함*
- wh- 접속사를 적게 사용하도록 수정을 제안한다면❓조금 더 세부적으로 단어/문장 수준의 변화를 제안한다면❓
  - EX. I lost Password. What do?
    - 가독성 나쁨 → 어떤 제품인지 명시하세요. 가독성이 나쁩니다.









참고

https://blog.crisp.se/2016/01/25/henrikkniberg/making-sense-of-mvp
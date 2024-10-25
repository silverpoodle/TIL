# DALL-E 3

- OpenAI 에서 개발한 이미지 생성 모델
- 텍스트 기반으로 이미지 생성
- ChatGPT 와 연동 -> 보다 효율적인 프롬프트 생성 가능
  - 이전 DALL-E 모델에 비해 프롬프트 설정 과정 간소, 직관적으로 입력 조절 가능
  - 이미지 생성 효율성 높음

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241025110403027.png?raw=true" alt="image" style="zoom:60%;" />



### 장점

- 창의적인 이미지 생성
- 고해상도 출력
- 프롬프트 이해력 샹상
- 사용자 친화적 인터페이스
- ChatGPT 통합

### 단점

- 정확성의 한계
- 편향된 결과 : 학습 데이터에 따라 특정 주제/스타일링에 편향된 결과 생성
- 해석의 주관성 : 입력된 텍스트에 대한 해석이 주관적일 수 있음
- 리소스 소모
- 법적/윤리적 문제 : 생성된 이미지의 저작권, 생성에 대한 법적 문제



<br/>

### 진행과정

#### 1. 텍스트 입력

- 텍스트 입력
- 텍스트 이해: 입력된 텍스트 분석, 이미지 생성에 필요한 키워드, 속성, 관계 등 추출

#### 2. 잠재 공간 생성

- 텍스트 벡터화 : 추출된 정보를 기반으로 텍스트 -> 고차원 벡터
  - 벡터는 텍스트의 의미를 수치적으로 표현
- 잠재 공간 생성: 텍스트 벡터 + 이미지 학습, 고차원 잠재 공간 생성
  - 공간은 텍스트와 이미지 간의 관계 포착

#### 3. 이미지 생성

- 조건부 생성 모델: 잠재 공간에서 텍스트 벡터에 해당하는 영역 찾고, 조건으로 새로운 이미지 생성
- 디테일 추가: 생성된 이미지에 대한 추가적인 조정 -> 더욱 사실적, 세밀함
  - 스타일, 색상, 구성 등을 조절

#### 4. 이미지 출력

- 최종 이미지 생성: 생성된 이미지를 사용자에게 보여즘
- 반복: 사용자는 생성된 이미지에 대한 피드백을 제공, 모델은 이를 바탕으로 이미지 개선



<br/>

## Diffusion 과 비교

| 구분                 | DALL-E 3                                                     | Diffusion Model                                              |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **기본 원리**        | • GPT-3 변형 모델 사용<br>• 텍스트 프롬프트 기반 이미지 생성<br>• 텍스트 이해와 이미지 생성 결합 | • 노이즈 있는 이미지에서 시작<br>• 점진적 노이즈 제거 방식<br>• 픽셀 단위 점진적 개선 |
| **이미지 생성 과정** | • 텍스트를 벡터로 인코딩<br>• 벡터 기반 이미지 생성<br>• 다중 레이어를 통한 세부 요소 조합 | • 랜덤 노이즈에서 시작<br>• 다단계 노이즈 제거<br>• 단계별 이미지 예측 및 개선 |
| **적용 및 활용**     | • 텍스트 기반 이미지 생성 특화<br>• 창의적/독창적 이미지 생성<br>• 다양한 스타일과 주제 표현 가능 | • 범용적 활용 가능<br>• 이미지 복원 및 변환<br>• 고해상도 이미지 생성에 강점 |



<br/>

## 활용 사례

- 고해상도 이미지 생성
- 이미지 변환/복원
- 디자인/예술 창작
- 교육 / 학습 자료 제작



<br/>



## 실습

```python
# 필요한 라이브러리 설치
!pip install openai requests pillow

# 필요한 라이브러리 임포트
from openai import AzureOpenAI
import os
import requests
from PIL import Image
import json
from io import BytesIO
from keybert import KeyBERT
from transformers import pipeline
from googleapiclient.discovery import build

# 환경 변수 설정
os.environ["AZURE_OPENAI_API_KEY"] = "AZURE_OPENAI_API_KEY"
os.environ["AZURE_OPENAI_ENDPOINT"] = "AZURE_OPENAI_ENDPOINT"

# Azure OpenAI 클라이언트 초기화
client = AzureOpenAI(
    api_version="2024-02-01",
    api_key=os.environ["AZURE_OPENAI_API_KEY"], # 환경 변수에서 API 키 가져오기
    azure_endpoint=os.environ['AZURE_OPENAI_ENDPOINT'] # 환경 변수에서 엔드포인트 가져오기
)


# DuckDuckGo 검색을 수행하는 함수
def duckduckgo_search(query):
    url = f'https://api.duckduckgo.com/?q={query}&format=json'
    response = requests.get(url)
    return response.json().get('Abstract', "No information found.")

# 키워드 추출 함수
def extract_keywords(prompt):
    kw_model = KeyBERT()
    keywords = kw_model.extract_keywords(prompt, keyphrase_ngram_range=(1, 1), stop_words=None, top_n=1)
    return keywords[0][0] if keywords else None

# 프롬프트 확장 함수
def expand_prompt(original_prompt):
    keyword = extract_keywords(original_prompt)
    if keyword:
        # DuckDuckGo API를 사용하여 키워드 관련 정보를 검색
        additional_info = duckduckgo_search(keyword)
        return f"{original_prompt}. Additionally, {additional_info}"
    else:
        return original_prompt
    
# JSON 응답을 파싱
json_response = json.loads(result.model_dump_json())

# 프롬프트 입력 및 확장
user_prompt = input("이미지를 생성할 프롬프트를 입력하세요: ")
expanded_prompt = expand_prompt(user_prompt)


# DALL-E 3 모델을 사용하여 이미지 생성 메시지 보내기
result = client.images.generate(
    model="DALL-E 3 배포 이름",
    prompt="[프롬프트]", # 생성할 이미지 설명
    n=1 # 생성할 이미지 수
)

# 필요한 라이브러리 임포트
from IPython.display import display # 이미지를 Colab에서 출력하기 위한 라이브러리

# 생성된 이미지 가져오기
image_url = json_response["data"][0]["url"] # 응답에서 이미지 URL 추출
generated_image = requests.get(image_url).content # 이미지를 다운로드

# 이미지 데이터를 PIL을 사용하여 열기
image = Image.open(BytesIO(generated_image))

# 이미지 출력
display(image) # IPython.display의 display 함수 사용
```



<br/>

### 문제 1

DaLL-E 3는 **OpenAI** 에서 개발한 이미지 생성 모델로, 텍스트 설명을 기반으로 이미지를 생성하는 인공지능입니다.

### 문제2

Dalle-3은 **ChatGPT** 와 연동되어 사용됨으로써 효율적인 프롬프트 생성 가능합니다.

### 문제 3

DALL-E3은 **사용자**가 입력한 텍스트의 맥락을 이해하고, 그에맞는 이미지를생성하는데 높은 성능 보유합니다.

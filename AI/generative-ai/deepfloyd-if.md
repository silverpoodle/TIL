# DeepFloyd-IF

- 텍스트 기반 고품질 / 초현실적 이미지 생성

- Diffusion Model 에서 사용했던 노이즈 기술 사용

  - 노이징을 통해 원하는 이미지 추출

- 3차원 공간에 대한 이해를 바탕으로 입체적인 이미지 생성 가능

  <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241025112001713.png?raw=true" alt="image" style="zoom:60%;" />



### 장점

- 빠르고 간편한 이미지 생성
- 다양한 스타일의 이미지 생성
- 높은 수준의 커스터마이징
- 높은 현실감

### 단점

- 정확성의 한계
- 편샹된 결과, 해석의 주관성
- 리소스 소모
- 오용 가능성: 딥페이크 등 악의적인 목적으로 사용



<br/>

## 진행과정

#### 1. 텍스트 입력 & 이해 (Transformer)

- 텍스트 입력
- 텍스트 이해 : 텍스트 -> 벡터 공간 ->  문맥 이해

#### 2. 잠재 공간 생성

- 텍스트 벡터화 -> 텍스트의 의미를 수치적으로 표현
- 잠재 공간 생성 -> 벡터 + 이미지 학습 -> 고차원 잠재 공간 생성

#### 3. 이미지 생성

- 노이즈 추가: 샘플링된 점에 점차적으로 노이즈 추가
- 노이즈 제거: 입력된 텍스트 정보를 활용하여 원하는 이미지의 특징 유지

#### 4. 이미지 출력





<br/>

## 특징

- **Transoformer, GAN, Diffusion 모델들을 조합하여 자체적인 구조**
- **클래스 조건부 생성**: 특정 클래스 (고양이, 강아지) 에 대한 이미지를 생성할 수 있도록 모델 학습 가능
- **스타일 전이**: 기존의 스타일 유지하면서 새로운 이미지 생성 가능
- 초고해상도 이미지 생성



<br/>

## 활용사례

- 마케팅 및 광고
- 엔터테인먼트 콘텐츠 제작: 웹사이트, 소셜 미디어 등
- 건축 및 인테리어 디자인
- 교육



<br/>

## 실습

```python
# 필요 라이브러리 다운로드
! pip install --upgrade \
diffusers~=0.16 \
transformers~=4.28 \
safetensors~=0.3 \
sentencepiece~=0.1 \
accelerate~=0.18 \
bitsandbytes~=0.38 \
torch~=2.3.1 -q
!pip install huggingface_hub –upgrade

#HugginFace Token을 이용한 연결
from huggingface_hub import login
login()

#transformers모듈 호출 / DeepFloyd/IF-I-XL-v1.0 모델 로드
from transformers import T5EncoderModel
text_encoder = T5EncoderModel.from_pretrained(
    "DeepFloyd/IF-I-XL-v1.0",
    subfolder="text_encoder",
    device_map="balanced",
    load_in_8bit=True,
    variant="8bit"
)
from diffusers import DiffusionPipeline
pipe = DiffusionPipeline.from_pretrained(
    "DeepFloyd/IF-I-XL-v1.0",
    text_encoder=text_encoder, # pass the previously instantiated 8bit text encoder
    unet=None,
    device_map="balanced"
)	

#파이프 라인 생성
pipe = DiffusionPipeline.from_pretrained(
    "DeepFloyd/IF-II-L-v1.0",
    text_encoder=None,
    variant="fp16",
    torch_dtype=torch.float16,
    device_map="balanced"
)

#이미지 생성
image = pipe(
    image=image,
    prompt_embeds=prompt_embeds,
    negative_prompt_embeds=negative_embeds,
    output_type="pt",
    generator=generator,
).images

#Pillow모듈을 이용한 이미지 출력
pil_image[0]
```



<br/>

### 문제 1

DeepFloyd-IF 모델은 **텍스트**를 기반으로 고품질 / 초현실적 이미지를 생성하는 데 특화된 AI기술입니다.

### 문제 2

DeepFloyd IF Model은 노이징을 통해 원하는 이미지를 추출이 가능한가요?

참✅

### 문제3

Deep Floyd IF Model은 3차원 공간에 대한 이해를 바탕으로 입체적인 이미지를 생성할 수 있나요?

참 ✅

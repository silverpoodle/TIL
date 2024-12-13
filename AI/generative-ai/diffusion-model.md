# Diffusion Model (확산 모델)

- 이미지에 **가우시안 잡음**을 더해가며 이미지를 흐릿하게 만들고 잡음을 제거하는 과정을 여러 번 반복하여 각 단계에서 잡음을 입력으로 받아 이전 단계의 이미지를 예측하는 모델.
- 대표 모델 : `Stable Diffusion`
-  딥러닝 분야에서 이미지, 텍스트 처리에 탁월한 성능을 보이는 딥러닝 모델
  - 데이터에 점진적으로 노이즈를 추가하는 **Forward Process(Diffusion Process)** 
  - 역으로 노이즈를 제거하는 **Reverse Process(Reverse Diffusion Process)**

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241024224644787.png?raw=true" alt="image" style="zoom:60%;" />



<br/>

### 장점

- 고품질 이미지 생성
- 다양한 응용: 이미지 복원, 텍스트 기반 생성, 등
- 안정적인 학습
- 샘플링 다양성: 다양한 스타일의 이미지 생성 가능

### 단점

- 학습 시간: 많은 시간, 컴퓨팅 자원 소모
- 복잡한 구조
- <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241024224855407.png?raw=true" alt="image" style="zoom:80%;" />
- 샘플링 속도 상대적 느림



<br/>

## Forward Process

- 원본 데이터에 점직적으로 노이즈를 추가, 데이터를 벼형
- 총 T 단계, 각 단계마다 이미지 흐려짐
  - 단계가 거듭될 수록 노이즈 양 줄어듦

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241024225031114.png?raw=true" alt="image" style="zoom:80%;" />



<br/>

## Reverse Process

- 노이즈 데이터에서 원래 데이터를 복원하는 과정

- 총 T 단계, 점점 선명해짐

  - 거듭될 수록 제거되는 노이즈 양 줄어듦
  - 초기에 큰 노이즈 제거, 후기에 작은 노이즈 제거하여 세부적 디테일 복원

  <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241024225212963.png?raw=true" alt="image" style="zoom:80%;" />



<br/>

## 노이즈? 

- 데이터의 **다양성** 확보: 노이즈를 추가함으로써 원본 데이터에 다양한 변형 적용가능 
- 데이터의 **일반화**: 노이즈를 추가하고 제거하는 과정을 반복하면서 모델은 특정 데이터에 과도하게 의존하지 않고, 데이터의 일반적인 특징을 학습 
- 복잡한 데이터 **분포 학습**: 실제 데이터는 매우 복잡한 분포를 가지고 있는데, 노이즈를 추가하고 제거하는 과정을 통해 모델은 이러한 복잡한 분포를 효과적으로 학습 
- 생성 과정의 **안정성**: 노이즈를 점진적으로 추가하고 제거하는 과정은 생성 과정을 안정적으로

> 사람은(확산 모델은) 캔버스에 아무것도 없는 상태(노이즈로 가득 찬 이미지상태)에서 시작하여, 붓(디테일을)으로 칠해나가며 그림을 완성한다.

<br/>

## 활용 사례

- Text-To-Image: 프롬프트 기반 고해상도 이미지 생성
- Image-To-Image: 손상된 이미지 복원, 선명도 향상 등
- Text-To-Video
- 의료 이미지 분석



<br/>

## 실습

```python
!pip install torch torchvision torchaudio --extra-index-url
https://download.pytorch.org/whl/cu113
!pip install diffusers

#필요한 모듈 임포트
import os
import torch
import matplotlib.pyplot as plt
from diffusers import StableDiffusionPipeline

#Hugging Face Token 환경 변수 설정
os.environ['HF_TOKEN'] = "Hugging Face Token"
hf_token = os.getenv('HF_TOKEN’)
                     
#Stable Diffusion 모델 로드
pipe = StableDiffusionPipeline.from_pretrained("stabilityai/stablediffusion-2-1", use_auth_token=hf_token).to("cuda")
                     
#이미지 생성에 들어갈 프롬포트 작성
prompt = "[프롬프트 내용]"
image = pipe(prompt).images[0]
                     
#이미지 출력
plt.imshow(image)
                     
#이미지 생성
image.save("/경로/diffusion_output_image.png")
```



<br/>

### 문제 1

이미지에 가우시안 잡음 더해가면 이미지를 흐릿하게 만들고 잡음을 제거하는 과정을 여러 번 반복하여 각 단계에서 잡음을 입력으로 받아 이전 단계의 이미지를 예측하는 모델은 무엇인가요?

확산 



### 문제 2

데이터에 점진적으로 노이즈를 추가하는 단계는 무슨 Processs인가요?

forward



###문제 3

조역으로 노이즈를 제거하는 단계는 무슨 Processs인가요?

reverse

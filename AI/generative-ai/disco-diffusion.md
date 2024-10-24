# Disco Diffusion

- 노이즈가 추가된 이미지에서 시작하여 점차적으로 노이즈를 제거하여 최종 이미지를 생성
- **U-Net 구조**를 활용하여 이미지의 세부 정보를 추출하고 노이즈를 제거하는데 효과적인 Diffusion 모델
- 생성된 이미지와 실제 이미지 간의 차이를 `최소화`하는 **손실 함수**를 사용하여 학습하고 노이즈 제거 능력을 향상

<br/>

### 장점

- 고품질 이미지 생성: 자연스럽고 사실적인 이미지를 생성 
- 다양한 스타일 응용: 이미지 생성 외에도 이미지 복원, 초해상도 이미지 생성, 텍스트 기반 이미지 생성 등 다양한 분야에 활용 가능 
- 안정적인 학습: 기존 생성 모델에 비해 학습이 안정적이고, 생성된 이미지의 품질이 균일 
- 샘플링 다양성: 다양한 스타일의 이미지를 생성할 수 있는 유연성 
- 강력한 일반화 능력: 예상치 못한 입력에 대해서도 유연하게 대응

### 단점 

- 연산 비용: Disco Diffusion Model은 계산량이 많아 학습과 추론에 상당한 시간이 소요
- 모델 크기: 모델의 파라미터 수가 많아 메모리 사용량이 증가 
- 학습 데이터 의존성: 모델의 성능은 학습 데이터의 품질과 양에 크게 의존. 데이터가 부족하거나 편향되어 있는 경우, 결과물의 품질과 다양성이 저하
- 노이즈 제거의 한계: 노이즈 제거 과정이 잘못되거나 부정확할 경우, 최종 이미지 품질이 떨어짐. 따라서 모델의 튜닝이 필요
- 제어의 어려움: 생성 과정에서 특정한 결과를 얻기 위해서는 텍스트 입력이나 파라미터 조정이 필요하지만, 원하는 결과를 얻기 위해 세밀한 조정이 어려움

<br/>



## Stable Diffusion 와의 차이점

| 특성            | Disco Diffusion Model                                      | Stable Diffusion Model                                       |
| --------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| **규모**        | 비교적 작은 모델                                           | 대규모 모델                                                  |
| **주요 용도**   | 특정 스타일/주제 중심 아트워크 생성                        | 일반화된 이미지 생성                                         |
| **이미지 품질** | 프롬프트와 훈련 정도에 따라 상이                           | 일반적으로 높은 품질, 실사적 결과물                          |
| **강점**        | • 스타일의 다양성<br>• 창의적 표현<br>• 다양한 분위기 연출 | • 복잡한 이미지 생성<br>• 안정적인 결과물<br>• 효율적인 처리 |
| **개발 목적**   | 연구 목적                                                  | 상업적 목적                                                  |
| **활용 분야**   | 예술 작품 창작                                             | • 비즈니스<br>• 게임<br>• 영화 산업                          |
| **데이터 학습** | 특정 스타일 중심                                           | 광범위한 데이터 학습                                         |



<br/>

## Stable Diffusion 와의 공통점

- 확산 모델 기반: 이미지를 점차적으로 생성해나가는 확산 모델을 기반. 
- 텍스트 기반 이미지 생성: 두 모델 모두 프롬포트를 입력하면 이미지를 생성하는 text to image Model
- 딥 러닝 기반: 방대한 양의 이미지 데이터를 학습하여, 텍스트와 이미지 간의 관계를 이해하고 새로운 이미지를 출력
- 높은 수준의 창의성: 단순 이미지 복제가 아닌, 주어진 프롬포트르 기반으로 새로운 이미지를 생성



<br/>

## 활용 사례

- 개인화
- 가상 현실 건축:
- 실시간 맞춤형 생성
- 시각적 학습 자료 생성



<br/>

## 실습

```python
#라이브러리 다운로드
!pip install torch
!pip install opencv-python
!pip install Pillow
!pip install numpy
!pip install tqdm
!pip install midas
!pip install py3d-tools
!pip install disco-xform-utils
!pip install raft

# MiDaS 깊이 모델 초기화
def init_midas_depth_model(midas_model_type="dpt_large", optimize=True):
    
# 모델 및 설정 변수 초기화
midas_model = None
net_w, net_h = None, None
resize_mode, normalization = None, None

# 선택된 모델 경로 로드
midas_model_path = default_models[midas_model_type]

# 모델 유형에 따라 초기화
if midas_model_type == "dpt_large":
midas_model = DPTDepthModel(path=midas_model_path, backbone="vitl16_384", non_negative=True)
net_w, net_h = 384, 384
normalization = NormalizeImage(mean=[0.5, 0.5, 0.5], std=[0.5, 0.5, 0.5])
elif midas_model_type == "midas_v21":
midas_model = MidasNet(midas_model_path, non_negative=True)
net_w, net_h = 384, 384
normalization = NormalizeImage(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])

# 이미지 전처리를 위한 변환 정의
midas_transform = T.Compose([
Resize(net_w, net_h, resize_method=resize_mode, image_interpolation_method=cv2.INTER_CUBIC),
normalization,
PrepareForNet(),
])
midas_model.eval() # 모델을 평가 모드로 설정

# 최적화 설정
if optimize:
if DEVICE == torch.device("cuda"):
    
midas_model = midas_model.to(memory_format=torch.channels_last).half() # 메모리 포맷 및 반정밀도 변환
midas_model.to(DEVICE) # 지정된 디바이스로 모델 이동
return midas_model, midas_transform, net_w, net_h, resize_mode, normalization # 초기화된 모델 및 설정 반환

#이미지 이름
batch_name = 'tutorial'

#반복 횟수
steps = 250

#이미지 크기 조정
width_height_for_512x512_models = [500, 300] # <- 필요시 값 수정
tv_scale = 0
range_scale = 150
sat_scale = 0
cutn_batches = 4
skip_augs = False
width_height_for_256x256_models = [512, 448]

text_prompts = {
0: ["[이미지 설명 프롬프트 작성]"],
}
image_prompts = {
# 0:['ImagePromptsWorkButArentVeryGood.png:2',],
}
```


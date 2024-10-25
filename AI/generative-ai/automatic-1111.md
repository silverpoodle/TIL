# Automatic 1111

- Stable Diffusion 모델을 기반으로 한 웹 인터페이스
  - 사용자가 프롬프트 입력 -> 고해상도 이미지 생성
- 복잡한 명령 X, 다양한 옵셜 설정



### 장점

- 사용 용이성
- 고품질 이미지 생성
- 다양한 옵션, 커스터마이징
- 커뮤니티 지원

### 단점

- 시스템 요구사항 : GPU 필요, 많은 리소스 소모
- 초기 설치 복잡성
- 모델 의존성: 선택한 모델에 따라 이미지 품질 달라짐



<br/>

### 설치

#### 시스템 요구사항

- NVIDIA GPU (최소 8GB VRAM 권장)
- Windows 10 이상
- Python 3.8 이상

#### 설치 단계

1. **Python 설치**

    [Python 공식 웹사이트](https://www.python.org/downloads/windows/)에서 최신 버전을 다운로드하고 설치

   설치할 때 "Add Python to PATH" 옵션을 체크

   ![image](https://github.com/user-attachments/assets/433b36da-b0ed-4621-beb8-0d59124b22b1)


3. **Git 설치**

   Git을 설치합니다. [Git 공식 웹사이트](https://git-scm.com/download/win)에서 Windows용 Git을 다운로드하고 설치

4. **Stable Diffusion 리포지토리 클론**

   명령 프롬프트를 열고 Stable Diffusion의 Automatic1111 리포지토리를 클론

   ```bash
   git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
   cd stable-diffusion-webui
   ```

5. **webui-user.bat파일 실행**
   Running on local URL: http://127.0.0.1:7860
   위와 같은 메세지가 출력되는데, 위 링크를 크롬으로 접속해서 사용

   ![image](https://github.com/user-attachments/assets/92492261-b7b2-4f01-ae0a-44e7037c4705)



<br/>

### 문제 1

Automactic1111은 Stable Diffusion 모델을 기반으로 한 웹 인터페이스로, 사용자가 텍스트 프롬프트를 입력하여 **고해상도**의 이미지를 생성할 수 있도록 설계된 도구입니다.



### 문제 2

Automatic 1111은 사용자가 쉽게 접근할 수 있는 **웹 인터페이스** 을 제공하여, 복잡한 명령어 없이도 이미지 생성이 가능합니다.



### 문제 3

Automatic 1111은 다양한 옵션을 설정함으로써 해상도, 스타일, 사이즈등 원하는 결과를 구체적으로 설정이 가능한가요?

참 ![정답](https://learn.hansung.ac.kr/theme/image.php?theme=coursemosv2&component=core&rev=1729803602&image=i%2Fgrade_correct)
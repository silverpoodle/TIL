# 가상 환경

Virtual Environment(가상 환경)는 Python 프로젝트를 **독립적으로 관리**하기 위한 도구

<img src="https://miro.medium.com/v2/resize:fit:946/1*dVAQy_UxF2DfBAuWJDkNCg.png" alt="ㅇ" style="zoom:47%;" />

<br/>

## 1. 필요한 이유

* 프로젝트별 독립적인 패키지 관리가 가능
* 서로 다른 버전의 라이브러리가 필요한 여러 프로젝트를 한 컴퓨터에서 작업
* 패키지 충돌을 방지
  * EX) 프로젝트 A는 TensorFlow 1.x를 사용하고 프로젝트 B는 TensorFlow 2.x를 사용

* `requirements.txt`를 통해 프로젝트 환경을 쉽게 재현

<br/>

<br/>

## 2. 사용하는 상황

### 개발 단계
* 새로운 Python 프로젝트를 시작할 때
* 오픈 소스 프로젝트를 로컬에서 개발할 때
* 다른 개발자의 프로젝트를 실행하거나 테스트할 때
* 여러 버전의 Python을 사용해야 하는 경우

### 배포 단계
* Docker 컨테이너에 Python 애플리케이션을 배포할 때
* 클라우드 환경에 애플리케이션을 배포할 때
* CI/CD 파이프라인에서 테스트 환경을 구성할 때

<br/>

<br/>

## 3. 명령어

### 3.1 venv  (Python 3.3+)
```bash
# 가상환경 생성
python -m venv env-name

# 가상환경 활성화
# Windows
myenv\Scripts\activate
# macOS/Linux
source myenv/bin/activate

# 가상환경 비활성화
deactivate
```

<br/>

### 3.2 pip 관련 명령어

```bash
# 현재 설치된 패키지 확인
pip list

# 패키지 설치
pip install package_name

# 특정 버전 패키지 설치
pip install package_name==1.0.0

# 설치된 패키지 목록 저장
pip freeze > requirements.txt

# requirements.txt의 패키지 설치
pip install -r requirements.txt
```

<br/>

### 3.3 프로젝트 구조 예시
```
my_project/
├── myenv/              # 가상환경 디렉토리
├── src/               # 소스 코드
├── tests/             # 테스트 코드
├── requirements.txt   # 의존성 목록
└── README.md
```

* `.gitignore`에 가상환경 디렉토리(예: myenv/)를 추가하여 버전 관리에서 제외
* 프로젝트마다 새로운 가상환경 생성
* requirements.txt는 정기적으로 업데이트
* 개발용과 프로덕션용 requirements 파일 분리 관리
  - requirements-dev.txt: 개발 도구 포함
  - requirements-prod.txt: 실제 운영에 필요한 패키지만 포함

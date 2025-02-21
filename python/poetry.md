# Poetry

Python 프로젝트의 의존성 관리와 패키지 배포를 도와주는 도구
`pyproject.toml` 파일을 사용하여 프로젝트 **설정과 의존성을 선언적으로 관리**

<img src="https://www.pythoncentral.io/wp-content/uploads/2024/11/poetry.png" alt="d" style="zoom:50%;" />

<br/>

## 1. Poetry 의 의존성 관리

### 1.1 toml 과 lock

- **선언적 의존성 관리**: `pyproject.toml` 파일을 통해 개발자는 필요한 패키지와 버전 범위를 지정하고, poetry가 이를 해결하고 관리
- **의존성 해결 및 잠금(poetry.lock)**: 호환 가능한 패키지 버전을 차장 `poetry.lock` 파일에 저장, 프로젝트가 다양한 환경에서도 일관된 의존성을 유지할 수 있도록 함

<br/>

### 1.2 의존성 추가 및 제거

```sh
poetry add <패키지명>          # 패키지 추가
poetry add <패키지명>@<버전>   # 특정 버전의 패키지 추가
poetry remove <패키지명>       # 패키지 제거
```

<br/><br/>

## 2. Poetry 프로젝트 설정 및 초기화

### 2.1 Poetry 설치

```sh
pip install poetry  # Poetry 설치
```

<br/>

### 2.2 프로젝트 초기화

```sh
poetry init  # 새로운 프로젝트 초기화 (설정 질문 포함)
poetry new <프로젝트명>  # 새로운 프로젝트 생성 (기본 디렉토리 구조 포함)
```

<br/>

### 2.3 프로젝트 환경 설정

```sh
poetry config --list   # 설정 목록 확인
poetry config <키> <값>  # 설정 값 변경
```

<br/><br/>

## 3. Poetry 환경 및 가상환경 관리

### 3.1 가상환경 생성 및 활성화

```sh
poetry install   # 의존성을 설치하고 가상환경 생성
poetry self add poetry-plugin-shell # shell 플러그인 설치
poetry shell     # 가상환경 활성화
poetry env use <python 경로>  # 특정 Python 버전 사용
```

<br/>

### 3.2 가상환경 제거 및 재설치

```sh
poetry env remove <환경명>  # 특정 가상환경 제거
poetry install --no-root  # 프로젝트를 제외한 의존성 재설치
```

<br/><br/>

## 4. Poetry 패키지 빌드 및 배포

### 4.1 패키지 빌드

```sh
poetry build  # 패키지를 빌드 (wheel 및 sdist 생성)
```

<br/>

### 4.2 패키지 배포

```sh
poetry publish --username <사용자명> --password <비밀번호>  # PyPI 배포
poetry publish --dry-run  # 실제 배포 없이 테스트 실행
```

<br/>

### 4.3 로컬 패키지 설치 및 사용

```sh
poetry add ./my-package-0.1.0.tar.gz  # 로컬 패키지 추가
```

<br/><br/>



## 5. Poetry 스크립트 및 실행

### 5.1 스크립트 실행

`pyproject.toml` 파일에 스크립트 추가:

```toml
[tool.poetry.scripts]
start = "my_module:main"
```

이후 실행:

```sh
poetry run start
```

<br/>

### 5.2 개별 명령 실행

```sh
poetry run python script.py  # 가상환경 내에서 특정 스크립트 실행
```

<br/><br/>



## 6. Poetry 의존성 업데이트

```sh
poetry update  # 모든 패키지 업데이트
poetry lock --no-update  # `poetry.lock`을 재생성 (버전 변경 없음)
poetry check  # 프로젝트의 의존성 및 설정 검증
```



<br/><br/>

## 7. Poetry와 FastAPI 연동

### 7.1 FastAPI 설치

```sh
poetry add fastapi uvicorn  # FastAPI 및 Uvicorn 설치
```

<br/>

### 7.2 FastAPI 실행

```sh
poetry run uvicorn main:app --reload  # FastAPI 서버 실행
```

<br/>

### 7.3 `main.py` 예제 코드

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Testing FastAPI with poetry"}
```

<br/><br/>



참고:

https://teddylee777.github.io/poetry/poetry-tutorial/

https://devspoon.tistory.com/179

https://geunuk.tistory.com/475

https://github.com/python-poetry/poetry-plugin-shell
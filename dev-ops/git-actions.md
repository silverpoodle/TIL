# Git Actions

<img src="https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fcdn-images-1.medium.com%2Fmax%2F2000%2F1%2A7Z5NDciyXIzGK791LriXrQ.png" alt="ga" style="zoom:80%;" />

#### 리포지토리에서 바로 소프트웨어 개발 워크플로를 자동화, 사용자 지정 및 실행

- **Workflow** 자동화
- **YAML** 형식의 파일 구성 (`.github/workflows`) 로 세부적 정의
- 다양한 `event`,`action` 로 복잡한 작업 설정 가능, 빌드/배포 파이프라인 구축

## 1. Components

<img src="https://docs.github.com/assets/cb-25535/mw-1440/images/help/actions/overview-actions-simple.webp" alt="wf" style="zoom:50%;" />

### 1.1 Workflow

- 하나 이상의 `job` 으로 구성된 *자동화 프로세스*
- Github Event (push, pull ..) 에 의해 trigger

### 1.2 Job

- Workflow 내에서 실행되는 *개별 작업 단위*
- 병렬 & 순차적 실행 모두 가능

### 1.3 Step

- Job 안에서 실행되는 개별 명령어/액션
- 각 단계는 독립적으로 실행
- 필요시 **캐싱** 가능

### 1.4 Action

- 재사용 가능한 코드 단위
- 특정 잡업 (빌드, 테스트, ..) 수행



<br/>

## 2. Runner

- GitHub Actions를 실행하면 **GitHub이 제공하는 관리형 가상 머신에서 작업**이 실행
- 필요 시 **Self-Hosted Runner**를 통해 자신이 준비한 환경에서 실행



참고

https://tech.kakao.com/posts/516

https://blog.devops.dev/a-deep-dive-into-devops-6-85f199efc3f8

https://engineers.ntt.com/entry/2022/11/04/084857
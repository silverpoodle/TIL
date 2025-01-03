# Docker

<img src="https://www.docker.com/wp-content/uploads/2021/11/docker-containerized-appliction-blue-border_2.png" alt="Docker containerized appliction blue border 2" style="zoom:35%;" />

#### 컨테이너 기술을 기반으로 애플리케이션을 신속하게 구축, 테스트 및 배포할 수 있는 소프트웨어 플랫폼

- ❗PC마다 환경이 다르기 때문에, 로컬에서 개발을 해, 서버에 올릴때 소스파일만 올리는 것으로는 문제❗
  - OS 구축, 포트 구성, 개발 툴 설치, 연동 환경 구성, 호환성을 위한 버전 고려... 🤢
- 💡**반복적이고, 불편한 세팅을 한번 해놓으면 쉽게 그 설정을 배포할 수 있다면?**💡



<br/>

## 1. 가상화 (VIRTUALIZATION)

![what is a virtualization techology](https://www.cloud4u.com/upload/medialibrary/e69/what-is-a-virtualization-techology.png)

**하나의 하드웨어를 *여러 개의 가상 머신으로 분할*해 효율적으로 사용 할 수 있게 해주는 기술**

<br/>

### 1.1 하이퍼바이저 (Hypervisor) 란? 

<img src="https://miro.medium.com/v2/resize:fit:786/format:webp/1*Ob3u2fORwzPPfiZovk3Mjw.png" alt="ㅍ" style="zoom:70%;" />

**가상화를 관리하는 소프트웨어로, 물리적 하드웨어 위에서 여러 가상 머신을 실행하고 제어**

- Type 1: 하드웨어 위에서 직접 실행되는 "Bare Metal" 하이퍼바이저
- Type 2: 호스트 운영 체제 위에서 실행되는 "Hosted Type" 하이퍼바이저

> - `가상화 호스트(Virtualization Host)`
>   하이퍼바이저(Hypervisor)가 실행되고 있는 물리적 서버
>
> - `호스트 OS (Host OS)`
>   하이퍼바이저가 설치된 물리적 컴퓨터의 운영 체제(OS)
>
> - `게스트 운영 체제(Guest Operating System)`
>   가상 머신(Virtual Machine) 내부에서 실행되는 운영 체제
>
> - `가상 머신(Virtual Machine)`
>   실제 하드웨어를 가상으로 복사한 형태로, 물리적 컴퓨터나 서버처럼 작동하는 애플리케이션

<br/>

### 1.2  가상화 유형

- **서버 가상화**
  물리적 서버를 여러 가상 서버로 분할하여 효율적으로 리소스를 사용하고 서비스를 배포

- **스토리지 가상화**
  다양한 스토리지 디바이스를 통합하여 단일 가상 스토리지로 만들고 관리 작업을 간소화
  네트워크 연결 스토리지(NAS) 및 스토리지 영역 네트워크(SAN)와 같은 물리적 스토리지 디바이스의 기능을 결합, 모든 물리적 데이터 스토리지를 사용하는 대규모 가상 스토리지 장치

- **네트워크 가상화**
  네트워크 리소스를 가상으로 결합해 중앙에서 관리하며
  소프트웨어 정의 네트워킹(SDN)과 네트워크 기능 가상화(NFV) 방식 등

- **데이터 가상화**
  다양한 소스와 형식의 데이터를 통합해 필요한 형식으로 제공하며 데이터 활용 유연성을 높임

- **애플리케이션 가상화**
  애플리케이션을 원래 설계된 운영 체제와 다른 환경에서도 실행할 수 있도록 지원

- **데스크톱 가상화**
  가상 머신에서 데스크톱 운영 체제를 실행하여 원격 액세스, 관리 효율성, 보안을 개선

<br/>

## 2. 컨테이너 (CONTAINER)

<img src="https://cloudnativenow.com/wp-content/uploads/2018/11/containerspic2.png" alt="Docker containerized appliction blue border 2" style="zoom:70%;" />

**호스트 os의 기능을 그대로 사용하면서, *프로세스를 격리*해 독립된 환경을 만드는 기술**

- 애플리케이션 계층에서 `코드-라이브러리-종속성`을 *하나로* 묶어주는 기술
- 여러 컨테이너가 한 대의 컴퓨터에서 *동시에* 실행
- 운영 체제(OS)의 커널을 여러 컨테이너들이 공유하면서 각각 *독립된* 프로세스로 실행
- VM(Virtual Machine) 보다 크기가 훨씬 작음 ⇒  리소스를 효율적으로 사용 가능, 이동성 높음

<br/>



## 3. 컨테이너 동작 원리

### 3.1 namespace 와 cgroup

- 도커에서는 여러개의 프로세스가 **커널을 공유**하며, **각자 동시에** **격리**되어 있는 프로세스로 동작

  - ❓*커널을 공유한다*❓
    1. 커널은 OS의 핵심 부분으로, 자원을 효율적으로 관리하고 프로세스 간의 통신을 조율
    2. 모든 프로세스는 운영체저의 커널을 공유
    3. 프로세서들이 커널을 공유하기 때문에 서로 간섭하지 않고 동작 가능!

  - ❓하나의 OS에서 자원을 관리하는데, 격리된 환경에서 자원을 사용하려는 충돌을 어떻게 회피 ❓

    ⇒  ❗리눅스의 `namespace`와 `cgroup`이라는 기능 사용❗

<br/>

- **namespace**: 프로세스 별로 리소스 사용을 분리

  - Hardware 자원 자체를 가상화 하는 것이 아니라, Linux 내의 자원을 가상화
    ```cmd
    pid name spaces # 프로세스 격리 처리 (독립된 프로세스 공간 할당)
    net name spaces # 네트워크 인터페이스
    ipc name spaces # IPC 자원에 대한 엑세스 관리
    mnt name spaces # 파일 시스템 포인트 관리
    uts name spaces # host name 할당
    ```

    

- **cgroup**: `Control Groups`의 약자로, 프로세스들이 사용할 수 있는 컴퓨팅 자원들을 제한하고 격리 시킬 수 있는 리눅스 커널의 기능

  - 메모리, CPU, I/O, 네트워크 등의 자원들을 제한

    <img src="https://i0.wp.com/duffy.fedorapeople.org/blog/designs/cgroups/diagram2.png" alt="ㅇ" style="zoom:67%;" />

<br/>

-  **즉, 컨테이너는 프로세스를 격리하고, 프로세스에 필요한 컴퓨팅 자원을 독립적으로 할당 / 격리하여 완벽히 격리된 가상 환경을 구축**

<br/>

## 4. 도커 이미지 (Docker Image)

<br/>

## 5. 도커 명령어

### 5.1  도커 시스템정보

```docker
# Docker 엔진의 버전 및 빌드 정보를 확인
docker version

# Docker 클라이언트의 버전 정보 확인
docker -v

# Docker 시스템에 대한 상세 정보 확인
# 엔진의 구성, 운영체제 정보, 컨테이너 및 이미지의 개수 등 docker 시스템에 대한 다양한 정보 제
docker system info

# Docker 시스템의 디스크 사용량 확인
# 엔진이 사용하는 디스크 공간 및 여유곤간, 그리고 사용중인 이미지 및 컨테이너의 디스크 사용량 등 확인가능
docker system df

# Docker 시스템의 디스크 사용량을 자세히 확인
# -v 옵션은 각컨테이너 및 이미지의 디스크 사용량을 자세히 표시해준다.
docker system df -v
```

<br/><br/>

### 5.2.1 컨테이너 실행

```docker
# 컨테이너 띄우기
docker container run <image> <command>

# EX. webserver라는 이름으로 가장 최신 niginx이미지를 백그라운드에서 80:80으로 포트포워딩해서 컨테이너를 띄워라
docker container run --name webserver -d -p 80:80 nginx:latest

# 컨테이너 쉘접속
docker exec -it <container-name> /bin/bash
```

<br/>

### 5.2.2 옵션 정리

```dockerfile
# detach로 백그라운드에서 실행을 의미
-d 

# 포트포워딩
-p

# 가장 최신의 이미지
:latest

# 컨테이너를 실행 할 때 컨테이너 쪽 표준 입력과의 연결을 그대로 유지
# 컨테이너 쪽 쉘에 들어가서 명령을 실행
-i

# 유사 터미널 기능을 활성화 하는 옵션
-t
```

<br/>

### 5.2.3 컨테이너 상태 확인

```docker
# 가동중인 컨테이너 상태 확인
docker container ps
# 축약버전
docker ps

# 꺼진 컨테이너도 확인하고싶다면 -a 옵션을 붙이면됨
docker ps -a

# 특정 컨테이너 확인
docker container stats <컨테이너 이름 or 번호>

# 컨테이너 쉘 접속
```

<br/>

### 5.2.4 컨테이너 연결

```docker
# 컨테이너에 터미널 연결
# 컨테이너 실행중에만 사용가
docker container attach <container-name>

# ctrl + c 를 하면 나올수잇다.
```

<br/>

### 5.2.5 컨테이너 종료/시작/재시작/삭제

```docker
# 종료
docker stop <container-name>

# 시작
docker start <container-name>

# 재시작
docker container restart <container-name>

# 삭제
docker container rm <container name>

# 강제 종료 및 삭제
docker container rm -f <container-name>
```

<br/>

### 5.2.6 컨테이너 로그

```docker
# 컨테이너 로그
docker container log [options] <container-name>
```

<br/><br/>

### 5.3 도커 이미지 명령어

```yaml
# Docker 레지스트리로부터 이미지를 내려받는 명령어
docker image pull [option] <image-name>[:tag]

ex)
# taegeun의 모든 이미지 다운로드
docker image pull -a taegeun

# 로컬 Docker 이미지 목록 표시 (옵션 및 레포지토리 필터링 가능)
docker image ls [option] [repository]

# 로컬 Docker 이미지 목록 표시
docker image ls
# 또는
docker images

# 특정 Docker 이미지의 상세 정보 표시
docker image inspect <image-name>[:tag]

# Docker 레지스트리에서 이미지 검색
docker search [option] <keyword>

# 로컬 Docker 이미지 삭제 (옵션 및 이미지 이름 지정)
docker image rm <option> <image-name>
```



<br/><br/>

참고

https://www.docker.com/resources/what-container/

https://aws.amazon.com/what-is/virtualization/

https://www.cloud4u.com/blog/how-virtualization-works/
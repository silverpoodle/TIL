# VPC in AWS

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250108204621033.png?raw=true" alt="image-20250108204621033" style="zoom:60%;" />

AWS 에서 제공하는 VPC 구성요소들을 결합하면 **사용자 정의 네트워크**를 만들고, AWS 리소스를 안전하고 효과적으로 관리할 수 있다!

<br/>

## 1. VPC (Virtual Private Cloud)

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250108205042535.png?raw=true" alt="image-20250108205042535" style="zoom:50%;" />

- **정의**: AWS 클라우드에서 사용자가 정의한 가상 네트워크 환경

  - 다른 사용자와 격리된 논리적 네트워크 제공
  - **CIDR 블록**으로 IP 주소 범위 지정 가능 (예: 10.0.0.0/16)
  - 다양한 AWS 리소스를 네트워크에 배치 및 관리

- 장점

  - **네트워크 격리**로 보안 강화

  - 사용자 정의 네트워크 설정 가능

  - 온프레미스 네트워크와 통합해 하이브리드 클라우드 구성 가능

    <br/>

## 2. Subnet

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250108205334439.png?raw=true" alt="image-20250108205334439" style="zoom:50%;" />

- **정의**: VPC 내에서 IP 주소 범위를 세분화한 네트워크 섹션
  - **Public Subnet**: 인터넷과 통신 가능. (*인터넷 게이트웨이* 연결 필수)
  - **Private Subnet**: 인터넷 접근 제한. (NAT 게이트웨이를 통해 외부로 요청 가능)
- **기능**
  - 네트워크 리소스를 그룹화하여 관리
  - 리소스별 접근 제어 가능 (예: 웹 서버와 데이터베이스를 분리)
  - 가용 영역(AZ)에 따라 배치 가능하여 고가용성 지원

<br/>

## 3. Internet Gateway

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250108205451000.png?raw=true" alt="image-20250108205451000" style="zoom:50%;" />

- **정의**: VPC 내 리소스와 인터넷 간의 통신을 가능하게 하는 컴포넌트

  - 퍼블릭 서브넷의 EC2 인스턴스 등이 인터넷과 데이터 송수신
  - 양방향 트래픽 지원 (인바운드/아웃바운드)

  - **VPC에 하나만** 연결 가능
  - 인터넷 액세스를 허용하기 위해 **라우팅 테이블에서 연결 필요**

  - 웹 서버, API 서버 등 인터넷이 필요한 리소스 배포



<br/>

## 4. Router

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250108210749932.png?raw=true" alt="image-20250108210749932" style="zoom:50%;" />

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250108211003921.png?raw=true" alt="image-20250108211003921" style="zoom:50%;" />

- **정의**: VPC 내 네트워크 트래픽의 경로를 결정하는 역할을 하는 컴포넌트

  - 라우팅 테이블을 통해 서브넷 간 트래픽 흐름 제어
  - 인터넷 게이트웨이 또는 NAT 게이트웨이와 연결하여 외부 네트워크로 라우팅
  - 네트워크 트래픽 흐름 최적화 및 안전한 통신 경로 설정

- **Routing Table**

  - 특정 트래픽(예: 0.0.0.0/0)을 인터넷 게이트웨이로 라우팅 (외부 요청이 들어올 수 있도록 설정!)
  - Private Subnet의 경우 NAT 게이트웨이를 경유하여 외부로 요청

  <br/>



## 5. CIDR 블록

- **CIDR**(Classless Inter-Domain Routing)은 **IP 주소 범위를 표현**하는 방식으로, 네트워크를 효율적으로 분할하고 관리하기 위해 사용
- AWS VPC에서는 CIDR 블록을 사용하여 VPC와 서브넷의 IP 주소 범위를 정의

### 5.1 CIDR 블록 구성

CIDR 블록 형식: `IP 주소/서브넷 마스크`

**예시:**

```
192.168.0.0/24
```

- **IP 주소**: `192.168.0.0` (네트워크의 시작 주소)
- **서브넷 마스크**: `/24` (네트워크 부분을 나타내는 비트 수)

<br/>

### 5.2 CIDR 블록의 의미

1. **IP 주소 범위 계산**

   - 서브넷 마스크(`/n`)는 IP 주소의 네트워크 부분과 호스트 부분을 구분
   - `n`은 네트워크 부분의 비트 수
   - 호스트 부분으로 할당 가능한 IP 주소의 개수를 계산 가능

   IP 주소 범위 계산 공식:

   ```
   2^(32-n) - 2
   ```

   - `32`: IPv4 주소의 총 비트 수
   - `-2`: 네트워크 주소와 브로드캐스트 주소를 제외

   

   **예시:**

   ```
   192.168.0.0/24
   ```

   - `n = 24` → 호스트 비트: `32-24 = 8`
   - 할당 가능한 IP 주소 개수: `2^8 - 2 = 254`
      (192.168.0.1 ~ 192.168.0.254)

   <br/>

   

2. **CIDR 블록 크기**

   - `/16`: 큰 네트워크, 최대 65,534개의 IP 주소.
   - `/24`: 중간 크기, 254개의 IP 주소.
   - `/28`: 작은 네트워크, 14개의 IP 주소.

<br/>

3. **AWS에서 CIDR 블록 활용**

   **VPC 생성 시**

   - VPC에 할당할 CIDR 블록 지정(예: `10.0.0.0/16`)
   - IP 주소 범위가 넉넉하면서도 서브넷으로 나누기 쉽게 설정

   **서브넷 생성 시**

   - VPC의 CIDR 블록에서 서브넷의 CIDR 블록을 정의
   - 서브넷은 VPC의 IP 범위 안에 포함되어야 함
   - 예: VPC(`10.0.0.0/16`)에서 서브넷(`10.0.1.0/24`)

   **IP 주소 관리**

   - 서비스 확장 시 CIDR 블록을 분리해 효율적으로 관리
   - 온프레미스와 네트워크 연결 시 IP 충돌 방지



<br/>

4. **CIDR 블록 설정 시 주의사항**
   - **적당한 범위 설정**
     - CIDR 블록 범위가 너무 좁으면 IP 부족 문제 발생
     - 너무 넓으면 IP 낭비 및 관리 복잡
   - **IP 주소 충돌 방지**
     - 온프레미스 네트워크 또는 다른 VPC와 연결(VPC 피어링)할 경우, CIDR 블록이 중복되지 않도록 설계
   - **확장 가능성 고려**
     - 네트워크 확장 가능성을 위해 초기 설정 시 여유 IP를 포함한 범위 지정

<br/>

## 6. 아키텍쳐

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250108214102100.png?raw=true" alt="image-20250108214102100" style="zoom:80%;" />

```
인터넷 요청
   ↓
인터넷 게이트웨이 (Internet Gateway)
   ↓
라우팅 테이블 (Route Table)
   ↓
퍼블릭 서브넷 (Public Subnet)
   ↓
서브넷 연결된 EC2 인스턴스 (혹은 다른 리소스)
```


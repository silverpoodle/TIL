# VPC (Virtual Private Cloud)

## 1. What is VPC?

<img src="https://cf-assets.www.cloudflare.com/slt3lc6tev37/4Tn2beFlmE1Xa8nt6ddphE/c6e9e80aaa3e975dcc798b8e0329949a/virtual-private-cloud.svg" alt="vpn" style="zoom:40%;" />

####  퍼블릭 클라우드 내에서 호스팅되는 안전하고 격리된 프라이빗 클라우드

- 퍼블릭 클라우드의 확장성과 프라이빗 클라우드의 보안성 결합
- 격리된 환경에서 리소스 운영 가능
- 비용 효율적이면서도 높은 보안성 확보
- 유연한 리소스 관리와 네트워크 구성 가능

<br/>

## 2.  Public Cloud vs Private Cloud

<img src="https://www.datamation.com/wp-content/uploads/2020/12/private-vs-public-cloud-computing_5fcea7aca19de.jpeg" alt="페ㅜ" style="zoom:80%;" />

### 2.1  Public Cloud

- 초기 비용이 낮고 빠른 구축 가능
- 관리 부담이 적음
- 보안은 클라우드 제공업체에 의존

<br/>

### 2.2  Private Cloud

- 높은 보안성과 데이터 통제력
- 초기 구축 비용과 유지보수 비용이 높음
- 자체 인력으로 관리 필요

<br/>

## 3. 작동 원리 (사용자 지정 방식)

### 3.1 Subnets



<img src="https://cf-assets.www.cloudflare.com/slt3lc6tev37/2pBqIHUTSlxI7EW9XZPKf3/551ab3390ab9ab86fee15c73fd245f6c/subnet-diagram.svg" alt="d" style="zoom:10%;" />

<img src="https://assets.gcore.pro/blog/what-is-a-subnet-how-subnetting-works/what-is-a-subnet-how-subnetting-works-3.png" alt="d" style="zoom:20%;" />

- L3 에서 네트워크 분할 
- IP 주소에서 네트워크 영역을 **부분적으로 분할해 나눠진 작은 부분 네트워크**
- 개인 용도로 네트워크의 일부를 분할
- 공개 인터넷을 통해 액세스할 수 없는 개인 IP 주소

<br/>

### 3.2 VLAN

<img src="https://www.fibermall.com/blog/wp-content/uploads/2023/01/VLAN-based-on-ports-e1673424252499.png" alt="d" style="zoom:60%;" />

- L2 에서 네트워크 분할
- 물리적 위치와 관계없이 하나의 네트워크에 있는 것처럼 동작하도록 구성된 가상의 네트워크 그룹

<br/>

### 3.3 VPN

<img src="https://cdn.adtidy.org/public/Adguard/Website/Images/seo/ko/how_vpn_2.jpg" alt="페ㅜ" style="zoom:50%;" />

- 암호화를 사용하여 공용 네트워크 위에 사설 네트워크를 생성

<br/>

### 3.4 NAT (Network Access Translation)

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c7/NAT_Concept-en.svg/1920px-NAT_Concept-en.svg.png" alt="nat" style="zoom:30%;" />

- IP 패킷에 적힌 소켓 주소의 포트 숫자와 소스 및 목적지의 IP 주소 등을 재기록하면서 라우터를 통해 네트워크 트래픽을 주고 받는 기술

<br/>

## 4. 장점

- **확장성**:
  퍼블릭 클라우드 공급자가 호스팅하므로 필요에 따라 손쉽게 컴퓨팅 리소스를 추가, 트래픽 증가나 워크로드 변화에도 유연하게 대응 가능!
- **성능**:
  데이터 센터(on-premise) 와 비교해 낮은 레이턴시와 높은 처리 속도를 제공, 리소스가 **동일한 네트워크 안에 배치**되어 최적화된 데이터 전송이 가능
- **보안**:
  네트워크 격리와 접근 제어를 통해 보안이 강화
  IP 주소 범위, 서브넷, 라우팅 테이블, 방화벽 규칙을 세부적으로 설정하여 데이터를 보호할 수 있음

<br/>



<br/>

참고

https://www.cloudflare.com/learning/cloud/what-is-a-virtual-private-cloud/

https://www.cloudflare.com/ko-kr/learning/network-layer/what-is-a-subnet/
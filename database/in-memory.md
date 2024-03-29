## 1️⃣ In-Memory Database란?

<img src="https://hazelcast.com/wp-content/uploads/2021/12/In-Memory-Database-Diagram_v0.1-800x453-1.png" alt="In-Memory Database diagram." style="zoom:80%;" />

출처 : https://hazelcast.com/glossary/in-memory-database/

![image-20240219222019735](https://raw.githubusercontent.com/silverpoodle/TIL/main/images/image-20240219222019735.png)

출처 : https://bommbom.tistory.com/entry/인메모리In-memory-DB-특징과-종류-비교

인메모리 데이터베이스(In-Memory Database, IMDB)는 데이터를 디스크가 아닌 `메인 메모리(RAM)`에 저장하고 관리하는 데이터베이스 시스템을 말한다.





### 인메모리 데이터베이스의 장점

1. **빠른 응답 시간과 높은 처리량 제공**

   인메모리 데이터베이스는 데이터를 메인 메모리에서 직접 처리하고,  내부 알고리즘들이 단순하여 적은 CPU 인스트럭션으로 수행되기 때문에 빠른 응답 시간과 높은 처리량을 제공한다. 이는 인메모리 데이터베이스의 가장 큰 장점이라고 할 수 있다.

2. **디스크 I/O의 부담이 없음**

   컴퓨터 시스템에서는 CPU가 연산을 수행하게 되는데, 이 CPU가 데이터를 처리하려면 해당 데이터를 디스크에서 메모리로 불러오는 과정이 필요하다. 이 과정을 디스크 I/O라고 부르는데, 인메모리 데이터베이스는 데이터를 메인 메모리에 저장하므로 이 과정이 필요없다.

3. **실시간 분석 및 처리에 적합**

   실시간 분석은 대량의 데이터를 빠르게 처리하고 분석 결과를 즉시 제공해야 한다. 이런 작업은 데이터 액세스 속도와 데이터 처리 속도가 굉장히 중요하다. 인메모리 데이터베이스는 데이터를 빠르게 액세스하고 처리할 수 있기 때문에 이런 시스템에 적합하다.

4. **성능 예측 가능**

   메인 메모리에 저장된 데이터를 접근하는 것은 성능 예측이 가능하다





### 인메모리 데이터베이스의 단점

1. **휘발성 메모리**

   인메모리 데이터베이스는 데이터를 휘발성 메모리인 RAM에 저장하기 때문에 전원이 꺼지거나 시스템에 문제가 발생하면 데이터가 손실될 수 있다.

2. **저장 용량 제한**

   RAM의 용량은 디스크에 비해 상대적으로 작다. 따라서, 대량의 데이터를 저장하기에는 제한적일 수 있다.

3. **높은 비용**

   RAM은 디스크에 비해 비싸므로, 대량의 메모리를 필요로 하는 인메모리 데이터베이스는 비용이 많이 든다.





### ACID… 괜찮을까?

인메모리 데이터베이스는 데이터를 RAM에 저장하는데, 이 RAM은 휘발성 메모리이므로 시스템이 다운되거나 전원이 꺼지는 경우 데이터가 모두 사라져버린다. 그렇게 된다면 ACID 중 **시스템에 장애가 발생하더라도 트랜잭션 작업 결과는 없어지지 않고 데이터베이스에 그대로 남아있어야 한다**는 ****`지속성(Durability)`를 보장하는데 어려움이 생길 가능성이 크다. 그러므로 인메모리 데이터베이스를 사용할 때는 해당 부분을 인지하고 보안하기 위한 방법을 사용하는 것이 좋다.

1. 스냅샷 백업
   - 정기적으로 데이터베이스의 스냅샷을 생성하여 디스크에 백업한다.
   - 스냅샷 백업을 사용하면 데이터 손실이 발생한 경우 가장 최근의 백업 상태로 복구할 수 있다.
   - 하지만 스냅샷 백업을 수행하는 동안 데이터베이스는 일시적으로 응답을 중지할 수 있으며, 큰 데이터셋의 경우 백업과 복구 시간이 길어질 수 있다.
2. 로그 백업
   - 변경된 데이터의 로그를 디스크에 기록하여 데이터 변경 내역을 추적한다.
   - 로그 백업을 사용하면 데이터베이스의 상태를 백업하는 대신, 변경된 데이터의 로그를 백업하여 데이터 손실을 최소화할 수 있다.
   - 하지만 로그 백업은 주기적으로 디스크에 기록되어야 하므로 일부 성능 손실이 발생할 수 있다.
3. 복제 (Replication)
   - 데이터베이스의 복제본을 여러 노드에 분산하여 데이터의 신뢰성과 가용성을 향상시킨다.
   - 인메모리 데이터베이스에서는 주로 복제를 통해 영속성을 보장하는 방법 중 하나이다.
   - 하지만 복제된 노드가 메모리에만 데이터를 저장하므로 모든 노드가 동시에 다운될 경우 데이터 손실이 발생할 수 있다.
4. 온디스크 로깅 (On-Disk Logging)
   - 데이터 변경 시 변경 내역을 메모리에만 저장하는 대신 디스크에도 로그를 기록하여 영속성을 보장한다.
   - 인메모리 데이터베이스에서는 주기적으로 디스크에 로그를 기록하여 데이터 손실을 방지하는 방법 중 하나이다.
   - 온디스크 로깅은 응답 시간에 약간의 성능 손실을 초래할 수 있다.





### In-Memory Database == NoSQL ?

결론부터 말하자면 **아니다!** 인메모리 데이터베이스에서 자주 언급되는게 Redis와 MemcacheDB라서 이렇게 생각하는 경우가 꽤 있는 것 같지만, 인메모리 데이터베이스가 무조건 NoSQL인 것은 아니다. MySQL의 스토리지 엔진 중 ‘MEMORY’라는 스토리지 엔진이 바로 인메모리 데이터베이스를 제공하는 엔진이다.





## 2️⃣ 디스크 기반 데이터베이스 VS 인메모리 데이터베이스

![인메모리 컴퓨팅](https://t1.daumcdn.net/cfile/tistory/036D8B4D51CA40A22E)

출처 : https://bettermesol.github.io/notes/2019/11/11/In-Memory-Computing/

인메모리 데이터베이스가 아닌 우리가 알고있는 보통의 데이터베이스는 디스크에 데이터를 저장하고 관리한다고해서 `디스크 기반 데이터베이스`라고 한다.

디스크 기반 데이터베이스는 일반적으로 자주 불러오는 데이터 일부만을 메모리에 저장하여 사용하는 구조이다. 이때 자주 불러오는 데이터 일부를 저장하는 이유는 캐시 방식을 통해 DB의 부하를 감소시키는 목적으로 사용된다. 이 밖에도 디스크 기반 데이터베이스와 인메모리 데이터베이스는 많은 차이점이 있다.

| 특징      | 디스크 기반 데이터베이스                                     | 인메모리 데이터베이스                                        |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 영속성    | 데이터를 디스크에 저장하여 시스템 장애 시에도 데이터 보존    | 데이터를 메모리에 저장하여 시스템 장애 시에 데이터 손실 가능성 있음 |
| 용량      | 대용량 데이터를 다룰 수 있음                                 | RAM 용량에 따라 제한됨                                       |
| 비용      | 대부분의 경우 비교적 저렴한 비용으로 운영 가능               | 대량의 RAM을 필요로 하기 때문에 비용이 높을 수 있음          |
| 응답 시간 | 디스크 I/O의 지연으로 인해 응답 시간이 느릴 수 있음          | 메모리에 데이터를 저장하고 처리하기 때문에 빠른 응답 시간을 제공 |
| 사용 사례 | 온라인 트랜잭션 처리(OLTP), 온라인 분석 처리(OLAP) 등 대용량 데이터를 다루는 다양한 사용 사례에 적합 | 실시간 분석, 실시간 캐싱, 실시간 트랜잭션 처리 등 실시간 데이터 처리에 적합 |





## 3️⃣ 대표적인 In-Memory Database

### Redis

Redis는 대표적인 인메모리 key-value 데이터 스토어이자 오픈 소스 데이터베이스이다. 주로 캐싱, 세션 관리, 실시간 분석, 메시지 큐 등 다양한 용도로 사용된다.

디스크에 데이터를 기록하여 메모리가 날아가도 데이터를 복구할 수 있으며, 다양한 데이터 구조를 지원한다는 장점이 있다.

### Memcached

Memcached는 분산 메모리 객체 캐시 시스템으로, 주로 웹 애플리케이션의 성능 향상을 위해 사용된다.

트래픽이 몰려도 Redis에 비해 응답 속도가 안정적이고, 내부적으로 slab 할당자를 사용하고 있어서 메모리 할당이 잦지 않다는 장점이 있다.

### Redis VS MemcacheDB

| 특징                | Redis                                                        | Memcached                                                    |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 데이터 구조         | 기본적으로 key-value지만 다양한 데이터 구조 지원 (문자열, 해시, 리스트, 세트 등) | 간단한 key-value 저장소로써 주로 문자열을 다룸               |
| 영속성              | 데이터를 디스크에 영속적으로 저장할 수 있음                  | 데이터를 영속적으로 저장하지 않음                            |
| 데이터 분산         | 분산 환경에서 안정적으로 동작함                              | 분산 환경에서도 잘 동작하지만, 데이터 손실이 발생할 가능성이 있음 |
| 복제 및 고가용성    | Master-Slave 복제 및 Sentinel을 통한 고가용성 제공           | Memcached 서버 간 데이터 동기화가 없으며, 클라이언트 측에서 처리해야 함 |
| 데이터 구성 및 용도 | 다양한 용도로 사용 가능하며, 데이터의 구조화가 가능함        | 주로 캐싱에 사용되며, 데이터의 구조화가 제한적임             |
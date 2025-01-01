# 1️⃣ Redis란?

<img src="https://upload.wikimedia.org/wikipedia/en/thumb/6/6b/Redis_Logo.svg/1200px-Redis_Logo.svg.png" alt="Redis - Wikipedia" style="zoom:40%;" />

Redis(REmote DIctionary Server)는 오픈 소스인 메모리 기반의 key-value storage이다. 주로 데이터 구조 서버로 사용되며, 주요 용도로는 캐싱, 세션 관리, 메시지 브로커 등이 있다. Redis는 디스크 기반이 아닌 메모리 기반의 데이터 저장 및 검색 시스템으로, 빠른 응답 시간을 제공하여 대규모 데이터베이스와 실시간 어플리케이션에서 주로 사용된다.

<br/>

## 1-1. Spring과 Redis

Spring 어플리케이션에서는 Spring Data Redis와 같은 라이브러리를 사용하여 프로그램 코드 내에서 Redis와의 상호작용을 처리한다. 이렇게 하면 별도의 스크립트 파일을 만들 필요 없이, 어플리케이션 코드 내에서 직접 Redis 데이터를 저장, 조회, 수정 등의 작업을 수행할 수 있다.

### **Spring Data Redis 사용 예시**

1. **의존성 추가**

   먼저, Spring Boot 프로젝트의 `build.gradle` 또는 `pom.xml` 파일에 Spring Data Redis 및 Redis 클라이언트 라이브러리 의존성을 추가한다.

   ```groovy
   dependencies {
       implementation 'org.springframework.boot:spring-boot-starter-data-redis'
   }
   ```

   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-data-redis</artifactId>
   </dependency>
   ```

2. **Redis 설정**

   `application.properties` 또는 `application.yml` 파일에 Redis 서버에 대한 설정을 추가한다.

   ```xml
   spring.redis.host=localhost
   spring.redis.port=6379
   ```

3. **Config 파일 설정**

   Spring Boot 어플리케이션에서 Redis를 사용할 수 있도록 RedisTemplate을 구성해야 한다. 이를 위해 Java Config를 사용하여 RedisConfig 클래스를 만들어야 한다.

   ```java
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import org.springframework.data.redis.connection.RedisConnectionFactory;
   import org.springframework.data.redis.core.RedisTemplate;
   import org.springframework.data.redis.serializer.StringRedisSerializer;
   
   @Configuration
   public class RedisConfig {
   
       @Bean
       public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
           RedisTemplate<String, Object> redisTemplate = new RedisTemplate<>();
           redisTemplate.setConnectionFactory(connectionFactory);
           redisTemplate.setKeySerializer(new StringRedisSerializer());
           redisTemplate.setValueSerializer(new StringRedisSerializer());
           redisTemplate.setHashKeySerializer(new StringRedisSerializer());
           redisTemplate.setHashValueSerializer(new StringRedisSerializer());
           return redisTemplate;
       }
   }
   ```

이렇게 하면 Spring Boot 어플리케이션에서 RedisTemplate을 사용해서 Redis와 상호작용할 수 있다.

<br/>

## **1-2. Redis의 특징과 장점**

1. **높은 성능**

   Redis는 주로 메모리에서 데이터를 읽고 쓰기 때문에 매우 빠른 응답 시간을 제공한다.

2. **다양한 데이터 구조 지원**

   Redis는 다양한 데이터 구조를 지원하여 String, List, Set, Hash, Sorted Set 등의 데이터를 저장하고 조작할 수 있다.

3. **영속성 지원✨**

   Redis는 메모리 기반이지만, 디스크에 데이터를 저장할 수 있는 영속성을 제공한다. 이를 통해 Redis는 서버 재시작 후에도 데이터를 보존할 수 있다.

4. **고가용성 및 확장성**

   Redis는 복제와 샤딩을 통해 고가용성과 확장성을 제공한다. 데이터의 복제는 장애 발생 시 데이터의 손실을 방지하고, 샤딩은 데이터베이스의 처리량을 확장할 수 있도록 한다.

5. **Pub/Sub 메시지 지원**

   Redis는 Pub/Sub(Publish/Subscribe) 메시지 패턴을 지원하여 다양한 애플리케이션 간의 메시지 전달을 쉽게 구현할 수 있다. 이를 통해 실시간 메시지 브로커 시스템을 구축할 수 있다.

6. **다양한 클라이언트 라이브러리**

   Redis는 다양한 프로그래밍 언어를 지원하는 클라이언트 라이브러리를 제공하여 다양한 환경에서 쉽게 사용할 수 있다.

   <br/>

## 1-3. 싱글 스레드

레디스는 사용자들이 실행한 명령어들을 이벤트 루프(event loop) 방식으로 처리한다. 즉, 클라이언트가 실행한 명령어들을 Event Queue에 적재하고 싱글 스레드로 하나씩 처리한다. 메모리를 사용하기 때문에 싱글 스레드로 데이터를 빠르게 처리할 수 있다.

[Redis는 싱글스레드인가?](https://junuuu.tistory.com/746)

[[Redis\] 레디스 알고 쓰자. - 정의, 저장방식, 아키텍처, 자료구조, 유효 기간](https://velog.io/@banggeunho/레디스Redis-알고-쓰자.-정의-저장방식-아키텍처-자료구조-유효-기간)



<br/>

<br/>

# 2️⃣ Redis의 마스터-슬레이브 구조

<img src="https://blog.kakaocdn.net/dn/cHMw5g/btqF4Vy3jKW/XHaYkSJT1ZlWLu6KkUjtrk/img.png" alt="Redis - Master / Replica(Slave) 의 구성 및 복제" style="zoom:80%;" />

Redis에서의 마스터-슬레이브(replication) 구조는 데이터의 백업과 고가용성을 보장하기 위해 설계되었다. Redis는 하나의 마스터 노드와 하나 이상의 슬레이브 노드가 있으며, 데이터는 마스터에서 슬레이브로 복제된다.

**마스터(Master)**

- 마스터는 데이터를 쓰기(write) 및 읽기(read)할 수 있는 원본 데이터 소스이다.
- 클라이언트로부터의 쓰기 요청은 먼저 마스터에게 전달되어 데이터가 쓰여지며, 이후 읽기 요청은 마스터 또는 슬레이브 중 하나에서 처리된다.
- 마스터는 쓰기 작업을 수행하고, 변경된 데이터를 슬레이브에 전달하여 복제한다.

**슬레이브(Slave)**

- 슬레이브는 마스터로부터 데이터를 복제하여 자신의 복사본을 유지한다.
- 슬레이브는 주로 읽기(read) 요청을 처리하며, 데이터의 읽기 부하를 분산시키고 응답 시간을 개선한다.
- 슬레이브는 마스터와 동일한 데이터를 가지고 있으며, 필요할 경우 마스터의 역할을 대신하여 데이터를 제공할 수 있다.

마스터는 슬레이브에게 데이터의 변경사항을 주기적으로 전달하여 동기화한다. 이를 통해 슬레이브는 항상 최신의 데이터를 유지할 수 있다.

복제는 비동기적으로 수행되며, 슬레이브가 항상 마스터의 변경 사항을 즉시 반영하는 것은 아니다. 따라서 일시적으로 마스터와 슬레이브의 데이터가 일치하지 않을 수 있다.

마스터-슬레이브 구조는 데이터의 고가용성을 보장하기 위해 사용된다. 만약 마스터가 다운될 경우, 하나 이상의 슬레이브 중 하나가 마스터로 승격되어 서비스의 지속성을 보장할 수 있다.

<aside> ✏️ **데이터 복제 과정**

1. 복제 초기화

   슬레이브 노드가 처음 마스터 노드에 연결될 때, 마스터 노드는 자신의 전체 데이터셋을 RDB 파일 형식으로 슬레이브 노드에 전송한다.

2. 동기화

   슬레이브 노드는 받은 RDB 파일을 로드하여 자신의 데이터셋을 마스터 노드와 동일하게 만든다. 이 과정이 완료되면, 슬레이브 노드는 마스터 노드에 있는 데이터의 정확한 복사본을 가지게 된다.

3. 복제

   초기 동기화 이후, 마스터 노드에서 발생하는 모든 데이터 변경(쓰기 작업)은 슬레이브 노드로 실시간으로 전송되어 복제된다. 이를 통해, 슬레이브 노드의 데이터셋을 마스터 노드와 동기화 상태로 유지한다.

</aside>

<br/>

<br/>

# 2️⃣ **Redis의 주요 기능**

## 2-1. 영속성 저장 방식

<img src="https://blog.kakaocdn.net/dn/lYw0C/btrEd4JkUke/Wdgch6BT3eKw3mXkV6jZ31/img.png" alt="Redis - Persistence 란?" style="zoom:67%;" />

### RDB(Redis DataBase)

- RDB 방식은 주기적으로 스냅샷을 찍어 디스크에 저장하는 방식이다. 지정된 시간 간격으로 Redis의 데이터 스냅샷을 생성하고 디스크에 저장한다.
- 스냅샷 파일은 Redis 서버가 재시작될 때 사용되어 데이터를 복원하므로 영구적인 데이터 보존을 보장한다.
- RDB 방식은 스냅샷 파일이 크기가 크지 않고 서버 재시작 시 빠르게 데이터를 로드할 수 있어서 주로 백업이나 복구에 사용된다.
- 하지만 스냅샷 이후 변경된 데이터는 복구할 수 없다.
- 주로 일부 데이터 손실에 영향을 받지 않는 경우, 즉 캐시로만 사용할 때 RDB 방식을 사용한다.

### AOF(Appen Only File)

- AOF 방식은 Redis의 모든 쓰기 작업을 명령의 형태로 순서대로, 쓰기 연산이 발생할 때마다 로그 파일에 기록하는 방식이다. 따라서 모든 변경 사항이 기록되어 있어서 데이터의 변경 이력을 추적할 수 있다.
- AOF 파일은 일반적으로 RDB 파일보다 크기가 크지만, 보다 신뢰성이 높은 데이터 복구를 제공한다.
- AOF 파일의 기록 형식은 텍스트 파일로 이해하기 쉽고 수정이 가능하기 때문에 유연성이 높다.
- 주로 장애 상황 직전까지의 모든 데이터가 보장되어야 할 경우 AOF 방식을 사용한다.

실제 운영 환경에서는 RDB와 AOF를 복합적으로 사용하는 것이 일반적이다. 이를 통해 스냅샷을 사용한 백업과 변경 이력 추적을 모두 활용할 수 있다.

Redis는 이 두 방식을 동시에 사용하여 **RDB 파일로 주기적으로 백업을 생성**하고, **AOF 파일로 변경 사항을 지속적으로 로깅**한다.

### 저장 방식 설정

설정 파일(redis.conf)을 수정하거나, 동적으로 CONFIG 명령어를 사용하여 저장 방식을 변경할 수 있다.

1. `redis.conf`를 수정하는 방법

   - Redis의 설정 파일(redis.conf)은 주로 **`/etc/redis/`** 디렉토리나 Redis 설치 디렉토리 내에 위치다.
   - 설정 파일을 텍스트 편집기로 열어서 해당하는 설정 항목을 수정다.
   - 저장 방식 설정은 **`save`** 디렉티브와 **`appendonly`** 디렉티브를 사용하여 구성할 수 있다.

   ```bash
   bashCopy code
   save 900 1
   appendonly yes
   ```

2. CONFIG 명령어를 사용하는 방법

   - Redis의 CONFIG 명령어를 사용하여 동적으로 설정을 변경할 수 있다.
   - CONFIG 명령어를 사용하면 Redis를 재시작하지 않고도 설정을 변경할 수 있다. 변경된 설정은 즉시 적용된다.

   ```bash
   CONFIG SET save "900 1"
   CONFIG SET appendonly yes
   ```

<br/>

## 2-2. Pub/Sub 메시지 패턴

Redis의 Pub/Sub 시스템은 Message Queue의 메시징 패턴중의 하나로, 실시간 메시지 교환에 사용된다. 메시지 발행자(publisher)와 구독자(subscriber) 간의 통신을 가능하게 한다. 발행자는 특정 채널에 메시지를 발행하고, 해당 채널을 구독하는 모든 구독자는 그 메시지를 받게 된다. 주로 실시간 알림, 채팅 애플리케이션, 작업 대기열 관리, 분산 시스템 간의 통신 등의 분야에서 활용된다.

- **발행자(Publisher)** : 메시지를 **발행**하는 클라이언트이다. 발행자는 특정 채널에 메시지를 발행할 수 있다.
- **구독자(Subscriber)** : 메시지를 **수신**하는 클라이언트이다. 구독자는 특정 채널에 구독하여 해당 채널로부터 메시지를 수신할 수 있다.
- **채널(Channel)** : 메시지를 전송하는 **통신 경로이**다. 채널을 통해 메시지를 발행하고 수신한다.
- **메시지(Message)** : 발행자가 구독자에게 전송하는 데이터이다. 데이터는 특정 채널을 통해 전달된다.

단, Redis의 pub/sub 메시지는 휘발성이고, 구독자가 연결되어 있지 않을 때 발행된 메시지는 손실된다. 다른 Message Queue 시스템들과는 다르게 수신확인을 하지 않기 때문에 전송이 보장되지 않는다. ****즉 Redis pub/sub 은 메시지를 저장, 수신확인 이 필요하지 않은 경우에 사용하면 좋은 방법이다.

[[Redis\] Redis - pub/sub 이란?](https://lucas-owner.tistory.com/60)

<br/>

## 2-3. 트랜잭션

Redis에서 트랜잭션은 여러 명령을 하나의 실행 단위로 묶어, 모든 명령이 순차적으로 실행되도록 하며, 중간에 오류가 발생하더라도 이전 상태로 롤백하지 않고, 오류가 발생한 위치 이후의 명령을 실행하지 않는 방식으로 처리한다. 레디스의 트랜잭션은 주로 `MULTI`, `EXEC`, `DISCARD`, `WATCH` 명령어를 사용하여 관리된다.

Redis의 트랜잭션은 다른 데이터베이스 시스템에서 제공하는 것처럼 엄격한 ACID 속성을 완벽히 만족시키지는 않는다.

### 명령어

- `**MULTI**`

  트랜잭션의 시작을 알린다. `MULTI`를 호출한 후부터 `EXEC`, `DISCARD`가 호출될 때까지의 모든 명령어는 즉시 실행되지 않고 큐에 순차적으로 저장된다.

- `**EXEC**`

  모든 명령어의 실행을 요청한다. `EXEC` 호출 시, `MULTI` 이후에 큐에 저장된 모든 명령어가 순차적으로 실행된다. 만약 `WATCH`로 설정된 키의 값이 `MULTI` 호출 이후 변경되었다면, 트랜잭션은 실행되지 않고 모든 명령어는 취소된다.

- `**DISCARD**`

  현재 트랜잭션을 취소하고 큐에 저장된 모든 명령어를 삭제한다.

- `**WATCH**`

  하나 이상의 키를 감시한다. `WATCH`로 지정된 키가 `MULTI` 호출 이후에 변경되면, `EXEC` 시 트랜잭션이 실행되지 않는다. 이는 트랜잭션 중에 다른 클라이언트가 해당 키를 변경하지 못하도록 보장하는 데 사용된다. 일종의 Lock이라고 볼 수 있다.

[[redis\] 트랜잭션(Transaction) - 이론편](https://sabarada.tistory.com/177)

<br/>

## 2-4. Lua 스크립팅

<aside> ✏️ **Lua Script**

루아는 간단하고 가벼운 스크립팅 언어로, 임베디드 시스템이나 게임 개발 등의 분야에서 주로 사용된다. Lua는 C 언어로 작성되어 있으며, 가독성이 높고 간결한 문법을 가지고있고, 빠르고 효율적인 실행 속도를 가지고 있다.

</aside>

Redis는 Lua 스크립트를 실행할 수 있는 기능을 제공한다. 이를 통해 사용자 정의 기능을 개발하거나 복잡한 데이터 처리를 수행할 수 있다. 또한 Lua 스크립트는 Redis 서버에서 원자적으로 실행되므로 데이터의 일관성을 보장한다.
<img src="https://blog.kakaocdn.net/dn/k3wGw/btrtHDP3QTo/CNX4jjI4MhmXpXSu0DzAI1/img.jpg" alt="img" style="zoom:33%;" />



<img src="https://static.packt-cdn.com/products/9781788391078/graphics/cdbb56bb-b04a-4bab-92b9-940af37a1cbb.png" alt="img" style="zoom:37%;" />

- **영속성 유닛**: 응용프로그램의 EntityManager 인스턴스에 의해 관리되는 모든 엔티티 클래스 집합을 정의
- **EntityManagerFactory**:  애플리케이션 전체에서 단 하나만 존재하며, 데이터베이스와의 연결을 설정하고 엔터티 매니저를 생성하는 역할 (인터페이스)
- **EntityManager**: DB table과  엔티티에 대한 CRUD 작업을 수행하기 위한 메소드들을 제공하며 엔티티의 라이프 사이클과 영속성 관리등을 담당
  각각의 트랜잭션마다 EntityManager가 생성되어 사용되며, 트랜잭션이 종료될 때 영속성 컨텍스트와 함께 소멸

```java
// 엔터티 매니저 팩토리 생성
EntityManagerFactory emf = Persistence.createEntityManagerFactory("persistenceUnitName");

// 엔터티 매니저 생성
EntityManager em = emf.createEntityManager();

// 트랜잭션 시작
em.getTransaction().begin();

// 엔터티 저장
Member member = new Member();
member.setName("YOJUNGIN");
em.persist(member);

// 트랜잭션 커밋
em.getTransaction().commit();

// 영속성 컨텍스트 종료
em.close();
emf.close();
```



#### 캐시 (cache)

**```엔티티 조회 - 1차 캐시 활용```**

![Caching in Hibernate: First Level and Second Level Cache in Hibernate -  Dinesh on Java](https://i0.wp.com/www.dineshonjava.com/wp-content/uploads/2017/04/hibernate_cache.jpg?w=728&ssl=1)

엔터티를 영속화할 때 영속성 내부에 있는 1차 캐시에 저장

```java
// 엔티티 생성 (비영속)
Member member = new Member();
member.setId("123");
member.setUsername("member1");

// 엔티티를 영속
em.persist(member);
```

1차 캐시에 저장된 상태 & 조회:

```java
1차 캐시: {"member1" -> Member(id="123", username="member1")}

// find() 메서드를 통한 엔티티 조회 -> 1차 캐시에서 "member1"을 찾아 반환
Member member = em.find(Member.class, "member1"); 
```

1차 캐시에 없는 데이터 조회:

```java
Member member2 = em.find(Member.class, "member2");
// 1차 캐시에 없어서 DB에서 "member2" 조회 후 1차 캐시에 저장 -> 영속상태!
```



이점

```java
// 1. 바로 DB에 조회하는 것이 아니라 메모리에 있는 1차 캐시에서 먼저 조회해서 불러오기 때문에 성능상 이점

// 2. 동일한 엔터티를 반복해서 조회해도 1차 캐시에서 동일한 인스턴스 반환
Member cachedMember1 = em.find(Member.class, "member1");
Member cachedMember2 = em.find(Member.class, "member1");
// cachedMember1 == cachedMember2 (동일성 보장)
```





#### 쓰기 지연 (Transactional Write-Behind)

**```영속성 컨텍스트에 변경이 발생했을 때, 바로 데이터베이스로 쿼리를 보내지 않고 SQL 쿼리를 버퍼에 모아놨다가, 영속성 컨텍스트가 flush 하는 시점에 모아둔 SQL 쿼리를 데이터베이스로 보내는 기능```**

```java
EntityManager em = emf.createEntityManager();
EntityTransaction transaction = em.getTransaction();
transaction.begin(); // 트랜잭션 시작

// 변경 감지를 통한 엔티티 수정
Member memberA = entityManager.find(User.Member, "123");
memberA.setName("NEW NAME");

// 영속성 컨텍스트에 엔티티 변경 사항 등록
entityManager.persist(memberA);
entityManager.persist(memberB);

// 여기까지 INSERT SQL을 DB에 보내지 않음.

// 트랜잭션 커밋 시 자동으로 플러시가 호출됨
entityManager.getTransaction().commit();
```



#### Flush?

**```변경된 엔티티를 데이터베이스에 동기화하는 과정```**

1. **트랜잭션 커밋 시:**

   ```java
   EntityManager entityManager = // obtain entity manager
   entityManager.getTransaction().begin();
   // 엔티티 조작
   entityManager.getTransaction().commit(); // 커밋 시 자동으로 플러시 수행
   ```

2. **명시적인 플러시 호출:**

   ```java
   // 엔티티 조작
   entityManager.flush(); // 명시적으로 플러시 호출
   entityManager.getTransaction().commit();
   ```

3. **JPQL(Java Persistence Query Language) 쿼리 실행 전:**

   - JPQL 쿼리를 실행할 때, 영속성 컨텍스트의 상태를 데이터베이스에 동기화하기 위해 플러시가 수행

   ```java
   // 엔티티 조작
   entityManager.createQuery("SELECT m FROM Member u WHERE m.age > 18").getResultList();
   // JPQL 쿼리 실행 시 자동으로 플러시 수행
   entityManager.getTransaction().commit();
   ```





#### 변경 감지 (Dirty Checking)

**```영속성 컨텍스트에서 엔티티의 상태 변경을 감지하는 방식.엔티티의 상태가 변경되면, 이를 감지하여 자동으로 데이터베이스에 해당 변경 사항을 동기화```**

1. **스냅샷**: JPA는 엔티티를 영속성 컨텍스트에 저장할 때 최초 상태를 복사하여 저장
2. 플러시 시점에 영속성 컨텍스트의 스냅샷과 현재 엔티티를 비교하여 변경된 엔티티를 찾음
3. 변경된 엔티티가 있다면, 수정 쿼리를 생성하고 쓰기 지연 SQL 저장소에 보냄
4. 쓰기 지연 저장소의 SQL을 DB에 보
5. DB 트랜잭션을 커밋

```java
// 엔티티 조회
Member member = entityManager.find(Member.class, 1L);

// 엔티티 수정 - Dirty Checking이 여기서 발생
member.setName("UpdatedName");

// 트랜잭션 커밋 시, Dirty 상태인 엔티티의 변경이 자동으로 데이터베이스에 반영됨
// 변경된 속성에 대한 SQL UPDATE 쿼리가 생성되고 실행
entityManager.getTransaction().begin();
entityManager.getTransaction().commit();
```

이점:

- **최적화된 쿼리 생성**: 변경된 필드만을 업데이트 쿼리에 포함시켜 최적화된 쿼리를 생성
- **재사용 가능한 쿼리**: 수정 쿼리가 항상 동일하므로 애플리케이션 로딩 시점에 미리 생성해두고 재사용
- **파싱 비용 감소**: DB에 동일한 쿼리를 반복해서 보내면 한 번 파싱된 쿼리이므로 파싱 비용이 감소
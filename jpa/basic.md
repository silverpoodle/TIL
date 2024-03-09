### JPA에서 Entity의 Life Cycle

<img src="https://3.bp.blogspot.com/-_7ZSlJmwcxk/XC4PU_L4BfI/AAAAAAAAFUI/0amFNqCfPJ8w-WyftTbcI2NSv-HsvM-rACLcBGAs/s1600/jpa-states.png" alt="JPA Entity Object Life Cycle" style="zoom:120%;" />

1. **New (Transient)**: 엔티티 객체가 생성되고, 아직 영속성 컨텍스트에 저장되지 않은 상태
2. **Managed (Persistent)**: 엔티티가 영속성 컨텍스트에 저장되었고, 데이터베이스에도 저장된 상태
3. **Detached**: 엔티티가 영속성 컨텍스트에서 분리되었지만, 데이터베이스에는 영향을 주지 않는 상태
4. **Removed**: 엔티티가 영속성 컨텍스트에서 제거되었고, 데이터베이스에서도 삭제된 상태

> #### 상태전이
>
> New -> Managed: **persist**() 메서드 호출로 인해 엔티티가 영속성 컨텍스트에 저장되면서 상태가 전이
> Managed -> Detached: 영속성 컨텍스트에서 분리되는 상태로, **detach**()나 **close**(**)** 메서드 호출로 발생
> Detached -> Managed: **merge**() 메서드 호출로 분리된 엔티티를 다시 영속성 컨텍스트에 연결.
> Managed -> Removed: **remove**() 메서드 호출로 엔티티가 삭제





### JPA Cascade Type

 **엔터티 간 연관관계에서 특정 작업을 한 엔터티에 적용하면 연관된 다른 엔터티에도 동일한 작업이 전파되는 기능**

> Cascade의 기본값은 없다!!! 명시적으로 지정하지 않으면 어떠한 Cascade 동작도 일어나지 않음. 
> 각각의 연관관계에 대해 개발자가 원하는 Cascade 동작을 선택적으로 명시하도록 할 것

- **CascadeType.ALL:** 모든 작업(영속성 전이, 병합, 삭제 등)을 대상 엔터티와 연관된 모든 엔터티에 전파

- **CascadeType.PERSIST:** 영속성을 전이시켜, 대상 엔터티가 영속 상태로 전환될 때 연관된 엔터티도 함께 영속 상태로 만듦

- **CascadeType.MERGE:** 병합을 전이시켜, 대상 엔터티가 병합될 때 연관된 엔터티도 함께 병합

- **CascadeType.REMOVE:** 삭제를 전이시켜, 대상 엔터티가 삭제될 때 연관된 엔터티도 함께 삭제

- **CascadeType.REFRESH:** 새로고침을 전이시켜, 대상 엔터티가 새로고침될 때 연관된 엔터티도 함께 새로고침

- **CascadeType.DETACH:** 분리를 전이시켜, 대상 엔터티가 분리될 때 연관된 엔터티도 함께 분리



> #### WHY?
>
> 1. **단일 소유자 관계:** 연관관계가 단일 소유자일 때 주로 사용. 
>    예를 들어, 부모 엔터티가 자식 엔터티를 소유하고, 부모 엔터티를 저장하거나 삭제할 때 자식 엔터티도 동일한 동작이 필요한 경우에 유용
> 2. **트랜잭션 관리:** Cascade를 사용하면 트랜잭션 내에서 관련 엔터티들이 일관성 있게 처리
>    하지만 신중하게 사용하지 않으면 의도치 않은 데이터 변경이 발생할 수 있음
> 3. **편의성 향상:** 일괄적으로 연관된 엔터티를 처리할 때 편리하게 사용할 수 있습니다. 예를 들어, 부모 엔터티를 저장할 때 자식 엔터티들도 자동으로 저장되어 코드가 단순화됩니다.

> #### BUT! 
>
> 1. **순환 참조:**  양방향 연관관계에서 상호 참조가 발생하면 무한 루프에 빠질 수 있음
> 2. **삭제 시 주의:** CascadeType.REMOVE를 사용할 때 삭제 연산이 자동으로 전파되므로 의도치 않은 삭제가 발생! 
>    특히 일대다 또는 다대다 관계에서 주의
> 3. **부모 엔터티의 상태 변화:** 의도하지 않은 부작용을 초래할 수 있음





### Proxy

![img](https://blog.kakaocdn.net/dn/MI545/btq9yNq7vC2/gmmHEpVGKMgYyeVGBFCK2K/img.png)

= Proxy는 실제 엔티티 대신에 **조회를 지연** 할 수 있는***가짜 객체*** 로, 실제 필요할 때까지 데이터베이스에서 엔티티를 가져오지 않음

> #### WHY?
>
> 연관된 테이블의 데이터를 조회하기 위해서는 `JOIN`을 사용하여 조회를 진행해야 함.
> 이때 실제로 연관된 테이블을 사용하지 않는다면 불필요한 `JOIN`을 하여 조회한 결과를 가져오기 때문에 많은 비용 발생
>
> **!이 문제를 해결하기 위해 프록시가 등장!**
>
> 연관된 객체를 처음부터 데이터베이스에서 조회하는 것이 아니라, **실제 사용하는 시점**에 데이터베이스에서 조회할 수 있고,  
> 자주 함께 사용하는 객체는 사용하는 시점이 아닌 해당 객체를 조회했을 때 바로 가져올 수 있음
>
> **target**이라는 실제 객체의 참조를 보관 -> 프록시 객체를 호출하면 실제 객체의 메소드 호출



#### 1. em.find() vs em.getReference()

- em.find(): 데이터베이스를 통해서 **실제** 엔티티 객체 조회
- em.getReference(): 데이터베이스 조회를 미루는 가짜(**프록시**) 엔티티 객체 조회

  > 프록시를 사용하면 성능상의 이점이 조금 있음
  > but 해당 엔티티가 없으면 OPTIONAL 반환하지 x
  > EntityNotFoundException 처리 해줘야함!



#### 2. 초기화

<img src="https://velog.velcdn.com/images/peanut_/post/7ba32fc0-8179-459b-b360-195be91c1e7f/image.png" alt="img" style="zoom:37%;" />

- 초기화 요청 : 처음에 MemberProxy에는 target이 비어있기 때문에 JPA가 영속성 컨택스트에 target을 요청. (== 진짜 객체 가져와!)

  - 한번 초기화 요청을 하면 target에 값이 저장되기 때문에 이후 또 초기화 요청을 할 필요 없음
  - 즉, 영속성 컨텍스트에 찾는 엔티티가 이미 있으면 em.getReference()를 호출해도 실제 엔티티가 반환

  

#### 3. 특징

1. 프록시 객체는 **처음 사용할때 한번만 초기화**
2. 프록시 객체가 **실제 엔티티로 교체되는 것이 아님**
   - 초기화가 되면 프록시는 유지되고 내부의 target이 채워지면서 프록시 객체를 통해서 실제 엔티티에 접근 가능

3. 프록시 객체는 **원본 엔티티를 상속받기 때문에 타입체크시 주의** (겉모습은 같음)

   - member1.getClass()==member2.getClass() 비교가 아니고 **instance of**를 사용해야 함

     > instanceof 연산자는 **원래 인스턴스의 형이 맞는지 여부를 체크하는 키워드**. 맞으면 true 아니면 false를 반환

4. 영속성 컨텍스트에 찾는 엔티티가 이미 있으면 em.getReference()를 호출해도 **실제 엔티티**를 반환한다.





### 로딩 전략

> 프록시 객체를 사용하게 되면 자주 함께 사용하는 것은 바로 가져올 수도 있고, 사용할 때 가져올 수 있도록 설정하는 방법이 존재
>
> ✏️즉시로딩 시 N+1 문제 주의!



#### 1.즉시 로딩

엔티티를 조회할 때 연관관계에 있는 엔티티도 함께 조회하는 방법!
`fetch` 속성을 `FetchType.EAGER`로 지정하면 `JPA` 구현체는 즉시 로딩을 최적화하기 위해 가능하면 조인 쿼리를 사용

```java
@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;

    // @ManyToOne의 경우 기본 페치 전략이 FetchType.EAGER이므로 생략 가능
    @ManyToOne
    @JoinColumn(name = "author_id")
    private Author author;

    // @OneToOne의 경우 기본 페치 전략이 FetchType.EAGER이므로 생략 가능
    @OneToOne
    @JoinColumn(name = "publisher_id")
    private Publisher publisher;
}

@Entity
public class Author {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
}

@Entity
public class Publisher {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
}

```

>  즉시 로딩 실행 `SQL`에서 `JPA`가 `내부 조인(INNER JOIN)`이 아닌 `외부 조인(LEFT OUTER JOIN)`을 사용하는 것을 확인할 수 있는데 이는 `NULL` 가능성 때문. 내부 조인이 외부 조인보다 성능이 좋기에 최적화를 위해 내부 조인을 사용하는 것이 유리한데 이때는 외래키에 `NOT NULL` 제약 조건 설정이 필요





#### 2.지연 로딩

연관된 엔티티를 실제 사용할 때 조회하는 방법!
`fetch` 속성을 `FetchType.LAZY`로 지정하면 실제 엔티티 객체 대신 앞에서 설명한 프록시 객체가 들어감

```java
@Entity
public class Author {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    // @OneToMany의 경우 기본 페치 전략이 FetchType.LAZY이므로 생략 가능
    @OneToMany(mappedBy = "author")
    private List<Book> books;
}

@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;

    // @ManyToOne의 경우 기본 페치 전략이 FetchType.EAGER이므로 FetchType.LAZY로 변경
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "author_id")
    private Author author;
}

```





### JPQL(JPA Query Language)

JPQL은 엔티티 객체를 대상으로 하는 객체 지향 쿼리 언어
SQL과 유사하지만, 데이터베이스 특정 구문이 아닌 엔티티 객체를 대상으로 쿼리를 작성할 수 있

1. **모든 엔티티 조회 (SELECT)**

```java
TypedQuery<Book> query = entityManager.createQuery("SELECT b FROM Book b", Book.class);
List<Book> books = query.getResultList();
```

2. **조건을 포함한 엔티티 조회 (WHERE)**

```java
TypedQuery<Book> query = entityManager.createQuery("SELECT b FROM Book b WHERE b.author = :author", Book.class);
query.setParameter("author", someAuthor);
List<Book> booksByAuthor = query.getResultList();
```

3. **정렬된 결과 조회 (ORDER BY)**

```java
TypedQuery<Book> query = entityManager.createQuery("SELECT b FROM Book b ORDER BY b.title DESC", Book.class);
List<Book> booksOrderedByTitleDesc = query.getResultList();
```

4. **페이징 조회 (LIMIT, OFFSET)**

```java
TypedQuery<Book> query = entityManager.createQuery("SELECT b FROM Book b", Book.class);
query.setFirstResult(0); // 시작 인덱스 (0부터 시작)
query.setMaxResults(10); // 최대 결과 수
List<Book> firstTenBooks = query.getResultList();
```

5. **집계 함수 사용 (COUNT, AVG, SUM, MAX, MIN)**

```java
TypedQuery<Long> countQuery = entityManager.createQuery("SELECT COUNT(b) FROM Book b", Long.class);
Long bookCount = countQuery.getSingleResult();
```

6. **조인 사용 (INNER JOIN)**

```java
TypedQuery<Book> query = entityManager.createQuery("SELECT b FROM Book b INNER JOIN b.author a WHERE a.name = :authorName", Book.class);
query.setParameter("authorName", "John Doe");
List<Book> booksByAuthorName = query.getResultList();
```

7. **Named Query 사용**

```java
@Entity
@NamedQuery(name = "Book.findByTitle", query = "SELECT b FROM Book b WHERE b.title = :title")
public class Book {
    // ...
}

TypedQuery<Book> query = entityManager.createNamedQuery("Book.findByTitle", Book.class);
query.setParameter("title", "The Great Gatsby");
List<Book> booksWithTitle = query.getResultList();
```

>Named Query는 JPA 엔티티 클래스에 정의된 사전에 정의된 JPQL 쿼리를 참조하는 방법
>Named Query를 사용하면 JPQL 쿼리를 엔티티 클래스에 직접 정의하고, 필요할 때마다 해당 이름을 사용하여 참조
>  ->   코드의 가독성과 재사용성을 높일 수 있습니다.

> JPQL의 경우 영속성 관련해서 주의를 해야 함

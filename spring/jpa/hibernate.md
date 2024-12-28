# Hibernate

<img src="https://suhwan.dev/images/jpa_hibernate_repository/overall_design.png" alt="JPA, Hibernate, 그리고 Spring Data JPA의 차이점" style="zoom:30%;" />

#### 자바 언어를 위한 ORM(Object Relationship Mapping) 프레임워크

=> JPA의 구현체로, JPA 인터페이스를 구현하며, 내부적으로 JDBC API를 사용

1. 관계형 데이터베이스와 객체의 패러다임 불일치 문제를 해결
2. 영속성 컨텍스트(엔티티를 영구 저정하는 환경) 제공



<br/>

## 1. ORM(Object Relationship Mapping) 이란?

![ORM Tool](https://media.geeksforgeeks.org/wp-content/uploads/20230619125144/Sender2.png)

=> 객체와 DB 를 이어주는!! 고런 역할



<br/>

## 2. 패러다임 불일치 문제

자바의 ***객체지향***과 데이터베이스의 ***관계지향***. 즉, 지향하는 바가 다르기 때문에 발생하는 문제!

```java
public class Student {
    private Long id;
    private String name;
    private List<Course> courses;
}
// Student 클래스는 Course 클래스와 관계
```



```sql
CREATE TABLE student (
    id BIGINT PRIMARY KEY,
    name VARCHAR(255)
);

CREATE TABLE course (
    id BIGINT PRIMARY KEY,
    name VARCHAR(255),
    student_id BIGINT REFERENCES student(id)
);
-- 이러한 관계를 표현하기 위해 외래 키 등을 사용
```

<br/>



## 3. Session과 Transaction

#### 3.1 Session

- Hibernate에서 데이터베이스와의 연결을 나타내는 객체로, 영속성 컨텍스트를 담당. 
- Session은 데이터베이스와의 트랜잭션을 관리하고, 영속성 컨텍스트를 통해 엔티티를 관리

#### 3.2 Transaction

- 데이터베이스 트랜잭션을 나타내며, 트랜잭션 내에서 실행되는 모든 데이터베이스 조작은 commit 또는 rollback으로
  트랜잭션의 일부로 처리 (트랜잭션을 사용하여 데이터의 일관성과 무결성을 보장)



<br/>

## 4. 영속성 컨텍스트(persistence context)

= **엔티티를 영구 저장하는 환경**

<img src="https://images.velog.io/images/minsuk/post/176d6f71-d488-43ba-8385-4d4de4880d9a/%EC%BA%A1%EC%B2%98.PNG" alt="JPA(영속성 컨텍스트)" style="zoom:80%;" />





<br/>

## 5. JDBC(Java Database Connectivity) 

**데이터베이스와 통신하기 위한 API,  *데이터베이스의 종류에 상관없이* 똑같은 코드**

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20200229213833/Architecture-of-JDBC2.jpg" alt="Introduction to JDBC (Java Database Connectivity) - GeeksforGeeks" style="zoom: 50%;" />

JDBC API는 설정한 데이터베이스에 맞는 드라이버를 사용하여 데이터베이스에 접근
즉, **JDBC는 인터페이스**이고 구현한 것은 각 데이터베이스에 맞는 드라이버들!



<br/>

## 6. JPA(Java Persistence API)

![img](https://velog.velcdn.com/images%2Fadam2%2Fpost%2Fcde32cd8-b9c0-49c4-bf99-b58c0b0c2e18%2FUntitled%203.png)

개발자가 JPA를 사용하면, JPA 내부에서 JDBC API를 사용하여 SQL을 호출하여 DB와 통신 = **간접적으로 사용** 

#### 6.1 insert

![img](https://velog.velcdn.com/images%2Fadam2%2Fpost%2F4c17dbbd-79d3-4728-9d8c-83b64a602303%2FUntitled%204.png)
MemberDAO에서 객체를 저장하고 싶을 때 개발자는 JPA에 Member 객체를 넘김

#### 6.2 find

![img](https://velog.velcdn.com/images%2Fadam2%2Fpost%2Fb579405a-fca9-4925-a418-1f2bcac68597%2FUntitled%205.png)
개발자는 member의 pk 값을 JPA에 넘긴다.

결과 반환 이후 결과(ResultSet)를 객체에 모두 매핑
쿼리를 JPA가 만들어 주기 때문에 Object와 RDB 간의 패러다임 불일치를 해결






### 1. **개념적 차이:**

- **MyBatis:** SQL 쿼리와 자바 객체 간의 매핑을 직접 수행하는 쿼리 매퍼 프레임워크
   -> **SQL을 직접 다루고**, XML 또는 어노테이션을 통해 쿼리를 정의하고 매핑
- **JPA (Java Persistence API):** 자바 객체와 데이터베이스 테이블 간의 매핑을 자동으로 처리하는 자바의 ORM 표준
  -> 객체를 데이터베이스에 저장하고 조회하기 위해 JPQL(Query Language)을 사용

<br/>

### 2. **매핑 방식:**

- **MyBatis:** 개발자가 직접 SQL을 작성하고 매핑하기 때문에 세밀한 제어가 가능하며, 복잡한 쿼리나 다이나믹한 쿼리에 적합
- **JPA:** 자동으로 SQL을 생성하고 관리해주기 때문에 생산성이 높음

<br/>

### 3. **유연성과 제어:**

- **MyBatis:** 개발자가 직접 SQL을 작성하고 매핑하기 때문에 세밀한 제어가 가능하며, 데이터베이스에 대한 직접적인 쿼리 튜닝이 필요한 경우에 유리
- **JPA:** 자동으로 SQL을 생성하고 매핑하기 때문에 개발자는 상위 수준에서 객체에 집중. 복잡한 쿼리가 필요한 경우에는 JPQL을 사용

<br/>

### 4. **성능:**

- **MyBatis:** 직접 작성한 SQL을 튜닝할 수 있어 성능에 민감한 환경에서 뛰어난 성능
- **JPA:** 성능 최적화를 위해 캐싱과 같은 기능을 제공하지만, 내부적으로 생성되는 SQL에 대한 튜닝이 제한적

<br/>

### 6. **사용 사례:**

- **MyBatis:** 복잡한 쿼리를 자주 사용하거나, 이미 존재하는 SQL 코드를 재사용
- **JPA:** 객체 지향적인 설계와 생산성이 요구되는 경우, 복잡한 SQL 작성이 필요 없는 간단한 쿼리를 다룰 때

<br/>

### 7. **선택 기준:**

- **MyBatis:** 세밀한 제어와 튜닝이 필요한 경우, 기존 SQL 코드를 재사용하고자 할 때
- **JPA:** 객체 지향적인 설계와 생산성을 중시하며, 쿼리 작성에 대한 부담이 적은 환경



<br/>

<br/>



## 🍪까까무까의 기억을 되살려봅시다!!!

#### MyBatis Configuration File (mybatis-config.xml):
```xml
<!-- mybatis-config.xml -->

<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mydatabase"/>
                <property name="username" value="root"/>
                <property name="password" value="password"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <mapper resource="com/example/mappers/MyMapper.xml"/>
    </mappers>
</configuration>
```

<br/>

#### MyBatis Mapper Interface:

```java
// MyMapper.java

package com.example.mappers;

import java.util.List;

public interface MyMapper {
    List<MyObject> getAllObjects();
    MyObject getObjectById(int id);
    void insertObject(MyObject object);
    void updateObject(MyObject object);
    void deleteObject(int id);
}
```

<br/>

#### MyBatis Mapper XML (MyMapper.xml):

```xml
<!-- MyMapper.xml -->

<mapper namespace="com.example.mappers.MyMapper">

    <select id="getAllObjects" resultType="com.example.model.MyObject">
        SELECT * FROM my_table;
    </select>

    <select id="getObjectById" parameterType="int" resultType="com.example.model.MyObject">
        SELECT * FROM my_table WHERE id = #{id};
    </select>

    <insert id="insertObject" parameterType="com.example.model.MyObject">
        INSERT INTO my_table (name, description) VALUES (#{name}, #{description});
    </insert>

    <update id="updateObject" parameterType="com.example.model.MyObject">
        UPDATE my_table SET name = #{name}, description = #{description} WHERE id = #{id};
    </update>

    <delete id="deleteObject" parameterType="int">
        DELETE FROM my_table WHERE id = #{id};
    </delete>

</mapper>
```

<br/>

<br/>

#### JPA Entity Class:
```java
// MyEntity.java

package com.example.model;

import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class MyEntity {

    @Id
    private int id;
    private String name;
    private String description;

    // Getters and setters

}
```



#### <br/>JPA Repository Interface:

```java
// MyRepository.java

package com.example.repositories;

import com.example.model.MyEntity;
import org.springframework.data.repository.CrudRepository;

public interface MyRepository extends CrudRepository<MyEntity, Integer> {
    // Custom queries can be defined here if needed
}
```

<br/>

#### JPA Service Class:

```java
// MyService.java

package com.example.services;

import com.example.model.MyEntity;
import com.example.repositories.MyRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class MyService {

    @Autowired
    private MyRepository myRepository;

    public List<MyEntity> getAllEntities() {
        return (List<MyEntity>) myRepository.findAll();
    }

    public MyEntity getEntityById(int id) {
        return myRepository.findById(id).orElse(null);
    }

    public void insertEntity(MyEntity entity) {
        myRepository.save(entity);
    }

    public void updateEntity(MyEntity entity) {
        myRepository.save(entity);
    }

    public void deleteEntity(int id) {
        myRepository.deleteById(id);
    }
}
```


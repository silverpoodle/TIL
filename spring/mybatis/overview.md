## 🕊️ MyBatis

![MyBatis| First-class persistence framework with support for custom SQL.](https://media.licdn.com/dms/image/D5612AQGFdbc7_m9_XA/article-cover_image-shrink_600_2000/0/1673530346698?e=2147483647&v=beta&t=VXFj2oeK408dKKGR1eWL0iRu3h0IH1jcCnrMLcPudc4)

<br/>

**MyBatis는 자바의 객체 지향 언어를 이용하여 관계형 데이터베이스 프로그래밍을 간편하게 할 수 있도록 도와주는 SQL Mapper(프레임워크)**

> SQL Mapper는 쿼리 실행결과를 간편하게 객체에 담고싶다에서 시작한 기술!
>
> SQL 매퍼는 쿼리의 실행결과를 미리 지정하여 두고 이를 객체로 매핑하는 기술을 말한다. (쿼리는 개발자가 직접 작성)
> 반면 ORM은 개발자가 쿼리에 관여하지 않는것이 기본! -> 객체지향 언어와 관계형 데이터베이스 사이의 차이를 해소, 개발자가 객체지향 코드만 신경쓰도록 하자!

이 프레임워크는 JDBC를 통해 데이터베이스에 접근하는 작업을 캡슐화하고, 일반 SQL 쿼리, 저장 프로시저, 그리고 고급 매핑을 지원합니다. MyBatis를 사용하면 JDBC 코드와 매개 변수의 중복 작업을 제거하고, 프로그램 내의 SQL 쿼리들을 한 구성 파일에 정리하여 코드와 SQL을 분리할 수 있는 장점이 있습니다.

<br/>

### 🕊️MyBatis의 특징

1. **쿼리 처리 강화:** 복잡한 쿼리나 다이나믹한 쿼리에 강한 성능
2. **코드와 SQL 분리:** 프로그램 코드와 SQL 쿼리를 분리함으로써 코드의 간결성과 유지보수성을 향상
3. **매핑의 유연성:** VO를 사용하지 않고, 조회 결과를 사용자 정의 DTO, MAP 등으로 매핑

<img src="https://www.researchgate.net/publication/304571194/figure/fig2/AS:378259620548610@1467195529603/MyBatis-Architecture.png" alt="MyBatis Architecture | Download Scientific Diagram" style="zoom:67%;" />

<br/>

### 🕊️MyBatis3의 구조

1. **MyBatis Configuration File:** MyBatis3의 작업 설정을 설명하는 XML 파일로, 데이터베이스 연결 대상, 매핑 파일 경로 등을 설정
2. **SqlSessionFactoryBuilder:** MyBatis3 구성 파일을 읽고 SqlSessionFactory를 생성하는 구성 요소
3. **SqlSessionFactory:** SqlSession을 생성하는 구성 요소
4. **SqlSession:** SQL 실행 및 트랜잭션 제어를 위한 API를 제공하는 구성 요소로, MyBatis3를 사용하여 데이터베이스에 액세스할 때 주요 역할
5. **Mapper Interface:** 매핑 파일에 정의된 SQL을 호출하는 인터페이스로, MyBatis3는 매퍼 인터페이스에 대한 구현 클래스를 자동으로 생성

<img src="https://blog.kakaocdn.net/dn/mvlsH/btrSAw0WxGY/pfJI0ax4TTpdkDvhW9Rpk0/img.png" alt="Spring + Mybatis 활용 원리" style="zoom:27%;" />

<br/>

### 🕊️MyBatis-Spring의 컴포넌트 구조

1. **SqlSessionFactoryBean:** SqlSessionFactory를 작성하고 Spring DI 컨테이너에 객체를 저장하는 구성 요소로, MyBatis 구성 파일이 없어도 SqlSessionFactory를 빌드할 수 있음
2. **MapperFactoryBean:** Singleton Mapper 객체를 만들고 Spring DI 컨테이너에 객체를 저장하는 구성 요소로, MyBatis3 표준 메커니즘에 의해 생성된 매퍼 객체가 스레드 안전하게 사용될 수 있도록 함
3. **SqlSessionTemplate:** SqlSession 인터페이스를 구현하는 Singleton 버전의 SqlSession 구성 요소로, MyBatis3 표준 메커니즘에 의해 생성된 SqlSession 개체를 스레드 안전하게 사용할 수 있도록 함
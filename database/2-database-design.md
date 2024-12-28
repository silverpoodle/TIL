# 데이터베이스 설계

![데이터베이스 설계](https://t1.daumcdn.net/cfile/tistory/999898375DE5F7F90D)

<br/>

### 1. 개념적 설계 (Concenptual Design)

**데이터베이스에 대한 추상적인 설계도면을 그리는 단계.** 

**`→ ERD(Entity Relationship Diagram) or ER Schema`**

<img src="https://www.dbvis.com/wp-content/uploads/2023/08/1-10-768x675.png" alt="erd" style="zoom:50%;" />

<br/>

### 2. 논리적 설계 (Logical Design)

**ER 스키마 로부터 관계형 데이터 모델과 같은 논리적 데이터베이스 구조에 맞는 스키마를 생성하는 단계** 

**`→  Table Schema`**

<img src="https://i.pinimg.com/736x/59/71/16/597116b55c7f5df4e8c28d798dca6458.jpg" alt="table" style="zoom:70%;" />



<br/>

### 3. 물리적 설계 (Physical Design)

**각 필드에 대한 데이터 타입을 결정하고 SQL create table 문을 이용해 DBMS 테이블을 생성하는 단계. 즉, 실제적인 저장 구조 결정**

* 성능(Performance) 에 대한 고려 필요

  * 시간적 측면 - 질의의 실행 시간

  * 공간적 측면 - 저장된 공간의 효율성, 접근하기 위해 필요한 물리적인 거리 등

    → Index,  외래키, View table 설정 등

<img src="https://s33046.pcdn.co/wp-content/uploads/2023/03/sql-insert-multiple-rows-using-the-insert-into-val.png" alt="pd" style="zoom:70%;" />

<br/>

### 4. 이상현상 (Anomaly)

**테이블을 설계할 때 잘못 설계하여 데이터를 삽입, 삭제, 수정할 때 논리적으로 생기는 오류**

- `삽입 이상 (Insertion Anomaly)` : 자료를 삽입할 때 특정 속성에 해당하는 값이 없어 NULL을 입력해야 하는 현상

  <img src="https://www.bestprog.net/wp-content/uploads/2020/10/09_00_06_03_01_05e-768x344.jpg" style="zoom:80%;" />

  <br/>

- `갱신 이상 (Modification Anomaly)` : 중복된 데이터 중 일부만 수정되어 데이터 모순이 일어나는 현상

  ​	<img src="https://www.bestprog.net/wp-content/uploads/2020/10/09_00_06_03_01_06e-768x287.jpg" alt="ma" style="zoom:80%;" />

  <br/>

- `삭제 이상 (Deletion Anomaly)` : 어떤 정보를 삭제하면, 의도하지 않은 다른 정보까지 삭제되어버리는 현상

  ​	<img src="https://www.bestprog.net/wp-content/uploads/2020/10/09_00_06_03_01_07e-768x260.jpg" alt="da" style="zoom:80%;" />



<br/>

### 5. DB Tuning

**DB의 구조나, DB 자체, 운영체제 등을 조정하여 DB 시스템의 전체적인 성능을 개선하는 작업**

#### 5.1 DB 설계 튜닝(모델링 관점)
DB 설계 단계에서 성능을 고려하여 설계
데이터 모델링, 인덱스 설계
데이터파일, 테이블 스페이스 설계
데이터베이스 용량 산정
튜닝 사례 - 반정규화, 분산파일배치

#### 5.2 DBMS 튜닝(환경 관점)
성능을 고려하여 메모리나 블록 크기 지정
CPU, 메모리 I/O에 관한 관점
튜닝 사례 - Buffer 크기, Cache 크기

#### 5.3 SQL 튜닝(App 관점)
SQL 작성 시 성능 고려
Join, Indexing, SQL Execution Plan
튜닝 사례 - Hash / Join





참고

https://www.bestprog.net/en/2020/10/17/databases-normalization-concept-and-necessity-of-application-modification-anomalies-examples/#google_vignette

https://www.dbvis.com/thetable/er-diagrams-vs-er-models-vs-relational-schemas/

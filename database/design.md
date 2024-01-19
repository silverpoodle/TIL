### 데이터베이스 설계

![데이터베이스 설계](https://t1.daumcdn.net/cfile/tistory/999898375DE5F7F90D)

#### 1. 개념적 설계

`데이터베이스에 대한 추상적인 설계도면을 그리는 단계. `

**`=> ERD(Entity Relationship Diagram) or ER Schema`**

#### 2. 논리적 설계

`ER 스키마 로부터 관계형 데이터 모델과 같은 논리적 데이터베이스 구조에 맞는 스키마를 생성하는 단계 `

**`=>  Table Schema`**

#### 3. 물리적 설계

`각 필드에 대한 데이터 타입을 결정하고 SQL create table 문을 이용해 DBMS 테이블을 생성하는 단계. 즉, 실제적인 저장 구조 결정`

* 성능(Performance) 에 대한 고려 필요

  * 시간적 측면 - 질의의 실행 시간

  * 공간적 측면 - 저장된 공간의 효율성, 접근하기 위해 필요한 물리적인 거리 등

    => Index,  외래키, View table 설정 등


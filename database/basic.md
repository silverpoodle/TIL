### Database 란

**`특정 조직의 업무를 수행하는 데 필요한 상호 관련된 데이터들의 집합`**



### 특징

| 실시간 접근성(Real-Time Accessibility)  | 비정형적인 질의(조회)에 대하여 실시간 처리에 의한 응답이 가능 |
| --------------------------------------- | ------------------------------------------------------------ |
| **지속적인 변화(Continuous Evloution)** | 데이터베이스의 상태는 동적. 즉 새로운 데이터의 삽입(Insert), 삭제(Delete), 갱신(Update)으로 항상 최신의 데이터를 유지 |
| **동시 공용(Concurrent Sharing)**       | 데이터베이스는 서로 다른 목적을 가진 여러 응용자들을 위한 것이므로 다수의 사용자가 동시에 같은 내용의 데이터를 이용 |
| **내용에 의한 참조(Content Reference)** | 데이터베이스에 있는 데이터를 참조할 때 데이터 레코드의 주소나 위치에 의해서가 아니라 사용자가 요구하는 데이터 내용으로 찾음 |

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          

### 데이터베이스 언어(SQL)

`데이터베이스에서 데이터를 추출하고 조작하는 데에 사용하는 데이터 처리 언어`

#### DML (Data Manipulation Language) - 데이터베이스에 들어 있는 데이터를 조회하거나 검색하기 위한 명령어

- select

  ```sql
  FROM, ON, JOIN > WHERE, GROUP BY, HAVING > SELECT > DISTINCT > ORDER BY > LIMIT   //실행 순서
  ```

- insert

- update

- delete

#### DDL (Data Definition Language) - 데이터 구조와 관련된 명령어

- create
- alter
- drop
- truncate
- rename

#### DCL (Data Control Language) - 데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어

- grant
- revoke

#### TCL (Transaction Control Language) - DML에 의해 조작된 결과를 작업단위 별로 제어하는 명령어

- commit
- rollback
- savepoint




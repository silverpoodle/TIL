### Isolation Level

`트랜잭션 격리수준(isolation level)이란 동시에 여러 트랜잭션이 처리될 때, 트랜잭션끼리 얼마나 서로 고립되어 있는지를 나타내는 것이다.
즉, 특정 트랜잭션이 다른 트랜잭션에 변경한 데이터를 볼 수 있도록 허용할지 말지를 결정하는 것`

- READ UNCOMMITTED - **어떤 트랜잭션의 변경내용이 COMMIT이나 ROLLBACK과 상관없이 다른 트랜잭션에서 보여짐**
- READ COMMITTED - **어떤 트랜잭션의 변경 내용이 COMMIT 되어야만 다른 트랜잭션에서 조회할 수 있다**
- REPEATABLE READ - **트랜잭션이 시작되기 전에 커밋된 내용에 대해서만 조회할 수 있는 격리수준**
- SERIALIZABLE -  **읽기 작업에도 `공유 잠금`을 설정하게 되고, 이러면 동시에 다른 트랜잭션에서 이 레코드를 변경하지 못함**



```
DEFAULT
- mysql: Repeatable Read
- oracle: read committed
- mongodb: read uncommitted
```




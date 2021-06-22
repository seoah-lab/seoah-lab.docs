# MySQL Transaction Isolation Levels

- MySQL의 Transaction Isolation Levels
    1. **[READ UNCOMMITTED](https://jupiny.com/2018/11/30/mysql-transaction-isolation-levels#readuncommitted)**
        - 다른 트랜젝션에서 COMMIT 되지 않은 데이터를 읽어올 수 있는 Level
        - Rollback 전의 데이터를 읽어 온다면 없는 데이터를 읽게 됨
        - Dirty Read 신뢰할 수 없는 데이터를 읽어오는 것
        - 아직 `COMMIT` 되지 않은 신뢰할 수 없는 데이터를 읽어옴(*dirty read*)
        - 한 트랜잭션에서 동일한 `SELECT` 쿼리의 결과가 다름(*non-repeatable read*)
        - 이전의 `SELECT` 쿼리의 결과에 없던 row가 생김(*phantom read*)
    2. **[READ COMMITTED](https://jupiny.com/2018/11/30/mysql-transaction-isolation-levels#readcommitted)**
        - 다른 트랜잭션에서 COMMIT 된 데이터만 읽어올 수 있는 level
        - 한 트랜잭션에서 동일한 `SELECT` 쿼리의 결과가 다름(*non-repeatable read*)
        - 이전의 `SELECT` 쿼리의 결과에 없던 row가 생김(*phantom read*)
    3. **[REPEATABLE READ](https://jupiny.com/2018/11/30/mysql-transaction-isolation-levels#repeatableread)**
        - MySQL InnoDB의 기본 isolation level

    4. **[SERIALIZABLE](https://jupiny.com/2018/11/30/mysql-transaction-isolation-levels#serializable)**
        - SERIALIZABLE 는 동시성을 상당 부분 포기하고 안정성에 큰 비중을 둔 isolation level
        - 한 트MySQL의 Transaction Isolation Levels랜잭션에서 SELECT 쿼리를 실행하면 그 트랜잭션이 COMMIT 되기 전까지 다른 트랜잭션에서는 수정, 추가, 삭제 등의 작업조차 할 수 없으므로 아래 3가지 현상 모두 발생할 일이 없다.


        ---
        참고
        https://jupiny.com/2018/11/30/mysql-transaction-isolation-levels/#readcommitted
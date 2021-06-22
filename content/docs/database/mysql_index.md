
# MySQL 인덱스

인덱스(영어: index)는 데이터베이스 분야에 있어서 테이블에 대한 동작의 속도를 높여주는 자료 구조를 일컫는다. 
Multi Coulumn Index 는 인덱스 컬럼을 연결(concat)하여 정렬한 배열입니다.



```sql
CREATE TABLE test (
    id         INT NOT NULL,
    last_name  CHAR(30) NOT NULL,
    first_name CHAR(30) NOT NULL,
    PRIMARY KEY (id),
    INDEX name (last_name,first_name)
);

```
다음과 같이 멀티 컬럼 인덱스를 생성합니다. last_name을 접두사로 활용하여 검색합니다.

```sql
SELECT * FROM test WHERE last_name='Jones';

SELECT * FROM test
  WHERE last_name='Jones' AND first_name='John';

SELECT * FROM test
  WHERE last_name='Jones'
  AND (first_name='John' OR first_name='Jon');

SELECT * FROM test
  WHERE last_name='Jones'
  AND first_name >='M' AND first_name < 'N';

```
위와 같이 접두사로 활용된 last_name 이 포함되여야 멀티 컬럼 인덱스가 사용되여 조회됩니다.

```sql
SELECT * FROM test WHERE first_name='John';

SELECT * FROM test
  WHERE last_name='Jones' OR first_name='John';
```

위와 같이 조회하면 멀티 컬럼인덱스가 사용되지 않습니다. 

```sql
SELECT * FROM tbl_name
  WHERE col1=val1 AND col2=val2;

```

col1 와 col2가 각각 컬럼 인덱스로 선언되어 있다면 옵티마이 저는 인덱스 병합 최적화를 사용하려고합니다.

---

참고 
https://dev.mysql.com/doc/refman/8.0/en/column-indexes.html
https://dev.mysql.com/doc/refman/8.0/en/multiple-column-indexes.html
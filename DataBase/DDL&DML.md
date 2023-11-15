## DDL(Data Definition Language)
### CREATE
1. CREATE DATABASE
```sql
CREATE DATABASE 데이터베이스이름
```
2. CREATE TABLE
```sql
CREATE TABLE 테이블이름
(
    필드이름1 필드타입1,
    필드이름2 필드타입2,
    ...
)
```
#### 제약 조건
데이터의 무결성을 지키기 위해 데이터를 입력받을 때 실행되는 검사 규칙이다.

CREATE로 테이블을 생성하거나 ALTER로 변경할 때 사용할 수 있다.

1. NOT NULL : 해당 필드는 NULL 값을 저장할 수 없다.
2. UNIQUE : 해당 필드는 서로 다른 값을 가져야 한다.
3. PRIMARY KEY : 해당 필드가 NOT NULL과 UNIQUE 제약 조건의 특징을 모두 가지게 된다.
4. FOREIGN KEY : 하나의 테이블을 다른 테이블에 의존하게 만든다.
5. DEFAULT : 해당 필드의 기본값을 설정한다.

>AUTO_INCREMENT 키워드를 사용하면 해당 필드의 값을 1부터 시작하여 새로운 레코드가 추가될 때마다 1씩 증가된 값을 저장한다.

### ALTER
1. ALTER DATABSE
```sql
ALTER DATABASE 데이터베이스이름 CHARACTER SET=문자집합이름

ALTER DATABASE 데이터베이스이름 COLLATE=콜레이션이름
```
>콜레이션(collation)이란?
데이터베이스에서 검색이나 정렬과 같은 작업을 할 때 사용하는 비교를 위한 규칙의 집합

2. ALTER TABLE
```sql
ALTER TABLE 테이블이름 ADD 필드이름 필드타입

ALTER TABLE 테이블이름 DROP 필드이름

ALTER TABLE 테이블이름 MODIFY COLUMN 필드이름 필드타입
```

### DROP
1. DROP DATABASE
```sql
DROP DATABASE 데이터베이스이름
```
2. DROP TABLE
```sql
DROP TABLE 테이블이름
```

---
## DML(Data Manifulation Language)

### INSERT
INTO와 VALUES를 사용하여 새로운 레코드를 추가할 수 있다.
```sql
INSERT INTO 테이블이름(필드이름1, 필드이름2, 필드이름3, ...)
VALUES (데이터값1, 데이터값2, 데이터값3, ...)

INSERT INTO 테이블이름
VALUES (데이터값1, 데이터값2, 데이터값3, ...)
```

### UPDATE
```sql
UPDATE 테이블이름
SET 필드이름1=데이터값1, 필드이름2=데이터값2, ...
WHERE 필드이름=데이터값
```
WHERE절을 생략하면 모든 레코드의 해당 필드의 값이 변경된다.

### DELETE
```sql
DELETE FROM 테이블이름
WHERE 필드이름=데이터값
```
WHERE절을 생략하면 모든 데이터가 삭제된다.

### SELECT
```sql
SELECT 필드이름
FROM 테이블이름
[WHERE 조건]
```
별(*)을 사용하여 모든 필드를 조회할 수 있다.
```sql
SELECT * FROM 테이블이름
```

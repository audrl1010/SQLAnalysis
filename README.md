# SQL(Structured Query Language)
관계명 데이터베이스를 제어하기 위한 언어이다.

# SQL문과 그 종류
SQL문은 RDBMS에 부여한 명령 종류에 따라 다음 3 가지로 나뉜다.

## DDL(Data Definition Language)
DDL(데이터 정의 언어)는 데이터를 저장하는 DB 및 Table을 생성, 삭제하기 위한 것이다.

`CREATE`: DB or Table 등을 작성한다.  
`DROP`: DB or Table 등을 삭제한다.  
`ALTER`: DB or Table 등의 구성을 변경한다.  

## DML(Data Manipulation Language)
DML(데이터 조작 언어)은 Table의 행을 검색하거나 변경하기 위한 것이다.

`SELECT`: Table 행을 검색한다.  
`INSERT`: Table에 신규 행을 등록한다.   
`DELETE`: Table에서 행을 삭제한다.  

## DCL(Data Control Language)
DCL(데이터 제어 언어)는 DB에서 처리한 변경 내용을 확정하거나 취소하기 위한 것이다. 또한 RDBMS 사용자에게 처리 권한을 부여하기도 한다.

`COMMIT`: DB 변경 내용을 확정한다.  
`ROLLBACK`: DB 변경 내용을 취소한다.   
`GRANT`: 사용자에게 처리 권한을 부여한다.  
`REVOKE`: 사용자에게 처리 권한을 제거한다.  

## 데이터베이스 생성
```sql
CREATE DATABASE <이름>
```

## 테이블 작성
```sql
CREATE TABLE <이름>  
(   
  <열 이름1> <데이터타입> <이 열의 제약>,  
  <열 이름2> <데이터타입> <이 열의 제약>,  
  <열 이름3> <데이터타입> <이 열의 제약>,  
   ...  
  <이 table의 제약1>, <이 table의 제약2>, ...  
);
```

```sql
CREATE TABLE Product 
(
  id            CHAR(4)      NOT NULL,
  name          VARCHAR(100) NOT NULL,
  classify      VARCHAR(32)  NOT NULL,
  price         INTEGER,
  register_date DATE,
  PRIMARY KEY(id)
);
```


## 데이터형 지정

### INTEGER
정수를 넣기 위한 데이터형 이다. 소수는 넣을 수 없다.

### CHAR
문자열을 넣기 위한 데이터형이다. CHAR(10), CHAR(150) 처럼 열 안에 넣을 수 있는 문자열의 최대 길이를 괄호 안에 지정할 수 있다. 
CHAR형 옆에는 **고정 문자열**이라는 데이터가 저장된다. 고정 문자열에서는 열에 넣는 문자열 길이가 최대 길이보다 작은 경우, 문자 수가 최대 길이가 될 때 까지 공백으로 채운다.

### VARCHAR
CHAR형과 비슷하지만 **가변문자열** 형식으로 열 안에 저장된다는 곳이 다르다.
가변 문자역에서는 문자 수가 최대 길이보다 작아도 공백으로 채우지 않는다.

### 제약 설정
데이터형 외에도 열에 넣을 데이터에 제약이나 조건을 추가하는 기능이다.
NULL 제약은 '데이터 없음' 상태를 표현하는 키워드다. NOT NULL 제약은 반드시 데이터가 존재해야 한다는 것을 의미한다. PRIMARY KEY(열 이름)는 주 키 제약을 의미한다. 주 키는 하나의 행을 특정 짓을 수 있는 열을 의미한다.

### 테이블 삭제
```sql
DROP TABLE <table 이름>;
```

```sql
DROP TABLE Shop;
```

## 테이블 정의 변경
열 추가하기
```sql
ALTER TABLE <table 이름> ADD COLUMN <열 정의>;
```

```sql
ALTER TABLE Shop ADD COLUMN name_eng VARCHAR(100);
```

열 삭제하기
```sql
ALTER TABLE <table 이름> DROP COLUMN <열 정의>;
```

```sql
ALTER TABLE Shop DROP COLUMN name_eng;
```
## 테이블 명 수정
```sql
RENAME TABLE <table 이름> to <새로운 table 이름>;
```

```sql
RENAME TABLE Shp to Shop;
```

# 열 출력
`SELECT`: 테이블에서 필요한 데이터를 검색해서 추출할 때 사용한다.

```sql
SELECT <열 이름>, ....
   FROM <테이블 이름>;
```
```sql
SELECT id, name, price
   FROM product;
```

## 모든 열을 출력
```sql
SELECT *
   FROM <테이블 이름>;
```
```sql
SELECT *
   FROM product;
```

## 열에 별칭 부여
AS 키워드는 사용해서 열에 별명을 부여할 수 있다.
```sql

SELECT id   AS product_id,
       name AS product_name,
       price AS product_price
  FROM product;
```

별명에 한글을 사용하려면 큰따옴표(`""`)를 사용한다.
```sql
SELECT  id     AS "상품ID",
	name   AS "상품명",
	price  AS "가격"
  FROM product;
```
## 결과에서 중복 행 제거
중복을 제외한 결과를 얻고 싶을 때는 SELECT 키워드 뒤에 `DISTINCT`라는 키워드를 붙인다.
```sql
SELECT DISTINCT <열 이름> ...
   FROM <테이블 이름>;
```

## 원하는 행 선택
선택하고 싶은 행의 조건을 WHERE에 지정한다.
```sql
SELECT <열 이름>, ....
 FROM <테이블 이름>
WHERE <조건식>;
```
```sql
SELECT price
  FROM product
 WHERE name = "구스잠바";
```

## 집약함수
`집약`은 '복수의 행을 하나의 행으로 모은다'라는 의미다.

`COUNT`: 테이블 행수를 계산한다.
```sql
SELECT COUNT(*) // * 이것을 쓸 경우 NULL값도 포함된다.
  FROM product;
  
SELECT COUNT(price) 특정 열을 지정할 경우 NULL값이 포함되지 않는다.
  FROM product;
```

`SUM`: 숫자열 데이터의 합계를 구한다.
```sql
SELECT SUM(price)
  FROM product;
```

`AVG`: 숫자열 데이터의 평균을 구한다.
```sql
SELECT AVG(price)
  FROM product;
```

`MAX`: 임의 열이 가진 데이터의 최대값을 구한다.
```sql
SELECT MAX(price)
  FROM product;
```

`MIN`: 임의 열이 가진 데이터의 최소값을 구한다.
```sql
SELECT MIN(price)
  FROM product;
```

집약 함수 사용 시 중복값 제외
`DISTINCT` 키워드를 사용하여 중복을 제거할 수 있다.

```sql
SELECT COUNT(DISTINCT classify)
  FROM product;
```

# SELECT 실행 순서
```sql
FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY
```


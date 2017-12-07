`MySQL` 기준으로 작성되었습니다.

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
`SELECT`: 테이블에서 필요한 데이터를 검색해서 추출할 때 사용한다. `SELECT`구 뒤에는 테이블에서 출력하고 싶은 열의 이름들을 기술한다. `FROM`구 뒤에는 데이터를 꺼낼 대상 테이블의 이름을 지정한다.
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

## GROUP BY
테이블을 테이블을 자르는 칼이다.
GROUP BY 구에 지정하는 열을 `집약 키` 또는 `그룹화 열`이라 한다.
```sql
SELECT <열 이름1>, <열 이름2>,  <열 이름3>, ....
  FROM <테이블 이름>
  GROUP BY <열 이름1>, <열 이름2>, <열이름3>, ....;
```
```sql
SELECT classify, COUNT(*)
  FROM product
  GROUP BY classify;
```


## SELECT 실행 순서
축약 실행 순서
```sql
FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY
```
전체 실행 순서
```sql
FROM -> ON -> JOIN -> WHERE -> GROUP BY -> CUBE | ROLLUP -> HAVING -> SELECT -> DISTINCT -> ORDER BY -> TOP
```
## 집약 함수와 GROUP BY 구를 사용할 때 자주하는 실수

### SELECT 구에 필요 없는 열을 쓴다
집약함수를 사용하는 경우 SELECT구에 쓸 수 있는 요소는 3가지이다. `상수`, `집약 함수`, `GROUP BY 구에서 지정할 열`

```sql
SELECT name, price, COUNT(*) -- name 때문에 에러가 난다. GROUP BY구에 없기 때문에 SELECT 구에 쓸 수 없다.
  FROM product
GROUP BY price; 
```
### GRUP BY 구에 별명을 쓴다
```sql
SELECT classify AS sb, COUNT(*)
  FROM product
GROUP BY sb; -- error, SELECT 구에서 부여한 별명을 GROUP BY 구에서 사용할 수 없다. (단 PostgresSQL은 허용한다.)
```

### GRUP BY 구는 결과의 순서를 정렬한다?
`GROUP BY` 구를 사용해도 표시 순서는 소트되지 않는다.

### WHERE 구에 집약함수를 사용한다.
집약함수를 사용할 수 있는 부분은 `SELECT`구와 `HAVING` 구, `ORDER BY`구 뿐이다.

## HAVING 구
`GROUP BY`를 통해 원 테이블을 그룹으로 나누어진 그룹에 대해 조건을 지정해서 선택하는 방법이다.

```sql
SELECT classify, COUNT(*)
  FROM product
GROUP BY classify
HAVING COUNT(*) = 2;
```
### HAVING 구에 쓸 수 있는 요소
`상수`, `집약 함수`, `GROUP BY` 구에 지정한 열명(=집약키)

## ORDER BY 구
검색 결과를 재정렬하려고 사용한다.

```sql
SELECT id, name, sell_price, buy_price
  FROM product
ORDER BY sell_price ASC -- DESC(내림차순);
```

## 데이터 갱신
### 데이터 등록
#### INSERT?
`INSERT`는 레코드(행)을 삽입하는 구이다.

```sql
INSERT INTO <테이블 이름> (열1, 열2, 열3, ...) VALUES (값1, 값2, 값3, ...)
-- 열 리스트와 값 리스트의 수가 일치해야 한다.
-- 열 리스트는 생략할 수 있다.(단, 테이블 생성 당시의 열 순서로 값리스트를 넣어야 한다.)
```
```sql
INSERT INTO product VALUES('0001', '세제', '주방용품', 6800, 5000, '2010-03-20');
```


#### 다른 테이블에서 데이터를 복사
```sql
INSERT INTO productCopy (id, name, classify, sell_price, buy_price, register_date)
SELECT id, name, classify, sell_price, buy_price, register_date
  FROM product;
```

### 데이터 삭제
#### DELETE ?
`DELETE`는 레코드(행)을 삭제하는 구이다.

```sql
DELETE FROM <테이블 이름>
WHERE <조건>;
```
```sql
DELETE 
  FROM product
  WHERE sell_price >= 5000;
```

### 데이터 갱신
#### UPDATE ?
`UPDATE`는 레코드(행)을 갱신하는 구이다.

```sql
UPDATE <테이블 이름>
   SET <열 이름> = <값>
   WHERE <조건>;
```
```sql
UPDATE product
   SET sell_price = sell_price * 10 
 WHERE classify = '주방용품';
```

복수 열 갱신
```sql
-- 방법 1
UPDATE product
   SET sell_price = sell_price * 20,
       buy_price = buy_price / 2
 WHERE classify = '주방용품';

-- 방법 2
UPDATE product
   SET (sell_price, buy_price) = (sell_price * 20, buy_price / 2)
 WHERE classify = '주방용품';
```

### 트랜잭션
#### 트랜잭션 ?
세트로 실행해야 할 하나 이상의 갱신(DELETE, INSERT, UPDATE) 처리 집합이다.

```sql
트랜잭션 개시문;
  DML 문1;
  DML 문2;
  DML 문3;
  ...
트랜잭션 종료문(COMMIT or ROLLBACK);
```
```sql
-- postgresSQL
BEGIN TRANSACTION
 ....
COMMIT

-- mySQL
START TRANSACTION
 ....
COMMIT
```
#### ACID 특성

### 원자성(Atomicity)
### 일관성(Consistency)
### 독립성(Isolation)
### 지속성(Durability)

### 뷰
#### 뷰와 테이블 차이
테이블과 뷰는 비슷하지만, 테이블은 `실제 데이터`를 저장하는 반면, 뷰는 테이블에서 데이터를 꺼내는 `SELECT 문`을 저장한다.

```sql
CREATE VIEW <뷰 이름> (<뷰의 열명1>, <뷰의 열명2>, ...)
AS
<SELECT 문> -- SELECT문 열과 뷰 열의 순서가 일치해야 한다.
```

```sql
CREATE VIEW productSum (classify, count_product)
AS
SELECT classify, COUNT(*)
  FROM product
  GROUP BY classify;

-- 사용
SELECT classify, count_product
  FROM productSum
```
#### 뷰의 제약사항
- 뷰 정의에 ORDER BY구는 사용할 수 없습니다.

#### 뷰 삭제
```sql
DROP VIEW <뷰 이름>;
```

```sql
DROP VIEW productSum;
```

### 서브쿼리
#### 서브쿼리와 뷰
`서브쿼리`는 뷰를 기반으로 하는 기술이다. 즉, `일회용 뷰`이다.
그러면 서브쿼리와 뷰의 차이는 ? 뷰는 데이터 자체를 저장하는 것이 아니라 데이터를 추출하는 `SELECT`문을 저장하는 방법으로, 사용자 편이성을 향상시키는 도구이고, 서브쿼리는 **뷰 정의 SELECT문**을 그대로 `FROM` 구에 삽입한 것이다.

```sql
-- 뷰
CREATE VIEW productSum (classify, count_product)
AS
SELECT classify, COUNT(*)
  FROM product
  GROUP BY classify;


SELECT classify, count_product
  FROM productSum;

-- 서브쿼리
SELECT classify, count_product
  FROM (SELECT classify, COUNT(*) AS count_product
          FROM product
          GROUP BY classify) AS productSum;

```
#### 스칼라 서브쿼리
`스칼라 서브쿼리`는 '**반드시 1행 1열만을 반환 값으로 반환한다**'라는 제약을 가진 서브쿼리이다. 즉, 10 or '부산' 처럼 하나의 값이 나온다.

```sql
-- 판매단가(sell_price)가 모든 상품의 평균 판매단가보다 높은 상품을 선택
SELECT id, name, sell_price
  FROM product
  WHERE sell_price > (SELECT AVG(sell_price)
                        FROM product);
```

`스칼라 서브쿼리`는 상수 or 열명을 쓸 수 있는 곳이라면 모두 가능하다.
```sql
SELECT id, name, sell_price, (SELECT AVG(sell_price) FROM product) AS avg_price
  FROM product;
```
* Note: 스칼라 서브쿼리 사용시 복수 행을 반환하지 않도록 해야 한다.

#### 상관 서브쿼리
바깥 쿼리 테이블의 열이 안쪽 쿼리에 나오는 경우.
* Note: 상관 서브쿼리는 성능이 좋지 않다.

```sql
-- 상품 분류별(classify)별로 평균 판매단가보다 높은 상품 질의
SELECT classify, name, sell_price
  FROM product AS S1
  WHERE sell_price > (SELECT AVG(sell_price)
                        FROM product AS S2
                        WHERE S1.classify = S2.classify);
```

## 집합연산
### 집합연산 ?
`집합`은 `레코드 집합`을 의미한다. `집합연산`은 `집합(=레코드 집합)을 더하거나 빼는  즉, 사칙연산이다. `집합연산`을 통해 두 개의 테이블에 있는 레코드를 모은 결과나 공통 레코드를 모은 결과, 한쪽에만 있는 레코드를 모은 결과 등을 취득할 수 있다.

### UNION (레코드 덧셈)
수학에서의 `합집합`처럼 레코드들을 합칠 수 있다.

```sql
SELECT id, name
  FROM product
UNION
SELECT id, name
  FROM product2
```

* Note: 중복 행은 제외한다. 만약에 중복 행을 포함하고 싶다면 `UNION ALL`을 사용한다.

### 집합 연산의 주의사항
#### 연산 대상이 되는 레코드의 열수가 같아야 한다.
```sql
-- 열 수가 불일치하기 때문에 에러
SELECT id, name
  FROM product
UNION
SELECT id, name, sell_price
  FROM product2
```
#### 덧셈 대상이 되는 레코드의 열이 같은 데이터형일 것
```sql
SELECT id, sell_price
  FROM product
UNION
SELECT id, register_date
  FROM product2
```
#### SELECT문은 어떤 것이든 지정할 수 있다. 단, ORDER BY 구는 마지막에 하나만 가능
```sql
SELECT id, name
  FROM product
  WHERE classify = '주방용품'
UNION
SELECT id, name
  FROM product2
  WHERE classify = '주방용품'
ORDER BY id;
```

### INTERSECT (테이블 간 공통 부분 선택)
두 레코드 집합의 공통 부분을 선택하는 것.

```sql
SELECT id, name
  FROM product
INTERSECT
SELECT id, name
  FROM product2
ORDER BY id;
```
### EXCEPT (레코드 뺄셈)
```sql
SELECT id, name
  FROM product
EXCEPT
SELECT id, name
  FROM product2
ORDER BY id;
```

## 결합
### 결합 ?
`결합(JOIN)`은 다른 테이블에서 열을 가지고 와서 **열을 늘리는** 처리다.

#### INNER JOIN (내부 결합)

```sql
SELECT TS.store_id, TS.store_name, TS.id, S.name, S.sell_price
  FROM storeProduct AS TS 
  INNER JOIN product AS S
  ON TS.id = S.id; -- ON은 결합 조건(두개의 테이블을 연결할 열(결합키)을 설명하는 구이다.
```
3개의 테이블을 내부 결합
```sql
SELECT TS.store_id, TS.store_name, TS.id, S.name, S.sell_price, ZS.stock_num
  FROM storeProduct AS TS
  INNER JOIN product AS S
  ON TS.id = S.id
  INNER JOIN stockProduct ZS
  ON TS.id = ZS.id
WHERE ZS.storage_id = 'S001';
```

#### OUTER JOIN (외부 결합)

```sql
SELECT TS.store_id, TS.store_name, S.id, S.name, S.sell_price
  FROM storeProduct AS TS
  RIGHT OUTER JOIN product AS S -- LEFT OUTER JOIN도 가능
  ON TS.id = S.id;
```

#### CROSS JOIN (크로스 결합)
`크로스 결합`은 두 개의 테이블에 있는 모든 레코드를 가지고 가능한 모든 조합을 만들어 내는 결합 방법이다. 한개의 테이블이 13행, 다른 테이블이 8행이라면 104행의 결과가 나온다.

`내부 결합`은 '`크로스 결합` 결과에 포함되는 부분을 가진다'라는 의미를 내포하며, `외부 결합`은 '`크로스 결합` 결과에 포함되지 않는 부분을 가진다'라는 의미가 있다.

```sql
SELECT TS.store_id, TS.store_name, TS.id, S.name
  FROM storeProduct AS TS
  CROSS JOIN product AS S;
```



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







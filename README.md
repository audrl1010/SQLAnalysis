# SQL(Structured Query Language)
관계명 데이터베이스를 제어하기 위한 언어이다.

# SQL문과 그 종류
SQL문은 RDBMS에 부여한 명령 종류에 따라 다음 3 가지로 나뉜다.

* **DDL(Data Definition Language)**
**DDL(데이터 정의 언어)**는 데이터를 저장하는 DB 및 Table을 생성, 삭제하기 위한 것이다.
`CREATE`: DB or Table 등을 작성한다.
`DROP`: DB or Table 등을 삭제한다.
`ALTER`: DB or Table 등의 구성을 변경한다.

* DML(Data Manipulation Language)

**DML(데이터 조작 언어)**은 Table의 행을 검색하거나 변경하기 위한 것이다.

`SELECT`: Table 행을 검색한다.
`INSERT`: Table에 신규 행을 등록한다.
`DELETE`: Table에서 행을 삭제한다.

* DCL(Data Control Language)

DCL(데이터 제어 언어)는 DB에서 처리한 변경 내용을 확정하거나 취소하기 위한 것이다. 또한 RDBMS 사용자에게 처리 권한을 부여하기도 한다.

`COMMIT`: DB 변경 내용을 확정한다.
`ROLLBACK`: DB 변경 내용을 취소한다.
`GRANT`: 사용자에게 처리 권한을 부여한다.
`REVOKE`: 사용자에게 처리 권한을 제거한다.

# 데이터베이스 생성
`**CREATE DATABASE** <이름>`

# 테이블 작성
`**CREATE TABLE** <이름>
( 
 <열 이름1> <데이터타입> <이 열의 제약>,
 <열 이름2> <데이터타입> <이 열의 제약>,
 <열 이름3> <데이터타입> <이 열의 제약>,
  ...
  <이 table의 제약1>, <이 table의 제약2>, ...
);
`
```sql
CREATE TABLE Product
(
	id CHAR(4) NOT NULL,
	name VARCHAR(100) NOT NULL,
	classify VARCHAR(32) NOT NULL,
	price INTEGER,
	register_date DATE,
	PRIMARY KEY(id)
);
```









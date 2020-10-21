# SQL Injection

## 목차

1. [개요](#개요)
2. [SQL이란](#SQL이란)


## 개요

SQL은 관계형 데이터베이스(RDBMS)의
데이터를 정의하고, 질의, 수정을 하기 위해
고안된 언어입니다.

DB에 의존하는 상당수의 웹 응용은 SQL를 사용해
데이터베이스와 상호작용합니다.

웹 응용에서 로그인/검색과 같이
입력 데이터를 기반으로 DBMS에 저장된 정보를
조회하는 기능을 구현하기 위해
SQL쿼리문에 입력 데이터를 추가해
DBMS에 요청합니다.

이 과정에 사용자의 입력이 SQL쿼리에 삽입돼,
SQL구문으로 해석되어,
개발자의 의도 외의 사태가 벌어질 수 있습니다.

즉 `SQL Injection`은 SQL 쿼리에
사용자의 입력 데이터가 삽입되어
사용자가 원하는 쿼리를 실행시키는
취약점입니다.

이 취약점이 발생하게 된다면,
쿼리를 실행하는 `DBMS의 계정`으로
공격이 가능하며,
DB에서 자료를 추출, 삭제, 추가 등의
행위가 가능합니다.

-----

## SQL이란
`SQL(Structured Query Language)`

이는 말 그대로 구조화된 형태를 가지는 언어이다.
올바른 구조로 요청해야만
DB가 이해하고 요청한 데이터를 수행하게 된다.

SQL은 사용 목적과 행우에 따라
다양한 구조가 존재하며
대표적으로 아래의 세가지가 존재합니다.

- [DDL](#DDL)(Data Definition language)
데이터를 정의하기 위한 언어이다.
데이터를 저장하기 위한 스키마,
데이터베이스의 **생성/수정/삭제** 등의
행위를 수행합니다.
</br>
- [DML](#DML)(Data Manipulation language)
데이터를 조작하기 위한 언어입니다.
실제 DB 내의 데이터에 대해
**조회/저장/수정/삭제**등의 행동을 수행합니다.
</br>

- DCL(Data control language)
DB의 접근 권한 등의 설정을 하기 위한 언어이다.
데이터베이스내에 사용자의 사용권한을
부여하기 위한 `GRANT`와 박탈하는 `REVOKE`
이 둘이 대표적인 DCL이다.

-----

### DDL
`DDL`(Data definition language)

대표적인 예시는 다음과 같다.

- CREATE
새로운 데이터베이스 또는 테이블을 생성합니다.

```SQL
CREATE TABLE Board(
	idx INT AUTO_INCREMENT,
	boardTitle VARCHAR(100) NOT NULL,
	boardContent VARCHAR(2000) NOT NULL,
	PRIMARY KEY(idx)
)
```
위 명령어를 통해 원하는 컬럼을 가진
`Board`테이블을 생성 할 수 있습니다.
|idx|boardTitle|boardContent|
|:--|:---------|:-----------|
| | |

----- 
- ALTER
데이터베이스 또는 테이블의 속성을 변경한다.

```SQL
ALTER TABLE Board ADD createdDate date;
```
위 명령어를 통해 테이블에 새로운 컬럼을 추가할 수 있습니다.(ex : createdDate)
|idx|boardTitle|boardContent|createdDate|
|:--|:---------|:-----------|:---|
| | | |
-----

- DROP
데이터베이스 또는 테이블을 삭제합니다.
```SQL
DROP TABLE Board;
```


### DML
`DML` (Data manipulation language)

- INSERT
테이블에 새로운 데이터를 추가합니다.
```SQL
INSERT INTO 
  Board(boardTitle, boardContent, createdDate) 
Values(
  'Hello', 
  'World !',
  Now()
);
```
이 명령어를 통해
테이블에 새로운 데이터를 추가할 수 있습니다.

|idx|boardTitle|boardContent|createdDate|
|:--|:---------|:-----------|:---|
|1|Hello|World!|20yy-MM-dd HH:mm:ss|

-----

- UPDATE
테이블에 존재하는 데이터를 수정합니다.
```SQL
UPDATE Board SET
boardContent='DreamHack!' 
Where idx=1;
```
위 명령어를 통해 테이블에 존재하는
데이터를 수정할 수 있습니다.

|idx|boardTitle|boardContent|createdDate|
|:--|:---------|:-----------|:---|
|1|Hello|__DreamHack!__|20yy-MM-dd HH:mm:ss|

-----

- 
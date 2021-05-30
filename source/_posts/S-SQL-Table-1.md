---
title: SQL >> 테이블 관리 (1)
tags:
  - SQL
categories:
  - 【STUDY - SQL】
  - SQL - 9. Table
description: '데이터 타입, 테이블 생성, CTAS (CREATE TABLE AS SELECT), 테이블 구조 변경, 테이블 이름 변경'
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
typora-root-url: ..
abbrlink: 39864
date: 2020-12-21 17:53:24
---

# 테이블 관리 (1) 

@[toc]

<br />

## **1. 데이터 타입**

테이블은 컬럼으로 이루어져 있고 컬럼은 다양한 데이터 타입을 지원한다. 이는 RDBMS가 제 역할을 하는데 있어서 매우 중요하다.

<br />

다양한 데이터 타입 지원:

* Boolean
* Character
* Numeric
* Time
* Arrays
* JSON

<br />

### >> Boolean, Character, Numeric

| 데이터 타입 | 세부 타입 | 설명                                                         |
| :----------- | :--------- | :------------------------------------------------------------ |
| Boolean     | Boolean   | 참과 거짓의 값을 저장한다.                                   |
| Character   | CHAR      | 고정형 길이의 문자열을 저장한다. <br>만약 CHAR(10)인데 'ABCDE'만 입력할 경우 실제로는 'ABCDE     '로 뒤에 공백을 붙여 저장한다. |
|             | VARCHAR   | 가변형 길이의 분자열을 저장한다. <br> 만약 VARCHAR(10) 인데 'ABCDE'만 입력할 경우 실제로 'ABCDE'만 저장한다. (뒤에 공백을 붙이지 않는다) |
|             | TEXT      | 대용량의 문자데이터를 저장한다.                              |
| Numeric     | INT       | 정수형데이터를 저장한다. 크기는 4byte이다. (범위는 -2,147,483,648 to 2,147,483,647) |
|             | SMALLINT  | 정수형 데이터를 저장한다. 크기는 2byte이다. (범위는 -32,768 to 32,767) |
|             | float     | 부동 소수점의 데이터를 저장한다. 크기는 8byte이다.           |
|             | numeric   | NUMERIC(15, 2)와 같이 전체 크기와 소수점의 자리를 지정할 수 있다. |

<br />

**[실습]**

```SQL
CREATE TABLE
DATA_TYPE_TEST_1
(
  A_BOOLEAN BOOLEAN,
  B_CHAR CHAR(10),
  C_VARCHAR VARCHAR(10),
  D_TEXT TEXT,
  E_INT INT,
  F_SMALLINT SMALLINT,
  G_FLOAT FLOAT,
  H_NUMERIC NUMERIC(15, 2)
);
```

```SQL
INSERT INTO 
DATA_TYPE_TEST_1
VALUES
(
  TRUE,        -- A_BOOLEAN
  'ABCDE',     -- B_CHAR
  'ABCDE',     -- C_VARCHAR
  'TEXT',      -- D_TEXT
  1000,        -- E_INT
  10,          -- F_SMALLINT
  10.12345,    -- G_FLOAT
  10.25        -- H_NUMERIC
);

COMMIT;
```

```SQL
SELECT * FROM DATA_TYPE_TEST_1;
```

![image-20201207164552207](/images/S-SQL-Table-1/image-20201207164552207.png)

<br />

<br />

### >> Time, Arrays, JSON

| 데이터 타입 | 세부 타입 | 설명                                                         |
| :----------- | :--------- | :------------------------------------------------------------ |
| Time        | Date      | 일자 데이터를 저장한다.                                      |
|             | TIME      | 시간 데이터를 저장한다.                                      |
|             | TIMESTAMP | 일자와 시간 데이터를 모두 저장한다.                          |
| Arrays      | array     | 배열 형식의 데이터를 저장한다. <br> 한개의 컬럼에 여러개의 데이터를 동시에 저장할 수 있으며 저장한 데이터의 순서로 조회할 수 있다. |
| JSON        | JSON      | JSON형식의 데이터를 저장한다. <br> JSON형식의 데이터를 입력해서 JSON형식대로 각 LEVEL의 데이터를 저장할 수 있다. |

<br />

**[실습]**

```SQL
CREATE TABLE DATA_TYPE_TEST_2
(
  A_DATE DATE,
  B_TIME TIME,
  C_TIMESTAMP TIMESTAMP,
  D_ARRAY TEXT[],
  E_JSON JSON
);
```

```SQL
INSERT INTO DATA_TYPE_TEST_2
VALUES
(
 CURRENT_DATE,        -- A_DATE
 LOCALTIME,           -- B_TIME
 CURRENT_TIMESTAMP,   -- C_TIMESTAMP
 ARRAY ['010-1234-1234', '010-4321-4321'],  -- D_ARRAY
 '{"customer": "John Doe", "items": {"product": "Beer", "qty": 6}}'  -- E_JSON
);

COMMIT;
```

```SQL
SELECT * FROM DATA_TYPE_TEST_2;
```

<img src="/images/S-SQL-Table-1/image-20201207171138943.png" alt="image-20201207171138943"  />

<br />

<br />

## **2. 테이블 생성**

테이블은 데이터를 담는 그릇으로써 반드시 생성해야만 데이터를 저장할 수 있다.

<br />

**\>> 테이블 생성 시 컬럼의 제약 조건**

| 제약조건명  | 설명                                                         |
| :----------- | :------------------------------------------------------------ |
| NOT NULL    | 해당 제약 조건이 있는 컬럼은 NULL이 저장될 수 없다.          |
| UNIQUE      | 해당 제약 조건이 있는 컬럼의 값은 테이블 내에서 유일해야 한다. |
| PRIMARY KEY | 해당 제약 조건이 있는 컬럼의 값은 테이블 내에서 유일해야 하고 반드시 NOT NULL이어야 한다. |
| CHECK       | 해당 제약 조건이 있는 컬럼은 지정하는 조건에 맞는 값이 들어가야 한다. |
| REFERENCES  | 해당 제약 조건이 있는 컬럼의 값은 참조하는 테이블의 특정 컬럼에 값이 존재해야 한다. |

<br />

**\>> 테이블 생성 실습**

```SQL
CREATE TABLE ACCOUNT
(
  USER_ID SERIAL PRIMARY KEY,
  USERNAME VARCHAR (50) UNIQUE NOT NULL,
  PASSWORD VARCHAR (50) NOT NULL,
  EMAIL VARCHAR (355) UNIQUE NOT NULL,
  CREATED_ON TIMESTAMP NOT NULL,
  LAST_LOGIN TIMESTAMP
);
```

```SQL
CREATE TABLE ROLE
(
  ROLE_ID SERIAL PRIMARY KEY,
  ROLE_NAME VARCHAR (255) UNIQUE NOT NULL
);
```

```SQL
CREATE TABLE ACCOUNT_ROLE
(
  USER_ID INTEGER NOT NULL,
  ROLE_ID INTEGER NOT NULL,
  GRANT_DATE TIMESTAMP WITHOUT TIME ZONE,
  PRIMARY KEY (USER_ID, ROLE_ID),   -- 기본키는 USER_ID + ROLE_ID로 한다
  CONSTRAINT ACCOUNT_ROLE_ROLE_ID_FKEY FOREIGN KEY (ROLE_ID)  -- ROLE_ID 컬럼은 ROLE 테이블의 ROLE_ID 컬럼을 참조한다
  REFERENCES ROLE (ROLE_ID) MATCH SIMPLE  -- ROLE_ID 컬럼은 ROLE 테이블의 ROLE_ID컬럼에 대한 삭제 혹은 변경 시 아무것도 하지 않는다
  ON UPDATE NO ACTION ON DELETE NO ACTION,
  CONSTRAINT ACCOUNT_ROLE_USER_ID_FKEY FOREIGN KEY (USER_ID)  -- USER_ID 컬럼은 ACCOUNT 테이블의 USER_ID 컬럼을 참조한다
  REFERENCES ACCOUNT (USER_ID) MATCH SIMPLE  -- USER_ID 컬럼은 ACCOUNT 테이블의  USER_ID 컬럼에 대한 삭제 혹은 변경 시 아무것도 하지 않는다
  ON UPDATE NO ACTION ON DELETE NO ACTION
);
```

<img src="/images/S-SQL-Table-1/image-20201208111620532.png" alt="image-20201208111620532"  />

* ACCOUNT 테이블과 ROLE 테이블은 다대다의 매칭관계이다.
* 두 테이블의 내용이 매칭될 수 있도록 ACCOUNT_ROLE 테이블을 생성하여 1대다의 관계를 만들어 준다.

<br />

```SQL
INSERT INTO ACCOUNT
VALUES
(1, '홍길동', '1234', 'honggd@naver.com', CURRENT_TIMESTAMP, NULL);

COMMIT;
```

```SQL
SELECT * FROM ACCOUNT;
```

<img src="/images/S-SQL-Table-1/image-20201208113648219.png" alt="image-20201208113648219"  />

<br />

```SQL
INSERT INTO ROLE
VALUES (1, 'DBA');

COMMIT;
```

```SQL
SELECT * FROM ROLE;
```

![image-20201208113804601](/images/S-SQL-Table-1/image-20201208113804601.png)

<br />

```SQL
INSERT INTO ACCOUNT_ROLE 
VALUES (1, 1, CURRENT_TIMESTAMP);

COMMIT;
```

```SQL
SELECT * FROM ACCOUNT_ROLE;
```

![image-20201208114018320](/images/S-SQL-Table-1/image-20201208114018320.png)

<br />

**\>> 에러**

**(1)  참조 누락성 제약 조건 위반**

* 참조키(Foreign Key)에 해당 데이터가 존재하지 않는 경우  

```SQL
INSERT INTO ACCOUNT_ROLE
VALUES (2, 1, CURRENT_TIMESTAMP);
```

<img src="/images/S-SQL-Table-1/image-20201208131508151.png" alt="image-20201208131508151" style="zoom:80%;" />

<br />

```SQL
INSERT INTO ACCOUNT_ROLE
VALUES (1, 2, CURRENT_TIMESTAMP);
```

<img src="/images/S-SQL-Table-1/image-20201208131440441.png" alt="image-20201208131440441" style="zoom:80%;" />

<br />

**(2)  고유 제약 조건 위반**

* 중복값이 없어야 하는 PRIMARY KEY에 중복이 발생한 경우

```SQL
INSERT INTO ACCOUNT_ROLE
VALUES (1, 1, CURRENT_TIMESTAMP);
```

<img src="/images/S-SQL-Table-1/image-20201208131635637.png" alt="image-20201208131635637" style="zoom:80%;" />

<br />

**(3)  참조 시 갱신/삭제 불가**

* 데이터가 참조되어 있을 때 해당 데이터를 갱신/삭제 불가한다.

```SQL
UPDATE ACCOUNT
SET USER_ID = 2
WHERE USER_ID = 1;
```

<img src="/images/S-SQL-Table-1/image-20201208133014712.png" alt="image-20201208133014712" style="zoom:80%;" />

<br />

```SQL
DELETE FROM ACCOUNT
WHERE USER_ID = 1;
```

<img src="/images/S-SQL-Table-1/image-20201208133014712.png" alt="image-20201208133014712" style="zoom:80%;" />

<br />

<br />

## **3. CTAS (CREATE TABLE AS SELECT)**

### 3-1. 개념

CTAS는 CREATE TABLE AS SELECT의 약어로써 SELECT문을 기반으로 CREATE TABLE을 할 수 있는 CREATE문이다.

<br />

### 3-2. CTAS 문법

```SQL
CREATE TABLE NEW_TABLE   -- 새로운 테이블의 이름을 설정한다
AS
SELECT문                 -- SELECT문을 작성한다
```

```SQL
CREATE TABLE NEW_TABLE (NEW_COLUMN_1, NEW_COLUMN_2)  -- 새로운 테이블명의 이름과 컬럼명을 설정한다
AS
SELECT문                 -- SELECT문을 작성한다
```

```SQL
CREATE TABLE IF NOT EXISTS NEW_TABLE   -- 기존에 테이블이 존재하지 않는 경우만 생성한다
AS
SELECT문                 -- SELECT문을 작성한다
```

<br />

### 3-3. CTAS 실습

**[MISSION]**  액션영화의 정보만으로 신규 테이블을 생성

<img src="/images/S-SQL-Table-1/image-20201208140314164.png" alt="image-20201208140314164" style="zoom:67%;" />

<br />

```SQL
SELECT * FROM CATEGORY WHERE CATEGORY_ID = 1;
```

![image-20201208140547218](/images/S-SQL-Table-1/image-20201208140547218.png)

<br />

```SQL
SELECT 
  A.FILM_ID, 
  A.TITLE,
  A.RELEASE_YEAR,
  A.LENGTH,
  A.RATING
FROM
  FILM A,
  FILM_CATEGORY B
WHERE A.FILM_ID = B.FILM_ID
AND B.CATEGORY_ID = 1;
```

<img src="/images/S-SQL-Table-1/image-20201208140813355.png" alt="image-20201208140813355" style="zoom:80%;" />

<br />

<br />

\>> 액션 영화 테이블 생성

```SQL
CREATE TABLE ACTION_FILM AS
SELECT 
  A.FILM_ID, 
  A.TITLE,
  A.RELEASE_YEAR,
  A.LENGTH,
  A.RATING
FROM
  FILM A,
  FILM_CATEGORY B
WHERE A.FILM_ID = B.FILM_ID
AND B.CATEGORY_ID = 1;
```

```SQL
SELECT * FROM ACTION_FILM;
```

<img src="/images/S-SQL-Table-1/image-20201208140813355.png" alt="image-20201208140813355" style="zoom:80%;" />

<br />

<br />

## **4. 테이블 구조 변경**

한번 만들어진 테이블이라고 하더라도 데이블 구조를 변경할 수 있다. 이 기능으로 인해 업무변화에 유연하게 대처할 수 있다. 

<br />

**\>> 테이블 구조 변경 실습**

```SQL
CREATE TABLE LINKS 
(
  LINK_ID SERIAL PRIMARY KEY,
  TITLE VARCHAR (512) NOT NULL,
  URL VARCHAR (1024) NOT NULL UNIQUE
);
```

![image-20201208143703988](/images/S-SQL-Table-1/image-20201208143703988.png)

<br />


```SQL
-- 1) ACTIVE 컬럼을 추가
ALTER TABLE LINKS ADD COLUMN ACTIVE BOOLEAN;
SELECT * FROM LINKS;
```

![image-20201208143726988](/images/S-SQL-Table-1/image-20201208143726988.png)

<br />

```SQL
-- 2) ACTIVE 컬럼을 제거
ALTER TABLE LINKS DROP COLUMN ACTIVE;
SELECT * FROM LINKS;
```

![image-20201208143703988](/images/S-SQL-Table-1/image-20201208143703988.png)

<br />

```SQL
-- 3) TITLE 컬럼을 LINK_TITLE 컬럼으로 변경
ALTER TABLE LINKS RENAME COLUMN TITLE TO LINK_TITLE;
SELECT * FROM LINKS;
```

![image-20201208144037777](/images/S-SQL-Table-1/image-20201208144037777.png)

<br />

```SQL
-- 4) TARGET 컬럼을 추가
ALTER TABLE LINKS ADD COLUMN TARGET VARCHAR(10);
SELECT * FROM LINKS;
```

![image-20201208144143373](/images/S-SQL-Table-1/image-20201208144143373.png)

<br />

```SQL
-- 5) TARGET 컬럼의 DEFAULT값을 "_blank"로 설정
ALTER TABLE LINKS ALTER COLUMN TARGET
SET DEFAULT '_blank';
SELECT * FROM LINKS;
```

![image-20201208144308010](/images/S-SQL-Table-1/image-20201208144308010.png)

<br />

* 데이터 추가 해보기

  ```SQL
  INSERT INTO LINKS (LINK_TITLE, URL)
  VALUES
  ('PostgreSQL Tutorial', 'http://www.postgresqltutorial.com/');
  ```

  ```SQL
  SELECT * FROM LINKS;
  ```

  ![image-20201208151743700](/images/S-SQL-Table-1/image-20201208151743700.png)

<br />

<br />

```SQL
-- 6) 체크 제약 조건 추가
ALTER TABLE LINKS ADD CHECK (TARGET IN ('_self', '_blank', '_parent', '_top'));
```

<br />

* TARGET 컬럼의 체크 제약 조건에 없는 'whatever' 값으로 INSERT 시도

  ```SQL
  INSERT INTO LINKS (LINK_TITLE, URL, TARGET)
  VALUES('PostgreSQL', 'http://www.postgresql.org/', 'whatever');
  ```

  <img src="/images/S-SQL-Table-1/image-20201208154416334.png" alt="image-20201208154416334" style="zoom:80%;" />

<br />

* TARGET 컬럼의 체크 제약 조건에 없는 'whatever' 값으로 INSERT 시도

  ```sql
  INSERT INTO LINKS (LINK_TITLE, URL, TARGET)
  VALUES('PostgreSQL', 'http://www.postgresql.org/', '_self');
  ```

  <img src="/images/S-SQL-Table-1/image-20201208154617221.png" alt="image-20201208154617221" style="zoom:80%;" />

<br />

<br />

## **5. 테이블 이름 변경**

한번 만들어진 테이블이라고 하더라도 테이블 이름을 변경할 수 있다. 이 기능으로 인해 업무변화에 유연하게 대처할 수 있다.

<br />

### 5-1. 테이블 이름 변경 문법

```SQL
ALTER TABLE OLD_TABLE_NAME
  RENAME TO NEW_TABLE_NAME
```

<br />

### 5-2. 테이블 이름 변경 실습

**\>> 테이블 이름 변경 실습 (1)**

**[MISSION]** VENDORS 테이블을 SUPPLIERS 테이블로 변경

```SQL
-- VENDORS 테이블 생성
CREATE TABLE VENDORS
(
  ID SERIAL PRIMARY KEY,
  NAME VARCHAR NOT NULL
);

SELECT * FROM VENDORS;
```

![image-20201208164854947](/images/S-SQL-Table-1/image-20201208164854947.png)

<br />

```SQL
-- VENDORS 테이블의 이름을 SUPPLIERS 로 변경
ALTER TABLE VENDORS RENAME TO SUPPLIERS;
```


```SQL
SELECT * FROM SUPPLIERS;
```

![image-20201208164854947](/images/S-SQL-Table-1/image-20201208164854947.png)

```SQL
SELECT * FROM VENDORS;
```

<img src="/images/S-SQL-Table-1/image-20201208171311297.png" alt="image-20201208171311297" style="zoom:80%;" />

<br />

**\>> 테이블 이름 변경 실습 (2)**

```SQL
-- SUPPLIER_GROUPS 테이블 생성
CREATE TABLE SUPPLIER_GROUPS
(
  ID SERIAL PRIMARY KEY,
  NAME VARCHAR NOT NULL
)
```

```SQL
-- SUPPLIERS 테이블에 컬럼 추가 후 FK 생성
ALTER TABLE SUPPLIERS ADD COLUMN GROUP_ID INT NOT NULL;  -- SUPPLIERS 테이블에 GROUP_ID 컬럼 추가

ALTER TABLE SUPPLIERS ADD FOREIGN KEY (GROUP_ID)  
REFERENCES SUPPLIER_GROUPS (ID);   -- SUPPLIER_GROUPS 테이블의 ID 컬럼을 참조하여 SUPPLIERS 테이블의 GROUP_ID 컬러의 값을 지정
```

![image-20201208170321928](/images/S-SQL-Table-1/image-20201208170321928.png)

<br />


```SQL
-- 아래와 같은 뷰를 생성 (뷰는 실체하는 데이터가 아닌 보기용)
CREATE VIEW SUPPLIER_DATA AS
SELECT
  S.ID,
  S.NAME,
  G.NAME "GROUP"
FROM
  SUPPLIERS S, SUPPLIER_GROUPS G
WHERE G.ID = S.GROUP_ID;
```

![image-20201208171537315](/images/S-SQL-Table-1/image-20201208171537315.png)

<br />

**1)  먼저 SUPPLIERS 테이블의 생성 과정 (DDL)를 살펴 본다**

[SUPPLIERS 테이블 --> 우클릭 --> SQL 생성 --> DDL]

<img src="/images/S-SQL-Table-1/image-20201208172445817.png" alt="image-20201208172445817" style="zoom: 67%;" />

* 지금 SUPPLIERS 테이블의 GROUP_ID 컬럼은 SUPPLIER_GROUPS 테이블의 ID 컬럼을 참조하고 있다.
* 그렇다면 여기서 부모 테이블인 SUPPLIER_GROUPS 테이블의 테이블명을 바꾸면 자식 테이블인 SUPPLIERS 테이블은 어떻게 될까?

<br />

**2) SUPPLIER_GROUPS 테이블의 이름을 "GROUPS" 로 바꾼다**

```SQL
ALTER TABLE SUPPLIER_GROUPS RENAME TO GROUPS;
```

다시 SUPPLIERS 테이블의 DDL을 확인:

<img src="/images/S-SQL-Table-1/image-20201209093846550.png" alt="image-20201209093846550" style="zoom: 67%;" />

* 이제 SUPPLIERS 테이블의 GROUP_ID 컬럼은 GROUPS 테이블의 ID 컬럼을 참조하고 있다.
* 즉 테이블명의 변경이 자동으로 반영된다.

<br />

그렇다면 우리가 만들었던 SUPPLIER_DATA 뷰는 어떻게 되었을까?

<img src="/images/S-SQL-Table-1/image-20201209093635706.png" alt="image-20201209093635706" style="zoom:80%;" />

* 테이블명이 바뀌었음에도 불구하고 자동으로 GROUPS 테이블을 참조하고 있다.
* 즉 테이블명의 변경이 자동으로 반영된다.

<br />

### 5-3. 걸론

1.  ALTER TALBE 문을 활용하여 테이블의 이름을 변경 가능.
2.  테이블 이름 변경하면, 기존의 참조무걸성 제약조건이나 뷰 등이 자동으로 반영된다.

<br />

<br />




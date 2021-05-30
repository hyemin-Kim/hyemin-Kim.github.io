---
title: SQL >> 테이블 관리 (2)
tags:
  - SQL
categories:
  - 【STUDY - SQL】
  - SQL - 9. Table
description: '컬럼 추가, 컬럼 제거, 컬럼 데이터 타입 변경, 컬럼 이름 변겅'
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
typora-root-url: ..
abbrlink: 27576
date: 2020-12-21 18:03:29
---

# 테이블 관리 (2)

@[toc]

<br />

## **1. 컬럼 추가**

### 1-1. 컬럼 추가 문법

```SQL
ALTER TABLE TABLE_NAME
 ADD COLUMN COL_NAME_1 SETTING
 ADD COLUMN COL_NAME_2 SETTING
```

<br />

### 1-2. 컬럼 추가 실습

<br />

>ORACLE (오라클):  
>
>* create, drop, alter 명령어 (DDL)를 치는 순간 자동으로 commit이 됩니다. 즉, commit 할 필요가 없습니다. 
>* 하지만 delete, update, merge, insert 등 명령어는 commit 필요 
>
> 
>
>PostgreSQL:
>
>* create, drop, alter, delete, update, merge, insert 명령어 모두 commit 을 필요합니다.

<br />


**(1) 아래와 같은 테이블을 생성한다**

```SQL
CREATE TABLE TB_CUST(
  CUST_ID SERIAL PRIMARY KEY,
  CUST_NAME VARCHAR(50) NOT NULL
);
```

![image-20201210094138951](/images/S-SQL-Table-2/image-20201210094138951.png)

<br />

<br />

**(2) 폰변호를 저장할 컬럼을 추가한다**

```SQL
ALTER TABLE TB_CUST
 ADD COLUMN PHONE_NUMBER VARCHAR(13);
```

![image-20201210094238362](/images/S-SQL-Table-2/image-20201210094238362.png)

<br />

<br />

**(3) 팩스번호 및 이메일 주소를 저장할 컬럼을 추가한다. (한 번에 2개 추가)**

```SQL
ALTER TABLE TB_CUST
 ADD COLUMN FAX_NUMBER VARCHAR(13),
 ADD COLUMN EMAIL_ADDR VARCHAR(50);
```

![image-20201210094317700](/images/S-SQL-Table-2/image-20201210094317700.png)

<br />

<br />

**>> TB_CUST의 생성 과정(DDL) 확인**

<img src="/images/S-SQL-Table-2/image-20201210095902038.png" alt="image-20201210095902038" style="zoom:80%;" />

<br />

<br />

**(4) NOT NULL 제약 컬럼 추가**

**\>> 문제**

테이블에 데이터가 있을 때는 NOT NULL 제약 컬럼을 바로 추가할 수 없다. 

추가하는 순간 해당 컬럼에 값이 없어서 NOT NULL 제약을 위반하게 되기 때문이다. 

<br />

[[ 실습 ]]

* 먼저 테이블에 데이터를 입력한다

  ```SQL
  INSERT INTO TB_CUST
  VALUES
  (1, '홍길동', '010-1234-5678', '02-123-1234', 'dbmsexpert@naver.com');
  
  COMMIT;
  ```

  <img src="/images/S-SQL-Table-2/image-20201210103454365.png" alt="image-20201210103454365"  />

  <br />

* 데이터를 입력 후 아래와 같이 NOT NULL 컬럼을 추가하면 기존에 레코드가 있기 때문에 ERROR가 발생한다.

  ```SQL
  ALTER TABLE TB_CUST
   ADD COLUMN ADDRESS VARCHAR NOT NULL;
  ```

  <img src="/images/S-SQL-Table-2/image-20201210105714436.png" alt="image-20201210105714436" style="zoom:80%;" />

<br />

**\>> 해결**

이런 경우 해결책은 우선 NULL 조건으로 컬럼을 추가한 다음, 컬럼 값을 부여하는 UPDATE 작업을 진행하고 다시 NOT NULL 제약을 추가하는 것이다.

<br />

[[ 실습 ]]

* 먼저 NULL 조건으로 컬럼을 추가한다.

  ```SQL
  ALTER TABLE TB_CUST
   ADD COLUMN ADDRESS VARCHAR NULL; 
  ```

<br />

* 그 다음 ADDRESS 컬럼을 UPDATE 한다. (컬럼 값 부여)

  ```SQL
  UPDATE TB_CUST
     SET ADDRESS = '서울시 영등포구'
   WHERE CUST_ID = 1;
   
  COMMIT;
  ```

  ![](/images/S-SQL-Table-2/image-20201210142057665.png)

    <br />

  <img src="/images/S-SQL-Table-2/image-20201210142716523.png" alt="image-20201210142716523" style="zoom:80%;" />

<br />

* 마지막으로 ALTER COLUMN으로 NOT NULL로 제약 조건을 준다.

  ```SQL
  ALTER TABLE TB_CUST
  ALTER COLUMN ADDRESS SET NOT NULL;
  ```

  <img src="/images/S-SQL-Table-2/image-20201210142834604.png" alt="image-20201210142834604" style="zoom:80%;" />

<br />

<br />

## **2. 컬럼 제거**

### 2-1. 컬럼 제거 문법

```SQL
ALTER TABLE TABLE_NAME
  DROP COLUMN COL_NAME_1,
  DROP COLUMN COL_NAME_2, 
  ... ;
```

<br />

```SQL
-- CASCADE 옵션: 해당 컬럼과 관련 있는 모든 개체들이 함께 삭제(DROP)된다.
ALTER TABLE TABLE_NAME
  DROP COLUMN COL_NAME CASCADE;
```

<br />

### 2-2. 컬럼 제거 실습

#### >> 실습 준비

```SQL
CREATE TABLE PUBLISHERS (
  PUBLISHER_ID SERIAL PRIMARY KEY,
  NAME VARCHAR NOT NULL
);
```

```SQL
CREATE TABLE CATEGORIES (
  CATEGORY_ID SERIAL PRIMARY KEY,
  NAME VARCHAR NOT NULL
);
```

```SQL
CREATE TABLE BOOKS (
  BOOK_ID SERIAL PRIMARY KEY,
  TITLE VARCHAR NOT NULL,
  ISBN VARCHAR NOT NULL,
  PUBLISHED_DATE DATE NOT NULL,
  DESCRIPTION VARCHAR,
  CATEGORY_ID INT NOT NULL,
  PUBLISHER_ID INT NOT NULL,
  FOREIGN KEY (CATEGORY_ID) REFERENCES CATEGORIES (CATEGORY_ID),
  FOREIGN KEY (PUBLISHER_ID) REFERENCES PUBLISHERS (PUBLISHER_ID)
);
```

<img src="/images/S-SQL-Table-2/image-20201217140819313.png" alt="image-20201217140819313" style="zoom:67%;" />

<br />

<br />

3개의 TABLE을 하나의 뷰로 생성한다.

```SQL
CREATE VIEW BOOK_INFO AS 
SELECT
  B.BOOK_ID,
  B.TITLE,
  B.ISBN,
  B.PUBLISHED_DATE,
  P.NAME
FROM
  BOOKS B,
  PUBLISHERS P
WHERE
  P.PUBLISHER_ID = B.PUBLISHER_ID
ORDER BY 
  B.TITLE;
```

![image-20201217140850918](/images/S-SQL-Table-2/image-20201217140850918.png)

<br />

<br />

#### >> 컬럼 제거 실습

<img src="/images/S-SQL-Table-2/image-20201217140819313.png" alt="image-20201217140819313" style="zoom:67%;" />

**관계:**

* 한 개의 카테고리가 여러 개의 책을 가진다. 한 개의 책은 반드시 카테고리를 가진다.
* 한 개의 출판사는 여러 개의 책을 출판한다. 한 개의 책은 반드시 출판사를 가진다. 

<br />

**[실습 1]  BOOKS 테이블에서 CATEGORY_ID 컬럼을 제거한다**

```SQL
SELECT * FROM BOOKS;
```

![image-20201217142424062](/images/S-SQL-Table-2/image-20201217142424062.png)

<br />


```sql
ALTER TABLE BOOKS DROP COLUMN CATEGORY_ID;

SELECT * FROM COOKS;
```

![image-20201217142727702](/images/S-SQL-Table-2/image-20201217142727702.png)

* BOOKS 테이블은 자식 테이블이므로 CATEGORY_ID 컬럼은 제거가 가능하다.
* 컬럼이 제거되면서 CATEGORY_ID의 FK (Foreign Key) 도 함께 삭제된다.

<br />

**[실습 2]  BOOKS 테이블에서 PUBLISHER_ID 컬럼을 제거한다**

```SQL
ALTER TABLE BOOKS DROP COLUMN PUBLISHER_ID;
```

<img src="/images/S-SQL-Table-2/image-20201217143419783.png" alt="image-20201217143419783" style="zoom:80%;" />

* PUBLISHER_ID 컬럼을 제거하고자 하는 경우 위와 같은 에러가 발생한다.
* 해당 컬럼은 BOOK_INFO 뷰에서 참조하고 있기 때문이다.

<br />

이런 경우에는 CASCADE 옵션을 줘서 삭제한다.

```SQL
ALTER TABLE BOOKS DROP COLUMN PUBLISHER_ID CASCADE;

SELECT * FROM BOOKS;
```

![image-20201217144023588](/images/S-SQL-Table-2/image-20201217144023588.png)

<br />

```SQL
SELECT * FROM BOOK_INFO;
```

<img src="/images/S-SQL-Table-2/image-20201217144204332.png" alt="image-20201217144204332" style="zoom:80%;" />


* 컬럼 삭제에는 성공했지만 BOOK_INFO 뷰도 같이 DROP 되었다.

<br />

**[실습 3]  동시에 N개의 컬럼을 제거한다**

```SQL
ALTER TABLE BOOKS
  DROP COLUMN ISBN,
  DROP COLUMN DESCRIPTION;
```

![image-20201217144804982](/images/S-SQL-Table-2/image-20201217144804982.png)

<br />

<br />

## **3. 컬럼 데이터 타입 변경**

### 3-1. 컬럼 데이터 타입 변경 문법 

```SQL
ALTER TABLE TABLE_NAME
  ALTER COLUMN COL_NAME_1 TYPE NEW_TYPE,
  ALTER COLUMN COL_NAME_2 TYPE NEW_TYPE,
  ... ;
```

<br />

### 3-2. 컬럼 데이터 타입 변경 실습

#### >> 실습 준비

```SQL
CREATE TABLE ASSETS (
  ID SERIAL PRIMARY KEY,
  NAME TEXT NOT NULL,
  ASSET_NO VARCHAR(10) NOT NULL,
  DESCRIPTION TEXT,
  LOCATION TEXT,
  DATE_ACQUIRED DATE NOT NULL
);
```

```SQL
INSERT INTO ASSETS (
  NAME,
  ASSET_NO,
  LOCATION,
  DATE_ACQUIRED
)
VALUES
('Server', '10001', 'Server room', '2017-01-01'),
('UPS', '10002', 'Server room', '2017-01-02');

COMMIT;
```

```SQL
SELECT * FROM ASSETS;
```

![image-20201218185044584](/images/S-SQL-Table-2/image-20201218185044584.png)

<br />

#### >> 컬럼 데이터 타입 변경 실습

![image-20201218185255265](/images/S-SQL-Table-2/image-20201218185255265.png)

**[MISSION 1]**  NAME, DESCRIPTION, LOCATION 컬럼의 데이터 타입을 TEXT에서 VARCHAR로 바꾸기

```SQL
-- 1개 컬럼의 데이터 타입 변경
ALTER TABLE ASSETS ALTER COLUMN NAME TYPE VARCHAR(50);
```

```SQL
-- 한번에 N개 컬럼의 데이터 타입 변경
ALTER TABLE ASSETS 
  ALTER COLUMN DESCRIPTION TYPE VARCHAR(100),
  ALTER COLUMN LOCATION TYPE VARCHAR(500);
```

<img src="/images/S-SQL-Table-2/image-20201218190150074.png" alt="image-20201218190150074" style="zoom:80%;" />

<br />

<br />

**[MISSION 2]**  ASSET_NO 컬럼의 데이터 타입을 VARCHAR 에서 INT로 바꾸기

* 그냥 ```TYPE INT``` 로 바꾸면 ERROR 가 발생한다

  ```SQL
  ALTER TABLE ASSETS ALTER COLUMN ASSET_NO TYPE INT;
  ```

  <img src="/images/S-SQL-Table-2/image-20201218190725819.png" alt="image-20201218190725819" style="zoom:80%;" />

  <br />

* **[주의]** ```USING col_name::integer``` 구문을 추가해야 함

  ```sql
  ALTER TABLE ASSETS
    ALTER COLUMN ASSET_NO TYPE INT USING ASSET_NO::INTEGER;
  ```

  <img src="/images/S-SQL-Table-2/image-20201218190942598.png" alt="image-20201218190942598" style="zoom:80%;" />

<br />

<br />

## **4. 컬럼 이름 변경**

### 4-1. 컬럼 이름 변경 문법

```SQL
ALTER TABLE TABLE_NAME
  RENAME COLUMN COL_NAME_OLD TO COL_NAME_NEW;
```

<br />

### 4-2. 컬럼 이름 변경 실습

#### >>  실습 준비

```SQL
DROP TABLE CUSTOMER_GROUPS;
DROP TABLE CUSTOMERS;
DROP VIEW CUSTOMER_DATA;
```

```SQL
CREATE TABLE CUSTOMER_GROUPS (
  ID SERIAL PRIMARY KEY,
  NAME VARCHAR NOT NULL
);

CREATE TABLE CUSTOMERS (
  ID SERIAL PRIMARY KEY,
  NAME VARCHAR NOT NULL,
  PHONE VARCHAR NOT NULL,
  EMAIL VARCHAR,
  GROUP_ID INT,
  FOREIGN KEY (GROUP_ID) REFERENCES CUSTOMER_GROUPS (ID)
);
```

```SQL
SELECT * FROM CUSTOMER_GROUPS;
```

![image-20201218220746648](/images/S-SQL-Table-2/image-20201218220746648.png)

```SQL
SELECT * FROM CUSTOMERS;
```

![image-20201218220814142](/images/S-SQL-Table-2/image-20201218220814142.png)

<br />


```SQL
CREATE VIEW CUSTOMER_DATA
AS SELECT
  C.ID,
  C.NAME,
  G.NAME CUSTOMER_GROUP
FROM 
  CUSTOMERS C,
  CUSTOMER_GROUPS G
WHERE C.GROUP_ID = G.ID;
```

```SQL
SELECT * FROM CUSTOMER_DATA;
```

![image-20201218220315994](/images/S-SQL-Table-2/image-20201218220315994.png)

<br />

#### >>  컬럼 이름 변경 실습

**[MISSION 1]**  CUSTOMERS 테이블 EMIAL 컬럼의 이름을 바꾸기:  EMAIL --> CONTACT_EMAIL

```SQL
ALTER TABLE CUSTOMERS
  RENAME COLUMN EMIAL TO CONTACT_EMAIL;
```

```SQL
SELECT * FROM CUSTOMERS;
```

![image-20201218221154310](/images/S-SQL-Table-2/image-20201218221154310.png)

<br />

**[MISSION 2]**  CUSTOMER_GROUPS 테이블의 NAME 컬럼의 이름을 바꾸기:  NAME --> GROUP_NAME

```SQL
ALTER TABLE CUSTOMER_GROUPS
  RENAME COLUMN NAME TO GROUP_NAME;
```

```SQL
SELECT * FROM CUSTOMER_GROUPS;
```

![image-20201218221509265](/images/S-SQL-Table-2/image-20201218221509265.png)

<br />

뷰 CUSTOMER_DATA 에서 참조중인 CUSTOMER_GROUP 테이블의 NAME 컬럼의 이름도 바뀌었는지 살펴본다

```SQL
SELECT * FROM CUSTOMER_DATA;
```

![image-20201218221834951](/images/S-SQL-Table-2/image-20201218221834951.png)

* 컬럼명이 바뀐 것이 뷰에 자동으로 적용된 것을 확인할 수 있다.

<br />

<br />
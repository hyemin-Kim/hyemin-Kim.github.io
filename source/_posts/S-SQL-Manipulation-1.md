---
title: SQL >> 데이터 조작 (1)
tags:
  - SQL
  - Manipulation
categories:
  - 【STUDY - SQL】
  - SQL - 8. Manipulation
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: 'INSERT 문, UPDATE 문, UPDATE JOIN 문'
typora-root-url: ..
abbrlink: 44086
date: 2020-12-07 13:45:49
---

# 데이터 조작 (1) 

@[toc]

<br />

## **1. INSERT 문**

### 1-1. 개념

INSERT는 테이블이 만들어지면 데이블 안에 데이터를 추가하는 명령어이다.

<br />

### 1-2. INSERT 문법

**\>> 1) 테이블의 컬럼 순서대로 입력**

```SQL
INSERT INTO 
  TABLE_NAME      -- INSERT할 테이블 지정
VALUES
(
  VALUE1,         -- 각 컬럼 값을 입력한다
  VALUE2,
  VALUE3,
  ...
);

COMMIT;
```

<br />

**\>> 2) 테이블 컬럼 지정**  (더 많이 쓰임. 컬럼 명을 명시해주기 때문에 유지보수에 용이함)

```SQL
INSERT INTO
   TABLE_NAME
   (
    COLUMN_1,
    COLUMN_2
   )
VALUES
(
  VALUE1,
  VALUE2
);

COMMIT;
```

<br />

### 1-3. INSERT 문 실습

#### \>> 실습 준비

```SQL
-- LINK라는 테이블을 생성함
CREATE TABLE LINK (
  ID SERIAL PRIMARY KEY,
  URL VARCHAR (255) NOT NULL,
  NAME VARCHAR (255) NOT NULL,
  DESCRIPTION VARCHAR (255),
  REL VARCHAR (50)
);
```

<br />

#### \>> INSERT 문 실습

**(1) 1개 ROW 입력**

```SQL
INSERT INTO 
   LINK (URL, NAME)
VALUES
  ('http://naver.com', 'Naver');
COMMIT;
```

```SQL
SELECT * FROM LINK;
```

<img src="/images/S-SQL-Manipulation-1/image-20201203111802507.png" alt="image-20201203111802507"  />

<br />

```SQL
-- 내용 안에 작은 따움표를 추가하고 싶으면 작은 따움표 두개(''##'')를 더 추가해주면 됨. 
INSERT INTO 
   LINK (URL, NAME)
VALUES
  ('''http://naver.com''', 'Naver');
  
COMMIT;
```

```SQL
SELECT * FROM FILM;
```

![image-20201203113353940](/images/S-SQL-Manipulation-1/image-20201203113353940.png)

<br />

<br />

**(2) 동시에 N개 ROW 입력**

```SQL
INSERT INTO 
   LINK (URL, NAME)
VALUES
 ('http://www.google.com', 'Google'),
 ('http://www.bing.com', 'Bing'),
 ('http://www.baidu.com', 'BaiDu');

COMMIT;
```

<img src="/images/S-SQL-Manipulation-1/image-20201203135135326.png" alt="image-20201203135135326" style="zoom:80%;" />

<br />

<br />

**(3) 테이블 프레임에 테이블을 입력**

\>  LINK 테이블의 스키마(껍데기)만 가져와서 LINK_TMP 테이블을 생성한다

```SQL
CREATE TABLE LINK_TMP AS
SELECT * FROM LINK
WHERE 0 = 1;      -- LINK_TMP 테이블의 구조는 LINK와 같고 데이터는 0건이 된다.
```

```SQL
INSERT INTO 
       LINK_TMP
SELECT * FROM LINK;
  
COMMIT;

SELECT * FROM LINK_TMP;
```

<img src="/images/S-SQL-Manipulation-1/image-20201203135135326.png" alt="image-20201203135135326" style="zoom:80%;" />

<br />

<br />

## **2. UPDATE 문**

### 2-1. 개념

UPDATE 문은 테이블에 존재하는 데이터를 수정하는 작업이다. 업무를 처리하는데 필수적인 것이며 동시성에 유의해야 한다.

* UPDATE는 대상 행에 대해서 락(LOCK)을 잡는다.
* 락(LOCK)이란 다른 사용자는 해당 행에 대해서 작업을 하지 못한다는 것이다. (대기하게 됨)
* 즉 UPDATE를 한 후 재빨리 COMMIT을 하지 않는다면 RDBMS의 동시성이 낮아진다. 

<br />

### 2-2. UPDATE 문법

```SQL
UPDATE
  TABLE_NAME           -- UPDATE할 테이블 지정
SET
  COLUMN_1 = VALUE1,   -- 수정할 컬럼 및 값 입력
  COLUMN_2 = VALUE2
WHERE
  조건;                 -- 대상 조건
```

<br />

### 2-3. UPDATE 실습

#### \>> 실습 준비

```SQL
ALTER TABLE LINK ADD COLUMN LAST_UPDATE DATE;    -- LINK테이블에 LAST_UPDATE컬럼을 추가
ALTER TABLE LINK ALTER COLUMN LAST_UPDATE SET DEFAULT CURRENT_DATE;  -- LAST_UPDATE 컬럼의 기본값을 현재시간으로 함

SELECT * FROM LINK;
```

<img src="/images/S-SQL-Manipulation-1/image-20201203160947571.png" alt="image-20201203160947571" style="zoom:80%;" />

<br />

<br />

#### >> UPDATE 문 실습

**(1) 지정 범위 수정** (WHERE절)

**[MISSION]**  LAST_UPDATE 컬럼의 값을 지정한 DEFAULT값으로 UPDATE하기

```SQL
UPDATE LINK
   SET LAST_UPDATE = DEFAULT
 WHERE LAST_UPDATE IS NULL;
 
COMMIT;
```

```SQL
SELECT * FROM LINK;
```

<img src="/images/S-SQL-Manipulation-1/image-20201203171411659.png" alt="image-20201203171411659" style="zoom:80%;" />

<br />

<br />

**(2) 전체 테이블 수정**

**[MISSION]**  REL컬럼의 값을 'NO DATA'로 수정하기

* 이 기능은 조심해서 사용 필요.

```SQL
UPDATE LINK
   SET REL = 'NO DATA';
   
COMMIT;
```

<img src="/images/S-SQL-Manipulation-1/image-20201203172450557.png" alt="image-20201203172450557" style="zoom:80%;" />

<br />

<br />

**(3) 전체 테이블 수정 -- 특정 컬럼을 이용**

**[MISSION]**  DESCRIPTION 컬럼을 NAME 컬럼의 값으로 채우기

```sql
UPDATE LINK
   SET DESCRIPTION = NAME;
   
COMMIT;
```

<img src="/images/S-SQL-Manipulation-1/image-20201204092744650.png" alt="image-20201204092744650" style="zoom:80%;" />

<br />

<br />

## **3. UPDATE JOIN 문**

### 3-1. 개념

UPDATA 시 다른 테이블의 내용을 참조하고 싶을 때 UPDATE JOIN 문을 사용한다. 복잡한 업무를 처리하는데 매우 유용한 방법이다.

<br />

### 3-2. UPDATE JOIN 문법

```SQL
UPDATE
       TARGET_TABLE A              -- UPDATE할 테이블 지정
   SET A.COLUMN_1 = 표현식          -- 특정 컬럼 UPDATE
  FROM REF_TABLE B                 -- 참조 테이블 지정
 WHERE A.COLUMN_1 = B.COLUMN_1;    -- 조인 조건
```

<br />

### 3-3. UPDATE JOIN 실습

#### >> 실습 준비

```SQL
CREATE TABLE PRODUCT_SEGMENT
(
 ID SERIAL PRIMARY KEY,
 SEGMENT VARCHAR NOT NULL,
 DISCOUNT NUMERIC (4, 2)
);
```

```SQL
INSERT INTO PRODUCT_SEGMENT
(SEGMENT, DISCOUNT)
VALUES
   ('Grand Luxury', 0.05),
   ('Luxury', 0.06),
   ('Mass', 0.1);
COMMIT;
```

<br />

```SQL
CREATE TABLE PRODUCT
(
 ID SERIAL PRIMARY KEY,
 NAME VARCHAR NOT NULL,
 PRICE NUMERIC(10, 2),          -- 정가
 NET_PRICE NUMERIC(10, 2),      -- 할인가 (실 판매가)
 SEGMENT_ID INT NOT NULL,
 FOREIGN KEY(SEGMENT_ID)
 REFERENCES PRODUCT_SEGMENT(ID)
);
```

```SQL
INSERT INTO PRODUCT (NAME, PRICE, SEGMENT_ID)
VALUES
	('K5', 804.89, 1),
  	('K7', 228.55, 3),
  	('K9', 366.45, 2),
 	('SONATA', 145.33, 3),
 	('SPARK', 551.77, 2),
 	('AVANTE', 261.58, 3),
 	('LOZTE', 519.62, 2),
 	('SANTAFE', 843.31, 1),
 	('TUSON', 254.18, 3),
 	('TRAX', 427.78, 2),
 	('ORANDO', 936.29, 1),
 	('RAY', 910.34, 1),
 	('MORNING', 208.33, 3),
 	('VERNA', 985.45, 1),
 	('K8', 841.26, 1),
 	('TICO', 896.38, 1),
 	('MATIZ', 575.74, 2),
 	('SPORTAGE', 530.64, 2),
 	('ACCENT', 892.43, 1),
 	('TOSCA', 161.71, 3);
COMMIT;
```

![image-20201204103115223](/images/S-SQL-Manipulation-1/image-20201204103115223.png)

<br />

```SQL
SELECT * FROM PRODUCT_SEGMENT;
```

<img src="/images/S-SQL-Manipulation-1/image-20201204103657029.png" alt="image-20201204103657029" style="zoom:80%;" />

<br />

```SQL
SELECT * FROM PRODUCT;
```

<img src="/images/S-SQL-Manipulation-1/image-20201204103747274.png" alt="image-20201204103747274" style="zoom:80%;" />

<br />

<br />

#### >> UPDATE JOIN 문 실습

**[MISSION]**  PRODUCT_SEGMENT 테이블에 있는 할인율(DISCOUNT) 정보를 이용해서 PRODUCT 테이블의 NET_PRICE (할인가 / 실 판매가)를 계산하여 채우기

```SQL
UPDATE PRODUCT A
   SET NET_PRICE = A.PRICE * (1 - B.DISCOUNT)
  FROM PRODUCT_SEGMENT B
 WHERE A.SEGMENT_ID = B.ID;
```

```SQL
SELECT * FROM PRODUCT;
```

<img src="/images/S-SQL-Manipulation-1/image-20201204112104933.png" alt="image-20201204112104933" style="zoom:80%;" />

<br />

<br />


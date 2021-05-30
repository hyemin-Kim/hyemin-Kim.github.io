---
title: SQL >> 데이터 조작 (2)
tags:
  - SQL
  - Manipulation
categories:
  - 【STUDY - SQL】
  - SQL - 8. Manipulation
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: 'DELETE 문, UPSERT 문, EXPORT 작업, IMPORT 작업'
typora-root-url: ..
abbrlink: 23606
date: 2020-12-07 13:46:50
---

# 데이터 조작 (2)

@[toc]

<br />

## **1. DELETE 문**

### 1-1. 개념

DELETE문은 테이블에서 특정 데이터를 삭제하거나 테이블 내에 존재하는 모든 데이터를 삭제할 수 있다.

<br />

### 1-2. DELETE 문법

#### (1) DELETE 

```SQL
DELETE
  FROM TARGET_TABLE A
 WHERE 조건식;          -- 삭제할 행에 대한 조건
 
COMMIT;
```

<br />

#### (2) DELETE JOIN 

DELETE 시 다른 테이블의 내용을 참조하고 싶을 때 DELETE JOIN 문을 사용한다. 

```SQL
DELETE
  FROM TARGET_TABLE A
 USING REF_TABLE B     -- 참조 테이블 지정 
 WHERE 조건식;          -- JOIN & DELETE 조건
 
COMMIT;
```

<br />

<br />

### 1-3. DELETE 문 실습

```SQL
SELECT * FROM LINK;
```

<img src="/images/S-SQL-Manipulation-2/image-20201204135107666.png" alt="image-20201204135107666" style="zoom:80%;" />

<br />

```SQL
SELECT * FROM LINK_TMP;
```

<img src="/images/S-SQL-Manipulation-2/image-20201203135135326.png" alt="image-20201203135135326" style="zoom:80%;" />

<br />

<br />

#### (1) 특정 조건의 행을 삭제

**[MISSION]** LINK테이블에서 ID가 5인 행을 삭제

```SQL
SELECT * FROM LINK;
```

<img src="/images/S-SQL-Manipulation-2/image-20201204135107666.png" alt="image-20201204135107666" style="zoom:80%;" />

<br />

```SQL
DELETE
  FROM LINK
 WHERE ID = 5;
 
COMMIT;

SELECT * FROM LINK;
```

<img src="/images/S-SQL-Manipulation-2/image-20201204135350865.png" alt="image-20201204135350865" style="zoom:80%;" />

<br />

<br />

#### (2) DELETE JOIN의 사용

**[MISSION]**  LINK_TMP 테이블에서 ID가 LINK 테이블의 ID 와 매칭된 행을 삭제

```SQL
SELECT * FROM LINK;
```

<img src="/images/S-SQL-Manipulation-2/image-20201204135350865.png" alt="image-20201204135350865" style="zoom:80%;" />

<br />

```SQL
SELECT * FROM LINK_TMP;
```

<img src="/images/S-SQL-Manipulation-2/image-20201203135135326.png" alt="image-20201203135135326" style="zoom:80%;" />

<br />

```SQL
DELETE
  FROM LINK_TMP A
 USING LINK B
 WHERE A.ID = B.ID;
```

```SQL
SELECT * FROM LINK_TMP;
```

![image-20201204144847961](/images/S-SQL-Manipulation-2/image-20201204144847961.png)

<br />

<br />

#### (3) 전체 행 삭제

**\>> LINK 테이블**

```SQL
SELECT * FROM LINK;
```

<img src="/images/S-SQL-Manipulation-2/image-20201204135350865.png" alt="image-20201204135350865" style="zoom:80%;" />

<br />

```SQL
DELETE FROM LINK;
COMMIT;

SELECT * FROM LINK;
```

<img src="/images/S-SQL-Manipulation-2/image-20201204150231132.png" alt="image-20201204150231132" style="zoom:80%;" />

<br />

<br />

**\>> LINK_TMP 테이블**

```SQL
SELECT * FROM LINK_TMP;
```

<img src="/images/S-SQL-Manipulation-2/image-20201204144847961.png" alt="image-20201204144847961" style="zoom:80%;" />

<br />

```SQL
DELETE FROM LINK_TMP;
COMMIT;

SELECT * FROM LINK_TMP;
```

![image-20201204150440196](/images/S-SQL-Manipulation-2/image-20201204150440196.png)

<br />

<br />

## **2. UPSERT 문**

### 2-1. 개념

UPSERT문은 INSERT를 시도할 때 조건(상황)에 따라 UPDATE를 할 수 있는 구문이다. 복잡한 업무 처리에 자주 사용된다. 

<br />

### 2-2. UPSERT 문법

```SQL
INSERT INTO TABLE_NAME (COLUMN_1) 
     VALUES (VALUE_1)                 -- INSERT 시도
ON CONFLICT TARGET ACTION;            -- 충돌 시 다른 액션 
```

<br />

### 2-3. UPSERT 문 실습

#### >> 실습 준비

```SQL
CREATE TABLE CUSTOMERS
(
  CUSTOMER_ID SERIAL PRIMARY KEY,
  NAME VARCHAR UNIQUE,
  EMAIL VARCHAR NOT NULL,
  ACTIVE BOOL NOT NULL DEFAULT TRUE
);
```

* NAME 컬럼이 UNIQUE 제약 조건 컬럼임을 주의 한다.

* 즉 NAME 컬럼은 중복된 값이 존재할 수 없다

  <br />


```SQL
INSERT INTO CUSTOMERS (NAME, EMAIL)
VALUES
  ('IBM', 'contact@ibm.com'),
  ('Microsoft', 'contact@microsoft.com'),
  ('Intel', 'contact@intel.com');
  
COMMIT;
```

```SQL
SELECT * FROM CUSTOMERS;
```

<img src="/images/S-SQL-Manipulation-2/image-20201204161107381.png" alt="image-20201204161107381" style="zoom:80%;" />

<br />

<br />

#### >> UPSERT 문 실습 -- DO NOTHING

**DO NOTHING:**  INSERT 액션이 충돌 시 (기존에 존재할 경우) 아무것도 안함

<br />

**[MISSION]**  Microsoft(기존에 존재하는 NAME)에 EMAIL 주소 추가

* 'Microsoft'라는 NAME이 이미 존재하므로 NAME의 UNIQUE 조건과 충돌
* 이런 경우에 아무 액션도 취하지 않음 (즉, 변화 없음)

```SQL
INSERT INTO CUSTOMERS (NAME, EMAIL)
     VALUES ('Microsoft',
             'hotline@microsoft.com')
ON CONFLICT (NAME)      -- 충돌 시(기존에 존재할 경우)
DO NOTHING;             -- 아무 것도 안함

COMMIT;
```

<img src="/images/S-SQL-Manipulation-2/image-20201204161107381.png" alt="image-20201204161107381" style="zoom:80%;" />

<br />

* 해당 DO NOTHING 명령어 없으면 SQL ERROR 발생 

```SQL
INSERT INTO CUSTOMERS (NAME, EMAIL)
     VALUES ('Microsoft',
             'hotline@microsoft.com')
ON CONFLICT (NAME)
```

<img src="/images/S-SQL-Manipulation-2/image-20201207095200026.png" alt="image-20201207095200026" style="zoom: 80%;" />

<br />

<br />

#### >> UPSERT 문 실습 -- UPDATE

**UPDATE:**  INSERT 액션이 충돌 시 (기존에 존재할 경우) UPDATE 함

<br />

**[MISSION]**  Microsoft(기존에 존재하는 NAME)에 EMAIL 주소 추가

* 'Microsoft'라는 NAME이 이미 존재하므로 NAME의 UNIQUE 조건과 충돌

* 이런 경우에 데이터를 UPDATE함

```SQL
INSERT INTO CUSTOMERS (NAME, EMAIL)
     VALUES ('Microsoft',
             'hotline@microsoft.com')
ON CONFLICT (NAME)       -- 충돌 검증 컬럼
  DO UPDATE
        SET EMAIL = EXCLUDED.EMAIL || '; ' || CUSTOMERS.EMAIL;
            -- EXCLUDED.EMAIL은 위에서 INSERT 시도한 EMAIL값을 가리킴
            
COMMIT;
```

<img src="/images/S-SQL-Manipulation-2/image-20201207102128506.png" alt="image-20201207102128506" style="zoom:80%;" />

<br />

<br />

## **3. EXPORT 작업**

### 3-1. 개념

EXPORT는 테이블의 데이터를 다른 형태의 데이터로 추출하는 작업이다. 대표적으로 CSV 형식으로 가장 많이 추출한다.

<br />

### 3-2. EXPORT 작업 실습

```SQL
SELECT * FROM DATEGORY;
```

<img src="/images/S-SQL-Manipulation-2/image-20201207110518434.png" alt="image-20201207110518434" style="zoom:80%;" />

<br />

#### >> 실습 -- 엑셀(.CSV) 형식으로 출력

```SQL
COPY CATEGORY (CATEGORY_ID, NAME, LAST_UPDATE)  -- 추출할 테이블과 컬럼을 지정
TO 'E:\Study_SQL\DB_CATEGORY.csv'               -- 추출한 데이터를 저장할 파일을 지정
DELIMITER ','       -- 구분자를 지정
CSV HEADER;         -- 파일 형식을 지정
```

* 저장 디랙토리(폴더)는 반드시 미리 존재해야 한다 (여기서는 'E:\Study_SQL')

<br />

<img src="/images/S-SQL-Manipulation-2/image-20201207111613206.png" alt="image-20201207111613206" style="zoom: 60%;" />

<br />

<img src="/images/S-SQL-Manipulation-2/image-20201207111745428.png" alt="image-20201207111745428" style="zoom:50%;" />

<br />

#### >> 실습 -- 텍스트(.TXT) 파일로 출력

```SQL
COPY CATEGORY(CATEGORY_ID, NAME, LAST_UPDATE)
TO 'E:\Study_SQL\DB_CATEGORY.txt'
DELIMITER '|'
CSV HEADER;
```

<img src="/images/S-SQL-Manipulation-2/image-20201207112258741.png" alt="image-20201207112258741" style="zoom:60%;" />

<br />

<img src="/images/S-SQL-Manipulation-2/image-20201207112337940.png" alt="image-20201207112337940" style="zoom:50%;" />

<br />

#### >> 실습 -- 컬럼명 없이 출력

```sql
COPY CATEGORY(CATEGORY_ID, NAME, LAST_UPDATE)
TO 'E:\Study_SQL\DB_CATEGORY_2.csv'
DELIMITER ','
CSV;
```

<img src="/images/S-SQL-Manipulation-2/image-20201207112700637.png" alt="image-20201207112700637" style="zoom:50%;" />

<br />

<br />

## **4. IMPORT 작업**

### 4-1. 개념

IMPORT는 다른 형식의 데이터를 테이블에 넣는 작업을 말한다. 데이터 구축 시 자주 사용 된다.

<br />

### 4-2. IMPORT 작업 실습

#### >> 실습 준비

```SQL
CREATE TABLE CATEGORY_IMPORT
(
  CATEGORY_ID SERIAL NOT NULL,
  "NAME" VARCHAR(25) NOT NULL,
  LAST_UPDATE TIMESTAMP NOT NULL DEFAULT NOW(),
  CONSTRAINT CATEGORY_IMPORT_PKEY PRIMARY KEY (CATEGORY_ID)
);
```

```SQL
SELECT * FROM CATEGORY_IMPORT;
```

<img src="/images/S-SQL-Manipulation-2/image-20201207113847655.png" alt="image-20201207113847655"  />

<br />

#### >> 실습 -- 엑셀파일을 적재

```SQL
COPY CATEGORY_IMPORT(CATEGORY_ID, "NAME", LAST_UPDATE)  -- 적재할 테이블 및 컬럼을 지정
FROM 'E:\Study_SQL\DB_CATEGORY.csv'                     -- 적재할 파일을 지정
DELIMITER ','        -- 적재할 파일의 구분자를 알려준다
CSV HEADER;          -- 파일 형식을 지정한다
```

```SQL
SELECT * FROM CATEGORY_IMPORT;
```

<img src="/images/S-SQL-Manipulation-2/image-20201207114306348.png" alt="image-20201207114306348" style="zoom:80%;" />

<br />

#### >> 실습 -- 텍스트 파일을 적재

```SQL
-- 실습 전 먼저 데이터를 삭제해야 함
DELETE FROM CATEGORY_IMPORT;
COMMIT;
```

```SQL
COPY CATEGORY_IMPORT(CATEGORY_ID, "NAME", LAST_UPDATE)
FROM 'E:\Study_SQL\DB_CATEGORY.txt'
DELIMITER '|'
CSV HEADER;
```

```SQL
SELECT * FROM CATEGORY_IMPORT;
```

<img src="/images/S-SQL-Manipulation-2/image-20201207130748150.png" alt="image-20201207130748150" style="zoom:80%;" />

<br />

#### >> 실습 -- 컬럼명이 없는 엑셀 파일 적재

```SQL
-- 실습 전 먼저 데이터를 삭제해야 함
DELETE FROM CATEGORY_IMPORT;
COMMIT;
```

```SQL
COPY CATEGORY_IMPORT(CATEGORY_ID, "NAME", LAST_UPDATE)
FROM 'E:\Study_SQL\DB_CATEGORY_2.csv'
DELIMITER ','
CSV;

SELECT * FROM CATEGORY_IMPORT;
```

<img src="/images/S-SQL-Manipulation-2/image-20201207131800879.png" alt="image-20201207131800879" style="zoom:80%;" />

<br />

* DB_CATEGOROY_2.csv 파일은 컬럼명(header) 이 존재하지 않으므로 반드시 HEADER를 제거해야한다.

* HEADER를 제거하지 않을 경우 가장 첫번째 데이터를 헤더로 인식하여 한건이 누락된다

```SQL
DELETE FROM CATEGORY_IMPORT;
COMMIT;
```

```SQL
COPY CATEGORY_IMPORT(CATEGORY_ID, "NAME", LAST_UPDATE)
FROM 'E:\Study_SQL\DB_CATEGORY_2.csv'
DELIMITER ','
CSV HEADER;

SELECT * FROM CATEGORY_IMPORT;
```

<img src="/images/S-SQL-Manipulation-2/image-20201207132305818.png" alt="image-20201207132305818" style="zoom:80%;" />

<br />

<br />

  
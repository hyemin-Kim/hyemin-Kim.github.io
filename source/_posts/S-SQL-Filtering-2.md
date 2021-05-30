---
title: SQL >> 데이터 필터링 (2)
tags:
  - SQL
  - Filtering
categories:
  - 【STUDY - SQL】
  - SQL - 2. Data Filtering
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: '데이터 필터링 -- IN 연산자, BETWEEN 연산자, LIKE 연산자, IS NULL 연산자'
typora-root-url: ..
abbrlink: 17046
date: 2020-11-10 14:25:03
---

# 데이터 필터링 (2) 

@[toc]

<br />

## **1. IN 연산자**

### 1-1. 용도

IN 연산자는 특정 집합(컬럼 혹은 리스트)에서 특정 집합 혹은 리스트가 존재하는지 판단하는 연산자이다.

<br />

### 1-2. IN 연산자 문법

#### 1) IN 문법

```SQL
-- COLUMN_NAME 집합에서 VALUE1, VALUE2등의 값이 존재하는지 확인 (조건에 만족한 행을 출력)
SELECT 
  *
FROM
  TABLE_NAME
WHERE COLUMN_NAME IN (VALUE1, VALUE2, ...)
```

 <br />

```SQL
-- COLUMN_NAME 집합에서 TABLE_NAME2 테이블의 COLUMMN_NAME2 집합이 존재하는지 확인
SELECT
  *
FROM
  TABEL_NAME
WHERE COLUMN_NAME IN 
  (SELECT COLUMN_NAME2 FROM TABLE_NAME2)  -- 서브 커리
```

<br />

#### 2) NOT IN 문법

```SQL
-- NOT IN --
-- COLUMN_NAME 집합에서 값이 VALUE1, VALUE2가 아닌 행을 출력
SELECT 
  * 
FROM
  TABLE_NAME
WHERE
  COLUMN_NAME NOT IN (VALUE1, VALUE2)
```

<br />



### 1-3. IN 연산자 실습

**\>> TABLE**



| rental                                                       |
| :------------------------------------------------------------: |
| \* rental_id <br/>rental_date <br/>inventory_id <br/>customer_id <br/>return_date <br/>staff_id <br/>last_update |


<br />

**>> IN 실습**  

```sql
-- CUSTOMER_ID가 1 혹은 2인 행을 뽑아서 RETURN_DATE 내림차순으로 출력한다 
SELECT
  CUSTOMER_ID,
  RENTAL_ID,
  RETURN_DATE
FROM
  RENTAL
WHERE 
  CUSTOMER_ID IN (1, 2)
ORDER BY 
  RETURN_DATE DESC
```

<img src="/images/S-SQL-Filtering-2/image-20201109192003435.png" alt="image-20201109192003435" style="zoom:80%;" />

<br />

* IN 연산자는 'OR' && '=' 과 같다

```SQL
-- OR 사용 --
-- CUSTOMER_ID가 1 혹은 2인 행을 뽑아서 RETURN_DATE 내림차순으로 출력한다

SELECT 
  CUSTOMER_ID,
  RENTAL_ID,
  RETURN_DATE
FROM
  RENTAL
WHERE 
  CUSTOMER_ID = 1 OR
  CUSTOMER_ID = 2
ORDER BY
  RETURN_DATE DESC
```

<img src="/images/S-SQL-Filtering-2/image-20201109192003435-1604987159526.png" alt="image-20201109192003435" style="zoom:80%;" />

<br />

**\>> NOT IN 실습**

```SQL
-- CUSTOMER_ID가 1 혹은 2가 아닌 행을 뽑아서 RETURN_DATE 내림차순으로 출력한다

SELECT
  CUSTOMER_ID,
  RENTAL_ID,
  RETURN_DATE
FROM 
  RENTAL
WHERE 
  CUSTOMER_ID NOT IN (1, 2)
ORDER BY
  RETURN_DATE DESC
```

<img src="/images/S-SQL-Filtering-2/image-20201109194032659.png" alt="image-20201109194032659" style="zoom:80%;" />

<br />

* NOT IN 연산자는 'AND' && '!=' 과 같다

```SQL
-- CUSTOMER_ID가 1 혹은 2가 아닌 행을 뽑아서 RETURN_DATE 내림차순으로 출력한다

SELECT
  CUSTOMER_ID,
  RENTAL_ID,
  RETURN_DATE
FROM 
  RENTAL
WHERE 
  CUSTOMER_ID != 1 AND
  CUSTOMER_ID != 2
ORDER BY
  RETURN_DATE DESC
```

<img src="/images/S-SQL-Filtering-2/image-20201109194032659-1604987190631.png" alt="image-20201109194032659" style="zoom:80%;" />

<br />

**\>> 서브 커리**

**Mission:** 2005년 5월 27일에 DVD 반납한 고객의  이름(FIRST_NAME & LAST_NAME)을 출력

1. 먼저 RENTAL 테이블에서 2005년 5월 27일에 DVD 반납한 고객의 ID(CUSTOMER_ID)를 추출 (서브 커리 부분)
2. 그다음 CUSTOMER 테이블에서 해당 ID인 고객의 이름(FIRST_NAME & LAST_NAME)을 출력 (메인 커리 부분)

```SQL
-- 서브 커리 부분 --
-- RETURN_DATE가 2005년 5월 27일인 CUSTOMER_ID를 출력한다
SELECT 
  CUSTOMER_ID
FROM 
  RENTAL
WHERE 
  CAST(RETURN_DATE AS DATE) = '2005-05-27'
```

<img src="/images/S-SQL-Filtering-2/image-20201109213802126.png" alt="image-20201109213802126" style="zoom:80%;" />

<br />

```SQL
-- 메인 커리 부분 --
-- 해당 ID인 고객의 FIRST_NAME & LAST_NAME 출력

SELECT
  FIRST_NAME, LAST_NAME
FROM
  CUSTOMER
WHERE 
  CUSTOMER_ID IN (
    SELECT
      CUSTOMER_ID
    FROM 
      RENTAL
    WHERE
      CAST(RETURN_DATE AS DATE) = '2005-05-27')
```

<img src="/images/S-SQL-Filtering-2/image-20201109214929978.png" alt="image-20201109214929978" style="zoom:80%;" />

<br />

<br />

## **2. BETWEEN 연산자**

### 2-1. 용도

BETWEEN 연산자는 특정 집합에서 어떠한 컬럼의 값이 특정 범위안에 들어가는 집합을 출력하는 연산자이다.

<br />

### 2-2. BATWEEN 연산자 문법

#### 1) BETWEEN 문법

```SQL
-- COLUMN_NAME의 값이 VALUE_A와 VALUE_B사이에 있는 집합을 출력한다
-- COLUMN_NAME >= VALUE_A AND COLUMN_NAME <= B

SELECT
  *
FROM
  TABLE_NAME
WHERE COLUMN_NAME 
  BETWEEN VALUE_A AND VALUE_B  
```

<br />

#### 2) NOT BETWEEN 문법

```SQL
-- COLUMN_NAME의 값이 VALUE_A와 VALUE_B 사이에 있지 않은 집합을 출력한다
-- COLUMN_NAME < VALUE_A OR COLUMN_NAME > VALUE_B

SELECT
  * 
FROM
  TABLE_NAME
WHERE COLUMN_NAME
  NOT BETWEEN VALUE_A AND VALUE_B
```

<br />

### 2-3. BETWEEN 연산자 실습

**\>> TABLE**


| payment                                                      |
| :------------------------------------------------------------: |
| \* payment_id <br/>customer_id <br/>staff_id <br/>rental_id <br/>amount <br/>payment_date |


<br />

**\>> BETWEEN  실습**

```SQL
-- PAYMENT 테이블에서 AMOUNT가 8과 9사이에 있는 행의 CUSTOMER_ID, PAYMENT_ID, AMOUNT를 출력
SELECT
  CUSTOMER_ID, 
  PAYMENT_ID,
  AMOUNT
FROM
  PAYMENT
WHERE AMOUNT BETWEEN 8 AND 9
```

<img src="/images/S-SQL-Filtering-2/image-20201110090038727.png" alt="image-20201110090038727" style="zoom:80%;" />

<br />

```SQL
-- 위 SQL은 이 SQL과 결과가 동일함
SELECT
  CUSTOMER_ID,
  PAYMENT_ID,
  AMOUNT
FROM
  PAYMENT
WHERE AMOUNT >= 8 AND
      AMOUNT <- 9
```

<br />

**\>> NOT BETWEEN 실습**

```SQL
-- PAYMENT 테이블에서 AMOUNT가 8부터 9사이가 아닌 행의 CUSTOMER_ID, PAYMENT_ID, AMOUNT를 출력
SELECT
  CUSTOMER_ID,
  PAYMENT_ID,
  AMOUNT
FROM
  PAYMENT
WHERE AMOUNT NOT BETWEEN 8 AND 9
```

<img src="/images/S-SQL-Filtering-2/image-20201110091032703.png" alt="image-20201110091032703" style="zoom:80%;" />

<br />

```SQL
-- 위 SQL은 이 SQL과 결과가 동일함
SELECT
  CUSTOMER_ID,
  PAYMENT_ID,
  AMOUNT
FROM
  PAYMENT
WHERE AMOUNT < 8 OR
      AMOUNT > 9
```

<br />

**\>> 일자 비교**

```SQL
-- PAYMENT_DATE가 2007년 2월 7일부터 2007년 2월 15일 데이터를 추출함

-- [방법 1]
SELECT
  CUSTOMER_ID, PAYMENT_ID,
  AMOUNT,      PAYMENT_DATE
FROM
  PAYMENT
WHERE CAST(PAYMENT_DATE AS DATE)
  BETWEEN '2007-02-07' AND '2007-02-15'
  
-- [방법 2]
SELECT
  CUSTOMER_ID, PAYMENT_ID,
  AMOUNT,      PAYMENT_DATE
FROM 
  PAYMENT
WHERE TO_CHAR(PAYMENT_DATE, 'YYYY-MM-DD')
  BETWEEN '2007-02-07' AND '2007-02-15'
```

<img src="/images/S-SQL-Filtering-2/image-20201110092522372.png" alt="image-20201110092522372" style="zoom:80%;" />

<br />

```SQL
-- CAST( # AS DATE)와 TO_CHAR( # , 'YYYY-MM-DD')의 결과 확인
SELECT
  CUSTOMER_ID, PAYMENT_ID,
  AMOUNT,      PAYMENT_DATE,
  CAST(PAYMENT_DATE AS DATE),          
  TO_CHAR(PAYMENT_DATE, 'YYYY-MM-DD')  
FROM 
  PAYMENT
WHERE TO_CHAR(PAYMENT_DATE, 'YYYY-MM-DD')
  BETWEEN '2007-02-07' AND '2007-02-15'
```

<img src="/images/S-SQL-Filtering-2/image-20201110093852708.png" alt="image-20201110093852708" style="zoom:80%;" />

<br />

<br />

## **3. LIKE 연산자**

### 3-1. 용도

LIKE연산자는 특정 집합에서 어떠한 컬럼의 값이 특정 값과 유사한 패턴을 갖는 집합을 출력하는 연산자이다.

<br />

### 3-2. LIKE 연산자 문법

#### 1) LIKE 문법

```SQL
-- COLUMN_NAME 컬럼의 값이 특정 패턴과 유사한 집합을 출력
SELECT 
  *
FROM
  TABLE_NAME
WHERE COLUMN_NAME
  LIKE 특정패턴
```

<br />

#### 2) NOT LIKE 문법

```SQL
-- COLUMN_NAME 컬럼의 값이 특정 패턴과 유사하지 않은 집합을 출력
SELECT
  *
FROM
  TABLE_NAME
WHERE COLUMN_NAME
  NOT LIKE 특정패턴
```

<br />

#### 3) 특정 패턴

* 특정 패턴에서 **%**는 어떠한 **문자 혹은 문자열**을 의미함 (길이가 상관없음)
* 특정 패턴에서 **_**는 **한 개의 문자**를 의미함

<br />

### 3-3. LIKE 연산자 실습

**\>> TABLE**


| customer                                                     |
| :------------------------------------------------------------: |
| \* customer_id <br>store_id <br>first_name <br/>email <br/>address_id <br/>activebool <br/>create_date <br/>last_update <br/>active |


<br />

**\>> LIKE 실습**

[```## LIKE '&&'```] 절은 ```TURE``` / ```FALSE```를 반환한다.  

'```%```'와 '```_```'를 이해하기 위해 다음 예를 살펴본다:

<div width = 100%>

| SQL                     | 결과값 | 설명                                                         |
| :---------------------- | :------: | :------------------------------------------------------------ |
| SELECT            |        |                                                              |
| 'FOO' LIKE 'FOO', | TRUE   | 'FOO'는 'FOO'이므로 참이다                                   |
| 'FOO' LIKE 'F%',  | TRUE   | 'F%'는 'F'로 시작하면 모두 참이다                            |
| 'FOO' LIKE '\_O\_', | TRUE   | '\_O\_'는 3자리 문자열이고 가운든 문자가 'O'라면 모두 참이다  |
| 'BAR' LIKE 'B\_'   | TRUE   | '\_B\_'는 B로 시작하는 2자리 문자열이면 모두 참. 하지만 'BAR'는 'B'로 시작하는 3자리 문자열이다 |

</div>

<br />

  ```SQL
-- FIRST_NAME이 'Jen'으로 시작하는 집합을 출력
-- 즉, 'Jen'뒤에 어떤 문자 혹은 문자열이든 OK

SELECT
  FIRST_NAME, 
  LAST_NAME
FROM 
  CUSTOMER
WHERE 
  FIRST_NAME LIKE 'Jen%'
  ```

<img src="/images/S-SQL-Filtering-2/image-20201110105536650.png" alt="image-20201110105536650" style="zoom:80%;" />

<br />

```SQL
-- FIRST_NAME에 'er'이 존재하는 모든 집합을 출력
-- 즉, 'er'앞과 뒤에 어떤 문자 혹은 문자열이든 OK

SELECT
  FIRST_NAME,
  LAST_NAME
FROM
  CUSTOMER
WHERE 
  FIRST_NAME LIKE '%er%'
```

<img src="/images/S-SQL-Filtering-2/image-20201110113041772.png" alt="image-20201110113041772" style="zoom:80%;" />

<br />

```SQL
-- FIRST_NAME: 하나의 문자 + 'her' + 임의의 문자/문자열

SELECT
  FIRST_NAME,
  LAST_NAME
FROM
  CUSTOMER
WHERE
  FIRST_NAME LIKE '_her%'
```

<img src="/images/S-SQL-Filtering-2/image-20201110113454144.png" alt="image-20201110113454144" style="zoom:80%;" />

<br />

**\>> NOT LIKE 실습**

```SQL
-- FIRST_NAME이 'jen'으로 시작하지 않는 집합을 출력

SELECT
  FIRST_NAME,
  LAST_NAME
FROM 
  CUSTOMER
WHERE
  FIRST_NAME NOT LIKE 'Jen%'
```

<img src="/images/S-SQL-Filtering-2/image-20201110113847995.png" alt="image-20201110113847995" style="zoom:80%;" />

<br />

<br />

## **4. IS NULL 연산자**

### 4-1. 용도

IS NULL 연산자는 특정 컬럼 혹은 값이 NULL 값인지 아닌지를 판단하는 연산자이다.

IS NULL 혹은 IS NOT NULL로 NULL 유무를 판단한다.

<br />

### 4-2. IS NULL 연산자 문법

#### 1) IS NULL 문법

```SQL
-- COLUMN_NAME 컬럼의 값이 NULL인 집합을 출력
SELECT 
  *
FROM
  TABLE_NAME
WHERE
  COLUMN_NAME IS NULL
```

<br />

#### 2) IS NOT NULL 문법

```SQL
-- COLUMN_NAME 컬럼의 값이 NULL이 아닌 집합을 출력
SELECT 
  *
FROM
  TABLE_NAME
WHERE
  COLUMN_NAME IS NULL
```

<br />

### 4-3. IS NULL 연산자 실습

**\>> 실습 준비**

```SQL
CREATE TABLE CONTACTS
(
  ID INT GENERATED BY DEFAULT AS IDENTITY,
  FIRST_NAME VARCHAR(50) NOT NULL,
  LAST_NAME VARCHAR(50) NOT NULL,
  EMAIL VARCHAR(255) NOT NULL,
  PHONE VARCHAR(15),
  PRIMARY KEY(ID)    
)

INSERT
  INTO 
    CONTACTS(FIRST_NAME, LAST_NAME, EMIAL, PHONE)
  VALUES
    ('John', 'Doe', 'john.doe@example.com', NULL),
    ('Lily', 'Bush', 'lily.bush@example.com', '(408-234-2764)')
```

```sql
SELECT 
  *
FROM
  CONTACTS
```

<img src="/images/S-SQL-Filtering-2/image-20201110132419710.png" alt="image-20201110132419710" style="zoom:80%;" />

<br />

**\>> IS NULL 실습**

```SQL
-- PHONE 컬럼의 값이 NULL인 집합을 출력
SELECT 
  *
FROM
  CONTACTS
WHERE 
  PHONE IS NULL
```

<img src="/images/S-SQL-Filtering-2/image-20201110133053492.png" alt="image-20201110133053492" style="zoom:80%;" />

<br />

* **[주의]** NULL은 "=" 연산으로 비교할 수 없다

```SQL
SELECT
  *
FROM
  CONTACTS
WHERE
  PHONE = NULL
```

<img src="/images/S-SQL-Filtering-2/image-20201110133321244.png" alt="image-20201110133321244" style="zoom:80%;" />

<br />

**\>> IS NOT NULL 실습**

```SQL
-- PHONE 컬럼의 값이 NULL이 아닌 집합을 출력
SELECT
  *
FROM
  CONTACTS
WHERE
  PHONE IS NOT NULL
```

<img src="/images/S-SQL-Filtering-2/image-20201110133559770.png" alt="image-20201110133559770" style="zoom:80%;" />

<br />

<br />
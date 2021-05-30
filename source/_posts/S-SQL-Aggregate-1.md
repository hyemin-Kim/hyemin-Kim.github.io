---
title: SQL >> 집계 함수 (1) -- 기초 집계 함수
tags:
  - SQL
  - Aggregate
categories:
  - 【STUDY - SQL】
  - SQL - 4. Aggregate Function
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: '기초 집계 함수 -- GROUP BY 절, 합계 SUM(), 카운트 COUNT(), HAVING 절'
typora-root-url: ..
abbrlink: 37595
date: 2020-11-12 20:23:06
---

# 집계 함수 (1) -- 기초 집계 함수

@[toc]

<br />

## **1. GROUP BY 절**

### 1-1. 개념

GROUP BY 절은 SELECT 문에서 반환된 행을 그룹으로 나눈다. 각 그룹에 대한 합계, 평균, 카운트 등을 계산할 수 있다.

<br />

### 1-2. GROUP BY 절 문법

```SQL
SELECT
  COLUMN_1,          -- GROUPING 기준 컬럼 기재
  집계함수(COLUMN2)   -- 집계함수 사용하여 그룹별 요약값 도출
FROM
  TABLE_NAME
GROUP BY COLUMN_1;  -- GROUP BY 절 기재, N개의 컬럼을 GROUP BY 하는 경우 ','구분
                    -- GROUP BY 절은 FROM 또는 WHERE절 바로 뒤에 나타나야 함

```

<br />

### 1-3. GROUP BY 절 실습

#### 1-3-0. 실습 데이터

**>> "dvdrental" 데이터 --> "payment" 테이블**

<img src="/images/S-SQL-Aggregate-1/image-20201112164755594.png" alt="image-20201112164755594" style="zoom:80%;" />

<br />

#### 1-3-1. 단순 GROUP BY

**\>> 특정 컬럼의 UNIQUE VALUE를 추출할 때 쓰이다** (SELECT DISTINCT과 유사)

**[MISSION]** 중복 값이 제거된 CUSTOMER_ID를 추출

```SQL
-- GROUP BY 사용
SELECT
  CUSTOMER_ID
FROM
  PAYMENT
GROUP BY
  CUSTOMER_ID;
```

<img src="/images/S-SQL-Aggregate-1/image-20201112170115424.png" alt="image-20201112170115424" style="zoom:80%;" />

<br />

```SQL
-- [대체] SELECT DISTINCT 사용
SELECT 
  DISTINCT  CUSTOMER_ID
FROM PAYMENT;
```

<br />

#### 1-3-2. GROUPING + GROUP 별 요약

**1) 합계 구하기**

**[MISSION]** 거래액이 (AMOUNT의 합계) 가장 많은 고객순으로 출력

```SQL
-- 거래액이 (AMOUNT의 합계) 가장 많은 고객순으로 출력
SELECT
  CUSTOMER_ID,
  FIRST_NAME,
  LAST_NAME,
  SUM(AMOUNT) AS AMOUNT_SUM
FROM
  PAYMENT
GROUP BY
  CUSTOMER_ID
ORDER BY AMOUNT_SUM DESC;  
```

<img src="/images/S-SQL-Aggregate-1/image-20201112171724011.png" alt="image-20201112171724011" style="zoom:80%;" />

<br />

**2) 카운트 구하기**

**[MISSION 1]** 직원별 처리한 결제 건수 출력

```SQL
-- 직원별 처리한 결제 건수 출력
SELECT
  STAFF_ID,
  COUNT(PAYMENT_ID) AS N_PAYMENT
FROM
  PAYMENT
GROUP BY
  STAFF_ID;
```

![image-20201112173013752](/images/S-SQL-Aggregate-1/image-20201112173013752.png)

<br />

**[MISSION 2]** STAFF 테이블에 있는 직원 이름 (FIRST_NAME, LAST_NAME)도 함께 추출

```SQL
-- STAFF 테이블에 있는 직원 이름 (FIRST_NAME, LAST_NAME)도 함께 추출
SELECT
  A.STAFF_ID, 
  A.FIRST_NAME,
  A.LAST_NAME,
  COUNT(B.PAYMENT_ID) AS N_PAYMENT
FROM
  STAFF A
INNER JOIN 
  PAYMENT B
ON A.STAFF_ID = B.STAFF_ID
GROUP BY            -- [주의]: SELECT 문에서 집계함수를 제외한 모든 컬럼명을 GROUP BY에서 적어야 함 
  A.STAFF_ID,
  B.STAFF_ID,
  A.FIRST_NAME,
  A.LAST_NAME;
```

<img src="/images/S-SQL-Aggregate-1/image-20201112184417882.png" alt="image-20201112184417882" style="zoom:80%;" />

<br />

<img src="/images/S-SQL-Aggregate-1/image-20201112185119399.png" alt="image-20201112185119399"  />

<br />

<br />

## **2. HAVING 절**

### 2-1. 개념

HAVING 절은 GROUP BY 절과 함께 사용하여 GROUP BY의 결과를 특정 조건으로 필터링하는 기능을 한다.

<br />

### 2-2. HAVING 절 문법

```SQL
SELECT
  COLUMN_1,           -- GROUPING 기준 컬럼 기재
  집계함수(COLUMN_2)   -- 집계함수 사용하여 그룹별 요약값 도출
FROM
  TABLE_NAME
GROUP BY             -- GROUP BY 절 기재, N개의 컬럼을 GROUP BY 하는 경우 ','구분
  COLUMN_1           -- GROUP BY 절은 FROM 또는 WHERE절 바로 뒤에 나타나야 함
HAVING 조건식;
```

* HAVING 절은 GROUP BY 절에 의해 생성된 그룹행의 조건을 설정한다
* 반면에 WHERE 절은 GROUP BY 절이 적용된기 전에 개별 행의 조건을 설정한다

<br />

### 2-3. HAVING 절 실습

#### 2-3-1. GROUP BY  "합계" + HAVING

**[GROUP BY 결과 출력]**

```SQL
-- 거래액이 (AMOUNT의 합계) 가장 많은 고객순으로 출력
SELECT
  CUSTOMER_ID,
  SUM(AMOUNT) AS AMOUNT_SUM
FROM 
  PAYMENT
GROUP BY
  CUSTOMER_ID;
```

<img src="/images/S-SQL-Aggregate-1/image-20201112191152327.png" alt="image-20201112191152327" style="zoom:80%;" />

<br />

<br />

**[MISSION 1]**  GROUP BY의 결과 값 중에서 AMOUNT_SUM이 200을 초과하는 행 출력

```SQL
-- AMOUNT_SUM > 200
SELECT
  CUSTOMER_ID,
  SUM(AMOUNT) AS AMOUNT_SUM
FROM
  PAYMENT
GROUP BY
  CUSTOMER_ID
HAVING
  SUM(AMOUNT) > 200;  -- [주의]: 여기서 SUM(AMOUNT)의 ALIAS(별칭)을 쓰면 안됨.
```

* **주의:** HAVING 절 뒤에 집계 데이터의 별칭(ALIAS)을 쓰면 안됨. (The HAVING clause is evaluated before the SELECT - so the server doesn't yet know about that alias.)

![image-20201112192700072](/images/S-SQL-Aggregate-1/image-20201112192700072.png)

<br />

<br />

**[MISSION 2]**  CUSTOMER 테이블에 있는 고객 이메일 주소 (EMAIL)도 함께 추출

<img src="/images/S-SQL-Aggregate-1/image-20201112194907662.png" alt="image-20201112194907662" style="zoom:80%;" />

```SQL
SELECT 
  A.CUSTOMER_ID,
  B.EMAIL,
  SUM(A.AMOUNT) AS AMOUNT_SUM
FROM
  PAYMENT A, 
  CUSTOMER B
WHERE 
  A.CUSTOMER_ID = B.CUSTOMER_ID
GROUP BY
  A.CUSTOMER_ID,
  B.EMAIL
HAVING
  SUM(A.AMOUNT) > 200;
```

![image-20201112195342549](/images/S-SQL-Aggregate-1/image-20201112195342549.png)

<br />

<br />

#### 2-3-2. GROUP BY "카운트" + HAVING

<img src="/images/S-SQL-Aggregate-1/image-20201112200641600.png" alt="image-20201112200641600" style="zoom:80%;" />

<br />

<br />

**[GROUP BY 결과 출력]**

```SQL
-- 매장(STORE)별 구매 고객 수 추출
SELECT
  STORE_ID,
  COUNT(CUSTOMER_ID) AS N_CUSTOMER
FROM
  CUSTOMER
GROUP BY
  STORE_ID;
```

![image-20201112201143045](/images/S-SQL-Aggregate-1/image-20201112201143045.png)

<br />

**[MISSION]**  구매 고객 수가 300 이상인 매장만 출력

```SQL
-- N_CUSTOMER > 300
SELECT
  STORE_ID,
  COUNT(CUSTOMER_ID) AS N_CUSTOMER
FROM 
  CUSTOMER
GROUP BY
  STORE_ID
HAVING
  COUNT(CUSTOMER_ID) > 300;
```

![image-20201112201350582](/images/S-SQL-Aggregate-1/image-20201112201350582.png)

<br />

```SQL
-- 해당 매장 정보 출력
SELECT
  *
FROM
  STORE
WHERE
  STORE_ID = 1;
```

![image-20201112201557040](/images/S-SQL-Aggregate-1/image-20201112201557040.png)

<br />

<br />
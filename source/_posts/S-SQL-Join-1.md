---
title: SQL >> 조인 (1)
tags:
  - SQL
  - Join
categories:
  - 【STUDY - SQL】
  - SQL - 3. Join
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: 'INNER 조인, OUTER 조인'
typora-root-url: ..
abbrlink: 9725
date: 2020-11-12 14:34:10
---

# 조인 (1)

@[toc]

<br />

## **1. 조인이란?**

### 1-1. 개념

조인은 2개 이상의 테이블에 있는 정보 중 사용자가 필요한 집합에 맞게 가상의 테이블처럼 만들어서 결과를 보여주는 것이다.

<br />

### 1-2. 조인의 종류

| 종류            | 설명                                                         |
| :--------------- | :------------------------------------------------------------ |
| INNER 조인      | 특정 컬럼을 기준으로 정확히 매칭된 집합을 출력한다           |
| OUTER 조인      | 특정 컬럼을 기준으로 매칭된 집합을 출력하지만 한쪽의 집합은 모두 출력하고 다른 한쪽의 집합은 매칭되는 컬럼의 값 만을 출력한다<br> (왼쪽 집합을 기준으로 하면 LEFT OUTER, 오른쪽 집합을 기준으로 하면 RIGHT OUTER) |
| SELT 조인       | 동일한 테이블 끼리의 특정 컬럼을 기준으로 매칭되는 집합을 출력한다 |
| FULL OUTER 조인 | INNER, LEFT OUTER, RIGHT OUTER 조인 집합을 모두 출력한다     |
| CROSS 조인      | Cartesian Product이라고도 하며 조인되는 두 테이블에서 곱집합을 반환한다 |

<br />

<br />

## **2. 실습 준비**

**실습을 위한 데이터 생성**

```SQL
CREATE TABLE BASKET_A
(
  ID INT PRIMARY KEY,
  FRUIT VARCHAR (100) NOT NULL
);

CREATE TABLE BASKET_B
(
  ID INT PRIMARY KEY,
  FRUIT VARCHAR (100) NOT NULL
)
```

```SQL
INSERT INTO BASKET_A
  (ID, FRUIT)
VALUES
  (1, 'Apple'),
  (2, 'Orange'),
  (3, 'Banana'),
  (4, 'Cucumber');

COMMIT;

-- INSERT, UPDATE, DELETE로 데이터의 삽입 혹은 갱신을 실시한 후에 꼭 COMMIT/ROLLBACK을 실현해야함.

INSERT INTO BASKET_B
  (ID, FRUIT)
VALUES
  (1, 'Orange'),
  (2, 'Apple'),
  (3, 'Watermelon'),
  (4, 'Pear');

COMMIT;
```

<br />

```SQL
SELECT * FROM BASKET_A;
```

<img src="/images/S-SQL-Join-1/image-20201111095120367.png" alt="image-20201111095120367" style="zoom:80%;" />



```SQL
SELECT * FROM BASKET_B;
```

<img src="/images/S-SQL-Join-1/image-20201111095201056.png" alt="image-20201111095201056" style="zoom:80%;" />

<br />

<br />

## **3. INNER 조인**

### 3-1. 개념

INNER 조인은 대표적인 조인의 종유이다. 이는 특정 컬럼을 기준으로 정확히 매칭된 집합을 출력한다. 

<img src="/images/S-SQL-Join-1/image-20201111110318071.png" alt="image-20201111110318071" style="zoom:50%;" />

<br />

### 3-2. INNER 조인 문법

```SQL
SELECT
  A.COL_A1, A.COL_A2, ...,
  B.COL_B1, B.COL_B2, ...
FROM 
  TABLE_A A
INNER JOIN
  TABLE_B B
ON 
  A.COL_Z_A = B.COL_Z_B         -- 조인의 기준이 되는 컬럼을 지정 
```

<br />

### 3-3. INNER 조인 실습

#### 3-3-1. BASKET 데이터를 활용한 간단한 실습

```SQL
SELECT                  -- 지정한 컬럼을 조회한다
  A.ID ID_A,
  A.FRUIT FRUIT_A,
  B.ID ID_B,
  B.FRUIT FRUIT_B
FROM                    -- BASKET_A 테이블에과 BASKET_B 테이블을
  BASKET_A A            -- FRUIT 컬럼 기준으로 조인한다.
INNER JOIN
  BASKET_B B
ON 
  A.FRUIT = B.FRUIT   
```

![image-20201111111333754](/images/S-SQL-Join-1/image-20201111111333754.png)

<br />

#### 3-3-2. dvdrental 데이터를 활용한 실습

##### (1) 2개의 테이블 조인

**\>> 테이블 구성**

<img src="/images/S-SQL-Join-1/image-20201111112825354.png" alt="image-20201111112825354" style="zoom:80%;" />

* 한 명의 고객은 여러 건의 결제내역을 가질 수 있다

* 하나의 결제는 반드시 고객을 가져야 한다

  <br />

**\>> 실습**

**MISSION 1:** CUSTOMER 테이블에 있는 고객 정보와 PAYMENT 테이블에 있는 결제정보를 종합하여 추출

```SQL
SELECT
  A.CUSTOMER_ID, A.FIRST_NAME,
  A.LAST_NAME,   A.EMAIL,
  B.AMOUNT,      B.PAYMENT_DATE
FROM
  CUSTOMER A
INNER JOIN 
  PAYMENT B
ON
  A.CUSTOMER_ID = B.CUSTOMER_ID
```

![image-20201111114614830](/images/S-SQL-Join-1/image-20201111114614830.png)

<br />

**MISSION 2:**  위에서 추출된 데이터에서 CUSTOMER_ID가 2인 행만 추출

```SQL
SELECT
  A.CUSTOMER_ID, A.FIRST_NAME,
  A.LAST_NAME,   A.EMAIL,
  B.AMOUNT,      B.PAYMENT_DATE
FROM
  CUSTOMER A
INNER JOIN 
  PAYMENT B
ON
  A.CUSTOMER_ID = B.CUSTOMER_ID
WHERE 
  A.CUSTOMER_ID = 2
```

![image-20201111125419551](/images/S-SQL-Join-1/image-20201111125419551.png)

<br />

##### (2)  3개의 테이블 조인

**\>> 테이블 구성**

<img src="/images/S-SQL-Join-1/image-20201111130320223.png" alt="image-20201111130320223" style="zoom:80%;" />

* 한 명의 직원은 여러 건의 결제내역을 처리한다
* 하나의 결제는 반드시 처리한 직원이 존재한다
* 한 명의 고객은 여러 건의 결제내역을 가질 수 있다
* 하나의 결제는 반드시 고객을 가져야 한다

<br />

**>> 실습**

**MISSION:** 결제를 진행한 고객 정보(CUSTOMER), 해당 고객의 결제내역(PAYMENT), 그리고 해당 결제를 처리하는 직원정보(STAFF)를 종합하여 추출

```SQL
SELECT
  A.CUSTOMER_ID, A.FIRST_NAME,
  A.LAST_NAME,   A.EMAIL,
  B.AMOUNT,      B.PAYMENT_DATE,
  C.FIRST_NAME AS S_FIRST_NAME,
  C.LAST_NAME AS S_LAST_NAME
FROM 
  CUSTOMER A
INNER JOIN PAYMENT B
        ON A.CUSTOMER_ID = B.CUSTOMER_ID
INNER JOIN STAFF C
        ON B.STAFF_ID = C.STAFF_ID
```

![image-20201111132315338](/images/S-SQL-Join-1/image-20201111132315338.png)

<br />

<br />

## **4. OUTER 조인**

### 4-1. 개념

특정 집합을 기준으로 매칭된 집합을 출력하지만, 한쪽의 집합은 모두 출력하고 다른 한쪽의 집합은 매칭되는 컬럼의 값 만을 출력한다.

<img src="/images/S-SQL-Join-1/image-20201111133926396.png" alt="image-20201111133926396" style="zoom:50%;" />

<img src="/images/S-SQL-Join-1/image-20201111134145555.png" alt="image-20201111134145555" style="zoom:50%;" />

<br />

### 4-2. OUTER 조인 문법

#### (1) LEFT OUTER 조인 문법

```SQL
-- LEFT OUTER JOIN
SELECT
  A.COL_A1, A.COL_A2, ...,
  B.COL_B1, B.COL_B2, ...
FROM 
  TABLE_A A
LEFT OUTER JOIN  -- 'LEFT JOIN'만 사용해도 좋다
  TABLE_B B
ON 
  A.COL_Z_A = B.COL_Z_B         
```

<br />

#### (2) RIGHT OUTER 조인 문법

```SQL
-- RIGHT OUTER JOIN
SELECT
  A.COL_A1, A.COL_A2, ...,
  B.COL_B1, B.COL_B2, ...
FROM 
  TABLE_A A
RIGHT OUTER JOIN  -- 'RIGHT JOIN'만 사용해도 좋다
  TABLE_B B
ON 
  A.COL_Z_A = B.COL_Z_B         
```

<br />

### 4-3. OUTER 조인 실습

<img src="/images/S-SQL-Join-1/image-20201111141327969.png" alt="image-20201111141327969" style="zoom: 70%;" />

<br />

**\>> LEFT OUTER JOIN**

**(1) LEFT ONLY + LEFT&RIGHT**

<img src="/images/S-SQL-Join-1/image-20201111144634389.png" alt="image-20201111144634389" style="zoom:50%;" />

```SQL
SELECT
  A.ID    ID_A, 
  A.FRUIT FRUIT_A,
  B.ID    ID_B, 
  B.FRUIT FRUIT_B
FROM
  BASKET_A A
LEFT OUTER JOIN 
  BASKET_B B
ON
  A.FRUIT = B.FRUIT  
```

<img src="/images/S-SQL-Join-1/image-20201111141611545.png" alt="image-20201111141611545" style="zoom:80%;" />

<br />

**(2) LEFT ONLY**

<img src="/images/S-SQL-Join-1/image-20201111144750586.png" alt="image-20201111144750586" style="zoom:50%;" />

```SQL
SELECT
  A.ID    ID_A, 
  A.FRUIT FRUIT_A,
  B.ID    ID_B, 
  B.FRUIT FRUIT_B
FROM
  BASKET_A A
LEFT OUTER JOIN 
  BASKET_B B
ON
  A.FRUIT = B.FRUIT  
WHERE B.ID IS NULL
```

<img src="/images/S-SQL-Join-1/image-20201111145103252.png" alt="image-20201111145103252" style="zoom:80%;" />



<br />

**\>> RIGHT OUTER JOIN**

**(1) RIGHT ONLY + LEFT&RIGHT**

<img src="/images/S-SQL-Join-1/image-20201111151323862.png" alt="image-20201111151323862" style="zoom:50%;" />

```SQL
SELECT
  A.ID ID_A, 
  A.FRUIT FRUIT_A,
  B.ID ID_B,
  B.FRUIT FRUIT_B
FROM
  BASKET_A A
RIGHT JOIN
  BASKET_B B
ON A.FRUIT = B.FRUIT
```

<img src="/images/S-SQL-Join-1/image-20201111151622024.png" alt="image-20201111151622024" style="zoom:80%;" />

<br />

**(2) RIGHT ONLY**

<img src="/images/S-SQL-Join-1/image-20201111151416027.png" alt="image-20201111151416027" style="zoom:50%;" />

<br />

```SQL
SELECT
  A.ID ID_A, 
  A.FRUIT FRUIT_A,
  B.ID ID_B,
  B.FRUIT FRUIT_B
FROM
  BASKET_A A
RIGHT JOIN
  BASKET_B B
ON A.FRUIT = B.FRUIT
WHERE A.ID IS NULL
```

<img src="/images/S-SQL-Join-1/image-20201111151747625.png" alt="image-20201111151747625" style="zoom:80%;" />

<br />

<br />


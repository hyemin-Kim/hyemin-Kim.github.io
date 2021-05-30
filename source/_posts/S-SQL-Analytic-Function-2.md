---
title: SQL >> 분석 함수 (2)
tags:
  - SQL
  - Analytic Function
categories:
  - 【STUDY - SQL】
  - SQL - 5. Analytic Function
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: '분석 함수 -- FIRST_VALUE, LAST_VALUE 함수; LAG, LEAD 함수'
typora-root-url: ..
abbrlink: 25367
date: 2020-11-18 08:57:17
---

# 분석 함수 (2) 

@[toc]

<br />

## **1. FIRST_VALUE, LAST_VALUE 함수**

### 1-1. 개념

FIRST_VALUE, LAST_VALUE 함수는 특정 집합 내에서 결과 건수의 변화 없이 해당 집합안에서 **특정 컬럼의 첫번째 값 혹은 마지막 값을 구하는 함수**이다.

<br />

### 1-2. FIRST_NAME 함수 실습

```SQL
SELECT * FROM PRODUCT_GROUP;
```

<img src="/images/S-SQL-Analytic-Function-2/image-20201117095413411.png" alt="image-20201117095413411" style="zoom:80%;" />

<br />

```SQL
SELECT * FROM PRODUCT;
```

<img src="/images/S-SQL-Analytic-Function-2/image-20201117095502521.png" alt="image-20201117095502521" style="zoom:80%;" />

<br />

**\>> MISSION:** GROUP_NAME 기준 PRICE가 가장 작은 값을 출력한다.

```SQL
SELECT
  A.PRODUCT_NAME,
  B.GROUP_NAME,
  A.PRICE,
  FIRST_VALUE (A.PRICE) OVER (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE)
    AS LOWEST_PRICE_PER_GROUP
FROM
  PRODUCT A
INNER JOIN 
  PRODUCT_GROUP B
ON A.GROUP_ID = B.GROUP_ID;
```

<img src="/images/S-SQL-Analytic-Function-2/image-20201117160221397.png" alt="image-20201117160221397" style="zoom:80%;" />

<br />

### 1-3. LAST_VALUE 함수 실습

LAST_VALUE 함수 사용 시 추가적으로 LAST_VALUE를 선택하는 범위를 지정해줘야 함.

<br />

**\>> MISSION:** GROUP_NAME 기준 PRICE가 가장 큰 값을 출력한다.

```SQL
SELECT
  A.PRODUCT_NAME,
  B.GROUP_NAME,
  A.PRICE,
  LAST_VALUE (A.PRICE) OVER 
    (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE
     RANGE BETWEEN UNBOUNDED PRECEDING   -- PARTITION의 첫번째 ROW부터
     AND UNBOUNDED FOLLOWING)            -- PARTITION의 마지막 ROW까지
     AS HIGHEST_PRICE_PER_GROUP
FROM
  PRODUCT A
INNER JOIN 
  PRODUCT_GROUP B
ON A.GROUP_ID = B.GROUP_ID;
```

<img src="/images/S-SQL-Analytic-Function-2/image-20201117162007699.png" alt="image-20201117162007699" style="zoom:80%;" />

<br />

* LAST_VALUE 함수에는 "RANGE BETWEEN ENBOUNDED PRECEDING AND **UNBOUNDED FOLLOWING**"를 추가함
* DEFAULT가 "RANGE BETWEEN ENBOUNDED PRECEDING AND **CURRENT ROW**"이기 때문이다

<br />

```SQL
-- DEFAULT 경우:
SELECT
  A.PRODUCT_NAME,
  B.GROUP_NAME,
  A.PRICE,
  LAST_VALUE (A.PRICE) OVER 
    (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE)            
    AS HIGHEST_PRICE_PER_GROUP
FROM
  PRODUCT A
INNER JOIN 
  PRODUCT_GROUP B
ON A.GROUP_ID = B.GROUP_ID;
```

<img src="/images/S-SQL-Analytic-Function-2/image-20201117162655768.png" alt="image-20201117162655768" style="zoom:80%;" />

<br />

* 범위 지정은 DEFAULT로 **CURRENT ROW** 까지여서 우리가 기대하는 바와 달리 PRICE 값 그대로 출력함.

<br />

<br />

## **2. LAG, LEAD 함수**

### 2-1. 개념

LAG 와 LEAD 함수는 특정 집합 내에서 결과 건수의 변화 없이 해당 집합안에서 **특정 컬럼의 이전 행의 값 혹은 다음 행의 값을 구하는 함수**이다.

<br />

### 2-2. LAG 함수 실습 -- 이전 행의 값을 찾는다

```SQL
SELECT * FROM PRODUCT_GROUP;
```

<img src="/images/S-SQL-Analytic-Function-2/image-20201117095413411.png" alt="image-20201117095413411" style="zoom:80%;" />

<br />

```SQL
SELECT * FROM PRODUCT;
```

<img src="/images/S-SQL-Analytic-Function-2/image-20201117095502521.png" alt="image-20201117095502521" style="zoom:80%;" />

<br />

```SQL
SELECT
  A.PRODUCT_NAME,
  B.GROUP_NAME,
  A.PRICE,
  LAG(A.PRICE, 1) OVER (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE) AS PREV_PRICE,
  PRICE - LAG(A.PRICE, 1) OVER (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE) AS CUR_PREV_DIFF
FROM
  PRODUCT A
INNER JOIN
  PRODUCT_GROUP B
ON A.GROUP_ID = B.GROUP_ID;
```

<img src="/images/S-SQL-Analytic-Function-2/image-20201117170809941.png" alt="image-20201117170809941" style="zoom:80%;" />

<br />

### 2-3. LEAD 함수 실습 -- 다음 행의 값을 찾는다

```SQL
SELECT
  A.PRODUCT_NAME,
  B.GROUP_NAME,
  A.PRICE,
  LEAD(A.PRICE, 1) OVER (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE) AS NEXT_PRICE,
  A.PRICE - LEAD(A.PRICE, 1) OVER (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE) AS CUR_NEXT_DIFF
FROM
  PRODUCT A
INNER JOIN 
  PRODUCT_GROUP B
ON A.GROUP_ID = B.GROUP_ID;
```

<img src="/images/S-SQL-Analytic-Function-2/image-20201117170707029.png" alt="image-20201117170707029" style="zoom:80%;" />

<br />

<br />
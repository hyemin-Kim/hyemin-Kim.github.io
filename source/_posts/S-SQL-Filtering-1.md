---
title: SQL >> 데이터 필터링 (1)
tags:
  - SQL
  - Filtering
categories:
  - 【STUDY - SQL】
  - SQL - 2. Data Filtering
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: '데이터 필터링 -- WHERE 절, LIMIT 절, FETCH 절'
typora-root-url: ..
abbrlink: 45718
date: 2020-11-10 14:17:37
---

# 데이터 필터링 (1) 

@[toc]

<br />

## **1. WHERE 절**

### 1-1. 용도

WHERE 절은 집합을 가져올 때 어떤 집합을 가져올 것인지에 대한 **조건을 설정**하는 절이다.

<br />

### 1-2. WHERE 절 문법

```SQL
SELECT
  COLUMN_1,
  COLUMN_2
FROM 
  TABLE_NAME
WHERE
  <조건>     -- 어떤 집합을 가져올지에 대한 조건을 준다
```

<br />

WHERE 절에 사용할 수 있는 연산자:

<div class="center">

| 연산자  | 설명                     |
| :-----: | :----------------------- |
|    =    | 같음                     |
|    >    | ~보다 큰 (초과)          |
|    <    | ~보다 작은 (미만)        |
|   >=    | ~보다 크거나 같은 (이상) |
|   <=    | ~보다 작거나 같은 (이하) |
| <> , != | ~가 아닌                 |
|   AND   | 그리고                   |
|   OR    | 혹은                     |

</div>

<br />

### 1-3. WHERE 절 실습

#### 1) 조건 한개

```SQL
-- CUSTOMER 테이블에서 FIRST_NAME이 'Jamie'인 행의 FIRST_NAME & LAST_NAME 출력

SELECT
  FIRST_NAME,
  LAST_NAME
FROM
  CUSTOMER
WHERE
  FIRST_NAME = 'Jamie'
```

**[주의]** 문자열은 꼭 **작은 따옴표( ' ' )로 묶어**야 한다. 큰 따옴표( " " )는 안됨



![image-20201107151221142](/images/S-SQL-Filtering-1/image-20201107151221142.png)

<br />

#### 2) 조건 두개

```sql
-- CUSTOMER 테이블에서 FIRST-NAME이 'Jamie'이면서 LAST_NAME이 'Rice'인 행을 출력

SELECT 
  LAST_NAME,
  FIRST_NAME
FROM 
  CUSTOMER
WHERE
     FIRST_NAME = 'Jamie'
 AND LAST_NAME = 'Rice'
```



![image-20201107151533774](/images/S-SQL-Filtering-1/image-20201107151533774.png)

<br />

```SQL
-- PAYMENT 테이블에서 AMOUNT가 1이하이거나 8이상인 행을 출력

SELECT
  CUSTOMER_ID,
  AMOUNT,
  PAYMENT_DATE
FROM
  PAYMENT
WHERE
	AMOUNT <= 1
 OR AMOUNT >= 8
```

<img src="/images/S-SQL-Filtering-1/image-20201107152434964.png" alt="image-20201107152434964" style="zoom:80%;" />

<br />

<br />

## **2. LIMIT 절**

### 2-1. 용도

LIMIT 절은 특정 집합을 출력 시 출력하는 행의 수를 한정하는 역할을 한다. 부분 법위 처리시 사용된다. 

PostgreSQL, MySQL 등에서 지원한다.

<br />

### 2-2. LIMIT 절 문법

```SQL
-- 출력하는 행의 수를 지정한다
SELECT
  * 
FROM
  TABLE_NAME
LIMIT N       -- 상위 N 행만 출력
```

<br />

```SQL
-- 출력하는 행의 수를 지정하면서 시작위치를 지정한다
SELECT
  *
FROM 
  TABLE_NAME
LIMIT N OFFSET M  -- M번째 뒤부터 출력
```

<br />

### 2-3. LIMIT 절 실습

**\>> TABLE**


|                             film                             |
| :----------------------------------------------------------: |
| *film_id <br/>title <br/>discription <br/>release_year <br/>language_id <br/>rentall_duration <br/>rental_rate <br/>length <br/>replacement_cost <br/>rating <br/>last_update <br/>special_features <br/>fulltext |




<br />

**>> LIMIT**

```SQL
-- FILM_NO [1]번 부터 5건 데이터 출력
SELECT
  FILM_ID,
  TITLE,
  RELEASE_YEAR
FROM
  FILM
ORDER BY FILM_ID
LIMIT 5
```

<img src="/images/S-SQL-Filtering-1/image-20201109113053651.png" alt="image-20201109113053651" style="zoom:80%;" />

<br />

<br />

```SQL
-- RENTAL_RATE 내림차순으로 정렬 후 상위 10개 출력
SELECT
  FILM_ID,
  TITLE,
  RENTAL_RATE
FROM
  FILM
ORDER BY
  RENTAL_RATE DESC
LIMIT 10
```

<img src="/images/S-SQL-Filtering-1/image-20201109124207207.png" alt="image-20201109124207207" style="zoom:80%;" />



<br />

**\>> LIMIT + OFFSET**

```SQL
-- FILM_ID [4]번 부터 4건 데이터 출력
SELECT 
  FILM_ID,
  TITLE,
  RELEASE_YEAR
FROM
  FILM
ORDER BY FILM_ID
LIMIT 4
OFFSET 3
```



<img src="/images/S-SQL-Filtering-1/image-20201109113620070.png" alt="image-20201109113620070" style="zoom:80%;" />

<br />

<br />

## **3. FETCH 절**

### 3-1. 용도

FETCH 절은 LIMIT 절과 동일하게, 특정 집합을 출력 시 출력하는 행의 수를 한정하는 역할을 한다. 부분 법위 처리시 사용된다. 

<br />

### 3-2. FETCH 절 문법

```SQL
-- 출력하는 행의 수를 지정한다
SELECT
  *
FROM
  TABEL_NAME
FETCH FIRST [N] ROW ONLY  -- N을 입력하지 않고 ROW ONLY만 입력하면 단 한 건만 출력한다.
```

<br />

```SQL
-- 출력하는 행의 수를 지정하면서 시작위치를 지정한다
SELECT
  * 
FROM
  TABLE_NAME
OFFSET M ROWS
FETCH FIRST [N] ROW ONLY
```

<br />

### 3-3. FETCH 절 실습

**\>> FETCH**

```SQL
-- TITLE로 정렬한 집합 중에서 최초의 단 한 건의 행을 출력
SELECT
  FILM_ID, 
  TITLE
FROM 
  FILM
ORDER BY TITLE
FETCH FIRST ROW ONLY
```



![image-20201109183743426](/images/S-SQL-Filtering-1/image-20201109183743426-1604987080769.png)

<br />

```SQL
-- TITLE로 정렬한 집합 중에서 최초의 10 건의 행을 출력
SELECT
  FILM_ID, 
  TITLE
FROM 
  FILM
ORDER BY TITLE
FETCH FIRST 10 ROW ONLY
```

<img src="/images/S-SQL-Filtering-1/image-20201109184236321.png" alt="image-20201109184236321" style="zoom:80%;" />

<br />

**\>> FETCH + OFFSET**

```SQL
-- TITLE로 정렬한 집합 중에서 6번째 행부터 5건 출력
SELECT
  FILM_ID,
  TITLE
FROM 
  FILM
ORDER BY TITLE
OFFSET 5 ROWS
FETCH FIRST 5 ROWS ONLY
```

<img src="/images/S-SQL-Filtering-1/image-20201109184624570.png" alt="image-20201109184624570" style="zoom:80%;" />

<br />

<br />


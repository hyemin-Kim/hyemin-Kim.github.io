---
title: SQL >> 집계 함수 (2) -- 고급 집계 함수
tags:
  - SQL
  - Aggregate
categories:
  - 【STUDY - SQL】
  - SQL - 4. Aggregate Function
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: '고급 집계 함수 -- GROUPING SET 절, ROLL UP 절, CUBE 절'
typora-root-url: ..
abbrlink: 38485
date: 2020-11-17 08:46:08
---

# 집계 함수 (2) -- 고급 집계 함수

@[toc]

<br />

## **1. GROUPING SET 절**

### 1-0. 학습 준비 (데이터 생성)

```SQL
CREATE TABLE SALES
(
  BRAND VARCHAR NOT NULL,
  SEGMENT VARCHAR NOT NULL,
  QUANTITY INT NOT NULL,
  PRIMARY KEY (BRAND, SEGMENT)
);

INSERT INTO SALES (BRAND, SEGMENT, QUANTITY)
VALUES
  ('ABC', 'Premium', 100),
  ('ABC', 'Basic', 200),
  ('XYZ', 'Premium', 100),
  ('XYZ', 'Basic', 300);
  
COMMIT;
```

```SQL
SELECT * FROM SALES;
```

<img src="/images/S-SQL-Aggregate-2/image-20201113092929823-1605753863307.png" alt="image-20201113092929823" style="zoom:80%;" />

<br />

<br />

### 1-1. GROUP BY 절 활용

#### (1) 2개 컬럼 GROUP BY 절

**[MISSION 1]**  BRAND별, SEGMENT별 총 판패량 구하기

```SQL
SELECT
  BRAND,
  SEGMENT,
  SUM(QUANTITY)
FROM 
  SALES
GROUP BY
  BRAND, 
  SEGMENT;
```

<img src="/images/S-SQL-Aggregate-2/image-20201113093816617-1605753863308.png" alt="image-20201113093816617" style="zoom:80%;" />

<br />

#### (2) 1개 컬럼 GROUP BY 절

**[MISSION 2]**  BRAND별 총 판매량 구하기

```SQL
SELECT
  BRAND,
  SUM(QUANTITY)
FROM
  SALES
GROUP BY 
  BRAND;
```

![image-20201113094753809](/images/S-SQL-Aggregate-2/image-20201113094753809-1605753863308.png)

<br />

**[MISSION 3]**  SEGMENT별 총 판매량 구하기

```SQL
SELECT
  SEGMENT,
  SUM(QUANTITY)
FROM
  SALES
GROUP BY
  SEGMENT;
```

![image-20201113095022421](/images/S-SQL-Aggregate-2/image-20201113095022421-1605753863308.png)

<br />

#### (3) GROUP BY 안하기

**[MISSION 4]**  판매량 전체 합계 구하기

```SQL
SELECT
  SUM(QUANTITY)
FROM 
  SALES;
```

![image-20201113095401699](/images/S-SQL-Aggregate-2/image-20201113095401699-1605753863308.png)

<br />

#### (4) 추출된 정보 합치기 -- UNION ALL의 활용

```SQL
SELECT             -- BRAND별, SEGMENT별 총 판패량
  BRAND,
  SEGMENT,
  SUM(QUANTITY)
FROM SALES
GROUP BY BRAND, SEGMENT
UNION ALL
SELECT             -- BRAND별 총 판패량
  BRAND,
  NULL,
  SUM(QUANTITY)
FROM SALES
GROUP BY BRAND
UNION ALL
SELECT             -- SEGMENT별 총 판패량
  NULL,
  SEGMENT,
  SUM(QUANTITY)
FROM SALES
GROUP BY SEGMENT
UNION ALL
SELECT             -- 전체 총 판패량
  NULL,
  NULL,
  SUM(QUANTITY)
FROM 
  SALES;
```

**[주의]**  각각의 UNION query는 같은 수의 columns를 가져야 한다. 따라서 각 부분의 SELECT 절에서 컬럼수가 부족하면 NULL로 채워야 함.



<img src="/images/S-SQL-Aggregate-2/image-20201113100352802-1605753863308.png" alt="image-20201113100352802" style="zoom:80%;" />

<br />

**이 방법의 단점:**

* 동일한 테이블을 4번씩이나 읽고 있다. --> 성능 저하 가능성이 존재
* SQL 문이 너무 길어진다. -->  복잡하다 --> 유지보수가 용이하지 않다

<br />

**\>>** 이런 불편함을 줄이기 위해서 GROUPING SET 절을 활용한다.

<br />

### 1-2. GROUPING SET 절 활용

#### 1-2-1. 용도

GROUPING SET 절을 사용하여 여러 개의 UNION ALL을 이용한 SQL과 같은 결과를 도출할 수 있다.

<br />

#### 1-2-2. GROUPING SET 절 문법

GROUPING SET 절을 이용하면 한번에 다양한 기준의 컬럼 조합으로 집계를 구할 수 있다.

```SQL
SELECT
  C1,
  C2,
  집계함수(C3)
FROM
  TABLE_NAME
GROUP BY
GROUPING SETS
(
  (C1, C2),
  (C1),
  (C2),
  ()
);
```

<br />

#### 1-2-3. GROUPING SET 절 실습

**>> GROUPING SET 절의 활용**

GROUPING SET 절을 이용하여 BRAND, SEGMENT 기준, BRAND 기준, SEGMENT 기준, 전체기준으로 QUANTITY 합계의 값을 구할 수 있다.

```SQL
SELECT * FROM SALES;
```

<img src="/images/S-SQL-Aggregate-2/image-20201113092929823-1605753863307.png" alt="image-20201113092929823" style="zoom:80%;" />

<br />

```SQL
SELECT
  BRAND,
  SEGMENT,
  SUM(QUANTITY)
FROM
  SALES
GROUP BY
GROUPING SETS
(
  (BRAND, SEGMENT),
  (BRAND),
  (SEGMENT),
  ()
);
```

<img src="/images/S-SQL-Aggregate-2/image-20201113104247913-1605753863308.png" alt="image-20201113104247913" style="zoom:80%;" />

<br />

**\>> GROUPING 함수의 활용**

GROUPING 함수를 이용하여 해당 컬럼이 GROUPING 시 사용되었으면 0, 그렇지 않으면 1을 리턴한다.

```SQL
SELECT * FROM SALES;
```

<img src="/images/S-SQL-Aggregate-2/image-20201113092929823-1605753863307.png" alt="image-20201113092929823" style="zoom:80%;" />

<br />

```SQL
SELECT 
  GROUPING(BRAND) AS GROUPING_BRAND,
  GROUPING(SEGMENT) AS GROUPING_SEGMENT,
  BRAND,
  SEGMENT,
  SUM(QUANTITY)
FROM
  SALES
GROUP BY
GROUPING SETS
(
  (BRAND, SEGMENT),
  (BRAND),
  (SEGMENT),
  ()
)
ORDER BY
  BRAND, SEGMENT;
```

<img src="/images/S-SQL-Aggregate-2/image-20201113111058889-1605753863309.png" alt="image-20201113111058889" style="zoom:80%;" />

<br />

```SQL
SELECT
  CASE WHEN GROUPING(BRAND) = 0 AND GROUPING(SEGMENT) = 0 THEN '브랜드별 + 등급별'
       WHEN GROUPING(BRAND) = 0 AND GROUPING(SEGMENT) = 1 THEN '브랜드별'
       WHEN GROUPING(BRAND) = 1 AND GROUPING(SEGMENT) = 0 THEN '등급별'
       WHEN GROUPING(BRAND) = 1 AND GROUPING(SEGMENT) = 1 THEN '전체합계'
       ELSE ''
       END AS "집계기준",
  BRAND,
  SEGMENT,
  SUM(QUANTITY)
FROM
  SALES
GROUP BY
GROUPING SETS
(
  (BRAND, SEGMENT),
  (BRAND),
  (SEGMENT),
  ()
)
ORDER BY BRAND, SEGMENT;
```

<img src="/images/S-SQL-Aggregate-2/image-20201113112514952-1605753863309.png" alt="image-20201113112514952" style="zoom:80%;" />

<br />

<br />

## **2. ROLL UP 절**

### 2-1. 용도

지정된 GROUPING 컬럼의 소계를 생성하는데 사용된다. 간단한 문법으로 다양한 소계를 출력할 수 있다.

<br />

### 2-2. ROLLUP 절 문법

* ROLLUP 절은 GROUP BY 절과 함계 사용된다. 

* ROLLUP 할 컬럼은 무조건 SELECT 절에 포함되어 있어야 한다.

* ROLLUP 절 컬럼의 **지정 순서가 의미 있다**.

  <br />

#### (1) 전체 ROLL UP

* 컬럼의 지정 순서가 **의미 있음**

```SQL
-- 전체 ROLL UP
SELECT
  C1, C2, C3,
  집계함수(C4)
FROM
  TABLE_NAME
GROUP BY
  ROLLUP(C1, C2, C3);  -- 소계를 생성할 컬럼을 지정한다.
                       -- 컬럼 지정 순서에 따라 결과값이 달라질 수 있다. 
```

<img src="/images/S-SQL-Aggregate-2/image-20201119102055273.png" alt="image-20201119102055273" style="zoom: 80%;" />

<br />

#### (2) 부분 ROLL UP

* 특정 컬럼만 분리하여 ROLL UP 할 수 있다

* 이런 경우에 분리된 특정 컬럼(C1)으로 시작하는 GROUPING SET 만 해당

* 즉, 전체 ROLL UP과 달리, GROUPING 하지 않는 전체 합계를 구하지 않는다.


```SQL
-- 부분 ROLL UP
SELECT
  C1, C2, C3,
  집계함수(C4)
FROM
  TABLE_NAME
GROUP BY C1
  ROLLUP(C2, C3)       -- 특정 컬럼을 제외한 부분적인 ROLLUP도 가능하다.
```

<img src="/images/S-SQL-Aggregate-2/image-20201119102820691.png" alt="image-20201119102820691" style="zoom:80%;" />

<br />

### 2-3. ROLLUP 절 실습

```SQL
SELECT * FROM SALES;
```

<img src="/images/S-SQL-Aggregate-2/image-20201113092929823-1605753863307.png" alt="image-20201113092929823" style="zoom:80%;" />

<br />

#### (1) GROUP BY만 사용 (ROLL UP 안함)

```SQL
-- BRAND, SEGMENT 컬럼 기준으로 GROUP BY 한다.
SELECT
  BRAND,
  SEGMENT,
  SUM(QUANTITY)
FROM
  SALES
GROUP BY
  BRAND, SEGMENT
ORDER BY
  BRAND, SEGMENT;
```

<img src="/images/S-SQL-Aggregate-2/image-20201116101725139-1605753863309.png" alt="image-20201116101725139" style="zoom:80%;" />

<br />

#### (2) GROUP BY + 전체 ROLL UP

```SQL
-- BRAND, SEGMENT 컬럼 기준으로 ROLL UP 한다.
SELECT
  BRAND,
  SEGMENT,
  SUM(QUANTITY)
FROM
  SALES
GROUP BY
  ROLLUP (BRAND, SEGMENT)
ORDER BY
  BRAND, SEGMENT;
```

<img src="/images/S-SQL-Aggregate-2/image-20201116094755070-1605753863309.png" alt="image-20201116094755070" style="zoom:80%;" />

<br />

* 전체 컬럼 ROLLUP 결과:
  * BRAND + SEGMENT 별 합계 --> *GROUP BY (BRAND, SEGMENT) 결과* 
  * BRAND 별 합계 (소계)  --> *GROUP BY + ROLL UP 절의 첫번째 컬럼*
  * 전체 합계 (총계)

<br />

#### (3) GROUP BY + 부분 ROLL UP

```SQL
-- SEGMENT 컬럼 기준으로 GROUP BY 한다 + BRAND 컬럼 기준으로 부분 ROLL UP 한다
SELECT
  SEGMENT,
  BRAND,
  SUM(QUANTITY)
FROM
  SALES
GROUP BY SEGMENT,
  ROLLUP (BRAND)
ORDER BY
  SEGMENT, BRAND
```

<img src="/images/S-SQL-Aggregate-2/image-20201116105618971-1605753863309.png" alt="image-20201116105618971" style="zoom:80%;" />

<br />

* 부분 컬럼 ROLLUP 결과:
  * SEGMENT, BRAND 별 합계 --> *GROUP BY (SEGMENT, BRAND) 결과* 
  * SEGMENT 별 합계 (소계)  --> *ROLLUP 절에서 제외된 특정 컬럼*

<br />

   **\>> **전체 합계 (총계)를 구하지 않는다

<br />

<br />

## **3. CUBE 절**

### 3-1. 용도

지정된 GROUPING 컬럼의 다차원 소계를 생성하는데 사용된다. 간단한 문법으로 다차원 소계를 출력할 수 있다.

<br />

### 3-2. CUBE 절 문법

* CUBE절은 GROUP BY 절과 함계 사용된다. 

* CUBE 할 컬럼은 무조건 SELECT 절에 포함되어 있어야 한다.

* CUBE절 컬럼의 **지정 순서가 의미 없다**

  <br />

#### (1) 전체 컬럼 CUBE 지정

* 컬럼의 지정 순서가 **의미 없음**
* 지정한 그룹의 **모든 경우의 수** 에 대한 소계와 총계를 구한다

 ```SQL
SELECT 
  C1, C2, C3,
  집계함수(C4)
FROM 
  TABLE_NAME
GROUP BY
  CUBE (C1, C2, C3);
 ```

<br />

CUBE 절 내 인자의 개수가 N개이면 2의 N승의 소계가 발생하게 된다.

CUBE (C1, C2, C3)를 GROUPING SETS으로 표현하면 총 9개의 소계가 발생한다.

<img src="/images/S-SQL-Aggregate-2/image-20201116140935710-1605753863309.png" alt="image-20201116140935710" style="zoom: 67%;" />

<br />

#### (2) 부분 컬럼 CUBE 지정

* 특정 컬럼만 분리하여 CUBE 를 지정할 수 있다

* 이런 경우에 분리된 특정 컬럼(C1)으로 시작하는 GROUPING SET 만 해당

```SQL
SELECT
  C1, C2, C3,
  집계함수(C4)
FROM
  TABLE_NAME
GROUP BY C1,
  CUBE (C2, C3);
```

<img src="/images/S-SQL-Aggregate-2/image-20201119105210943.png" alt="image-20201119105210943" style="zoom:80%;" />

<br />


### 3-3. CUBE 절 실습

```SQL
SELECT * FROM SALES;
```

<img src="/images/S-SQL-Aggregate-2/image-20201113092929823-1605753863307.png" alt="image-20201113092929823" style="zoom:80%;" />

<br />

#### (1) 전체 컬럼 CUBE 지정

```SQL
-- BRAND, SEGMENT 컬럼 기준으로 CUBE 한다.
SELECT
  BRAND, 
  SEGMENT,
  SUM(QUANTITY)
FROM SALES
GROUP BY
  CUBE (BRAND, SEGMENT)
ORDER BY
  BRAND, SEGMENT;
```

<br />

<img src="/images/S-SQL-Aggregate-2/image-20201116142724305-1605753863311.png" alt="image-20201116142724305" style="zoom:80%;" />

<br />

* 전체 컬럼 CUBE 결과:
  * BRAND + SEGMENT 별 합계 --> *GROUP BY (BRAND, SEGMENT) 결과* 
  * BRAND 별 합계 (소계)
  * SEGMENT 별 합계 (소계)
  * 전체 합계 (총계)

<br />

   **\>>** 인자가 2개 이므로 총 4개의 경우의 수가 합계로 출력된다



<br />

#### (2) 부분 컬럼 CUBE 지정

```SQL
-- BRAND 컬럼 기준으로 GROUP BY 한다 + SEGMENT 컬럼 기준으로 부분 CUBE 한다
SELECT
  BRAND,
  SEGMENT,
  SUM(QUANTITY)
FROM
  SALES
GROUP BY BRAND,
  CUBE (SEGMENT)
ORDER BY
  BRAND, SEGMENT
```

<img src="/images/S-SQL-Aggregate-2/image-20201116144806788-1605753863311.png" alt="image-20201116144806788" style="zoom:80%;" />

 <br />

* 부분 컬럼 CUBE 결과:

  * BRAND + SEGMENT 별 합계 --> *GROUP BY (BRAND, SEGMENT) 결과*

  * BRAND 별 합계 (소계)  --> *CUBE 절에서 제외된 특정 컬럼*

    <br />

   **\>>**  SEGMENT 별 합계 (소계)를 구하지 않는다.

   **\>> ** 전체 합계 (총계)를 구하지 않는다.

<br />

<br />
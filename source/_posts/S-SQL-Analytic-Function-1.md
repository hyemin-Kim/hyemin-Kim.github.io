---
title: 'SQL >> 분석 함수 (1) -- 평균 함수, 순위 함수'
tags:
  - SQL
  - Analytic Function
categories:
  - 【STUDY - SQL】
  - SQL - 5. Analytic Function
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: '분석 함수 -- 평균 함수(AVG), 순위 함수 (ROW_NUMBER, RANK, DENSE_RANK)'
typora-root-url: ..
abbrlink: 59330
date: 2020-11-18 08:47:11
---

# 분석 함수 (1) -- 평균 함수, 순위 함수

@[toc]

<br />

## **0. 분석 함수란?**

### 0-1. 개념

분석 함수는 특정 집합 내에서 결과 건수의 변화없이 해당 집합안에서 합계 및 카운트 등을 계산할 수 있는 함수이다.

<br />

### 0-2. 분석 함수 실습 준비

```SQL
CREATE TABLE PRODUCT_GROUP (
  GROUP_ID SERIAL PRIMARY KEY,
  GROUP_NAME VARCHAR (255) NOT NULL
);

CREATE TABLE PRODUCT (
  PRODUCT_ID SERIAL PRIMARY KEY,
  PRODUCT_NAME VARCHAR (255) NOT NULL,
  PRICE DECIMAL (11, 2),   -- DECIMAL (전체 자릿수, 소수점 자릿수)
  GROUP_ID INT NOT NULL,
  FOREIGN KEY (GROUP_ID)
  REFERENCES PRODUCT_GROUP (GROUP_ID)
);
```

 ```SQL
INSERT INTO PRODUCT_GROUP (GROUP_NAME)
VALUES
  ('Smartphone'),
  ('Laptop'),
  ('Tablet');
  
COMMIT;

INSERT INTO PRODUCT (PRODUCT_NAME, GROUP_ID, PRICE)
VALUES
  ('Microsoft Lumia', 1, 200),
  ('HTC One', 1, 400),
  ('Nexus', 1, 500),
  ('iPhone', 1, 900),
  ('HP Elite', 2, 1200),
  ('Lenovo Thinkpad', 2, 700),
  ('Sony VAIO', 2, 700),
  ('Dell Vostro', 2, 800),
  ('iPad', 3, 700),
  ('Kindle Fire', 3, 150),
  ('Samsung Galaxy Tab', 3, 200);
  
COMMIT;
 ```

<br />

```SQL
SELECT * FROM PRODUCT_GROUP;
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117095413411.png" alt="image-20201117095413411" style="zoom:80%;" />

<br />

```SQL
SELECT * FROM PRODUCT;
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117095502521.png" alt="image-20201117095502521" style="zoom:80%;" />

<br />

### 0-3. 분석 함수 문법

```SQL
SELECT
  C1,
  분석함수(C2, C3, ...) OVER (PARTITION BY C4 ORDER BY C5)
FROM 
  TABLE_NAME;
```

* **분석함수(C2, C3,...) :** 사용하고자 하는 분석함수와 적용할 대상 컬럼을 지정
* **PARTITION BY :** 분석 함수를 적용 시 기준이 되는 컬럼을 지정 (즉, 그룹별로 값을 구할 때 그룹핑의 기준 컬럼)
* **ORDER BY :** 정렬 컬럼을 지정

<br />

### 0-4. 분석 함수 결과 예시

집계 함수 vs 분석 함수:

* 집계 함수는 집계의 결과만 출력한다

* 분석 함수는 집계의 결과 및 테이블의 내용을 함계 출력한다. 

  --> 이게 바로 분석 함수의 역할이다.

<br />

```sql
-- 집계 함수
SELECT
 COUNT(*)
FROM 
  PRODUCT
```

![image-20201117101439406](/images/S-SQL-Analytic-Function-1/image-20201117101439406.png)

<br />

```SQL
-- 분석 함수
SELECT
  COUNT(*) OVER(),  -- 집계 결과 
  A.*               -- 원래 집합
FROM
  PRODUCT A
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117101622478.png" alt="image-20201117101622478" style="zoom:80%;" />

<br />

<br />

## **1. AVG 함수**

### 1-1. 개념

AVG 함수는 특정 집합 내에서 결과 건수의 변화 없이 해당 집합안에서 **특정 컬럼의 평균을 구하는 함수**이다.

<br />

### 1-2. AVG 함수 실습

```SQL
SELECT * FROM PRODUCT_GROUP;
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117095413411.png" alt="image-20201117095413411" style="zoom:80%;" />

<br />

```SQL
SELECT * FROM PRODUCT;
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117095502521.png" alt="image-20201117095502521" style="zoom:80%;" />

<br />

#### (1) 전체  평균 가격(PRICE) 구하기

**\>> 집계함수 사용**

* AVG: 집계의 결과만 출력

  ```SQL
  -- 집계 함수(AVG): 집계의 결과만 출력
  SELECT
  AVG(PRICE)
  FROM
  PRODUCT;
  ```

![image-20201117130450587](/images/S-SQL-Analytic-Function-1/image-20201117130450587.png)

<br />

**\>> 분석함수 사용**

* AVG ( )  OVER ( ) : 결과 집합을 그대로 출력하면서 집계 결과도 함계 출력

  ```SQL
  -- 분석 함수
  SELECT 
    PRODUCT_NAME,
    PRICE,
    AVG(PRICE) OVER()
  FROM 
    PRODUCT;
  ```

  <img src="/images/S-SQL-Analytic-Function-1/image-20201117133842813.png" alt="image-20201117133842813" style="zoom:80%;" />

  <br />



#### (2) 그룹별 평균 가격(PRICE) 구하기

**\>> 집계함수 사용**

* GROUP BY + AVG:  집계의 결과만 출력

  ```SQL
  -- 집계 함수: GROUP BY + AVG
  SELECT
  B.GROUP_NAME,
  AVG(A.PRICE)
  FROM PRODUCT A
  INNER JOIN PRODUCT_GROUP B
  ON (A.GROUP_ID = B.GROUP_ID)
  GROUP BY
  B.GROUP_NAME;
  ```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117131044658.png" alt="image-20201117131044658" style="zoom:80%;" />

<br />

**\>> 분석함수 사용**

* AVG (C1)  OVER ( PARTITION BY C2 ) : 결과 집합을 그대로 출력하면서 집계 결과도 함계 출력

  ```SQL
  -- 분석 함수
  SELECT
  A.PRODUCT_NAME,
  A.PRICE, 
  B.GROUP_NAME,
  AVG(A.PRICE) OVER (PARTITION BY B.GROUP_NAME)
  FROM
  PRODUCT A
  INNER JOIN 
  PRODUCT_GROUP B
  ON A.GROUP_ID = B.GROUP_ID;
  ```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117132959087.png" alt="image-20201117132959087" style="zoom:80%;" />

<br />

#### (3) 그룹별 누적 평균 가격(PRICE) 구하기

**\>> 분석함수 사용**

* AVG (C1)  OVER ( PARTITION BY C2  ORDER BY C3 )

  ```SQL
  SELECT
    A.PRODUCT_NAME,
    A.PRICE,
    B.GROUP_NAME,
    AVG(A.PRICE) OVER (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE)
  FROM
    PRODUCT A
  INNER JOIN 
    PRODUCT_GROUP B
  ON A.GROUP_ID = B.GROUP_ID;
  ```

  <img src="/images/S-SQL-Analytic-Function-1/image-20201117134939361.png" alt="image-20201117134939361" style="zoom:80%;" />

<br />

<br />

## **2. ROW_NUMBER, RANK, DENSE_RANK 함수**

### 2-1.  개념

ROW_NUMBER, RANK, DENSE_RANK 함수는 모두 특정 집합 내에서 결과 건수의 변화 없이 해당 집합안에서 **특정 컬럼의 순위를 구하는 함수**이다. 

* **ROW_NUMBER:** 같은 순위가 있어도 무조건 순차적으로 순으로 순위를 매긴다. (1, 2, 3, 4, 5 ...)

* **RANK:** 같은 순위가 있으면 동일 순위로 매기고 그 다음 순위를 건너뛰다. (1, 1, 3, 4, 5 ...)

* **DENSE_RANK:** 같은 순위가 있으면 동일 순위로 매기고 그 다음 순위를 건너뛰지 않는다. (1, 1, 2, 3, 4 ...)

  <br />

### 2-2. 순위 함수 실습

```SQL
SELECT * FROM PRODUCT_GROUP;
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117095413411.png" alt="image-20201117095413411" style="zoom:80%;" />

<br />

```SQL
SELECT * FROM PRODUCT;
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117095502521.png" alt="image-20201117095502521" style="zoom:80%;" />

<br />

#### 2-2-1. ROW_NUMBER 함수 실습

**ROW_NUMBER:** 같은 순위가 있어도 무조건 순차적으로 순으로 순위를 매긴다. (1, 2, 3, 4, 5...)

```SQL
SELECT
  A.PRODUCT_NAME,
  B.GROUP_NAME,
  A.PRICE,
  ROW_NUMBER() OVER (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE)
FROM 
  PRODUCT A
INNER JOIN 
  PRODUCT_GROUP B
ON A.GROUP_ID = B.GROUP_ID;
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117142626970.png" alt="image-20201117142626970" style="zoom:80%;" />

<br />

* Laptop 에서 가격순으로 정렬했을 때 "Sony VAIO"와 "Lenovo Thinkpad"의 가격이 동일해도 (즉, 가격 순위 같아도)  순차적으로 순번을 부여한다

<br />

#### 2-2-2. RANK 함수 실습

**RANK:** 같은 순위가 있으면 동일 순위로 매기고 그 다음 순위는 건너뛰다. (1, 1, 3, 4, 5 ...)

```SQL
SELECT
  A.PRODUCT_NAME,
  B.GROUP_NAME,
  A.PRICE,
  RANK() OVER (PARTITION BY B.GROUP_NAME ORDER BY A.PRICE)
FROM 
  PRODUCT A
INNER JOIN 
  PRODUCT_GROUP B
ON A.GROUP_ID = B.GROUP_ID;
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117150134038.png" alt="image-20201117150134038" style="zoom:80%;" />

<br />

#### 2-2-3. DENSE_RANK 함수 실습

**DENSE_RANK:** 같은 순위가 있으면 동일 순위로 매기고 그 다음 순위를 건너뛰지 않는다. (1, 1, 2, 3, 4 ...)

```SQL
SELECT
  PRODUCT_NAME,
  GROUP_NAME,
  PRICE,
  DENSE_RANK() OVER (PARTITION BY GROUP_NAME ORDER BY PRICE)
FROM
  PRODUCT A
INNER JOIN 
  PRODUCT_GROUP B
ON 
  A.GROUP_ID = B.GROUP_ID;
```

<img src="/images/S-SQL-Analytic-Function-1/image-20201117151955026.png" alt="image-20201117151955026" style="zoom:80%;" />

<br />

<br />
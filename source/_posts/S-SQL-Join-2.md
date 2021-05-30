---
title: SQL >> 조인 (2)
tags:
  - SQL
  - Join
categories:
  - 【STUDY - SQL】
  - SQL - 3. Join
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: 'SELF 조인, FULL OUTER 조인, CROSS 조인, NATURAL 조인'
typora-root-url: ..
abbrlink: 54781
date: 2020-11-12 15:21:33
---

# **조인 (2)**

@[toc]

<br />

## **1. SELF 조인**

### 1-1. 개념

SELF 조인은 같은 테이블 끼리 특정 컬럼을 기준으로 매칭 되는 컬럼을 출력하는 조인이다.  

즉, 같은 테이블의 데이터를 각각의 집합으로 분류한 후  조인한다.

<br />

### 1-2. SELF 조인 문법

```SQL
SELECT
  A.COL_1, A.COL_2, ...,
  B.COL_1, B.COL_3, ...
FROM 
  TABLE_NAME AS A
INNER JOIN
  TABLE_NAME AS B    -- THE SAME TABLE WITH THE FORMER
ON A.COL_T = B.COL_T
```

<br />

### 1-3. SELF 조인 실습

#### 1-3-1. 실습 준비

```SQL
CREATE TABLE EMPLOYEE
(
    EMPLOYEE_ID INT PRIMARY KEY,
    FIRST_NAME VARCHAR(255) NOT NULL,
    LAST_NAME VARCHAR(255) NOT NULL,
    MANAGER_ID INT,
    FOREIGN KEY (MANAGER_ID)               -- MANAGER_ID는 같은 테이블 (EMPLOYEE)의 EMPLOYEE_ID를 참조함
    REFERENCES EMPLOYEE (EMPLOYEE_ID)
    ON DELETE CASCADE
);
```

```SQL
INSERT INTO EMPLOYEE (
    EMPLOTEE_ID,
    FIRST_NAME,
    LAST_NAME,
    MANAGER_ID
)
VALUES
(1, 'Windy', 'Hays', NULL),
(2, 'Ava', 'Christensen', 1),
(3, 'Hassan', 'Conner', 1),
(4, 'Anna', 'Reeves', 2),
(5, 'Sau', 'Norman', 2),
(6, 'Kelsie', 'Hays', 3),
(7, 'Tory', 'Goff', 3),
(8, 'Salley', 'Lester', 3);

COMMIT;
```

<br />

```SQL
SELECT * FROM EMPLOYEE
```

<img src="/images/S-SQL-Join-2/image-20201111155046250.png" alt="image-20201111155046250" style="zoom:80%;" />

<br />

**\>> 조직도**

<img src="/images/S-SQL-Join-2/image-20201111155421168.png" alt="image-20201111155421168" style="zoom: 67%;" />

<br />

#### 1-3-2. SELF 조인 실습

**\>> SELF INNER 조인 실습**

**MISSION:** 

* 각 직원의 상위 관리자를 출력 
* 최고관리자인 'Windy Hays'는 결과 집합에 포함시키지 않음.

<br />

```SQL
SELECT 
  E.FIRST_NAME || ' ' || E.LAST_NAME AS EMPLOYEE,
  M.FIRST_NAME || ' ' || M.LAST_NAME AS MANAGER
FROM
  EMPLOYEE E  -- EMPLOYEE 중심
INNER JOIN
  EMPLOYEE M  -- MANAGER 중심
ON 
  E.MANAGER_ID = M.EMPLOYEE_ID   -- 매칭 시 헷갈리지 않도록 주의
ORDER BY
  MANAGER
```

<img src="/images/S-SQL-Join-2/image-20201111162640186.png" alt="image-20201111162640186" style="zoom:80%;" />



<br />

**\>> SELF LEFT OUTER 조인 실습**

**MISSION:** 

* 각 직원의 상위 관리자를 출력하면서 모든 직원을 출력
* 최고관리자인 'Windy Hays'가 결과 집합에 포함시킴

<br />

```SQL
SELECT
  E.FIRST_NAME || ' ' || E.LAST_NAME AS EMPLOYEE,
  M.FIRST_NAME || ' ' || M.LAST_NAME AS MANAGER
FROM 
  EMPLOYEE E
LEFT OUTER JOIN
  EMPLOYEE M
ON 
  E.MANAGER_ID = M.EMPLOYEE_ID
ORDER BY
  MANAGER
```

<img src="/images/S-SQL-Join-2/image-20201111163954892.png" alt="image-20201111163954892" style="zoom:80%;" />

<br />

**\>> 부정형 조건 실습**

**MISSION:** FILM 테이블에서 영화의 상영시간이 동일한 서로 다른 영화의 리스트를 출력

|                             film                             |
| :----------------------------------------------------------: |
| *film_id <br/>title <br/>discription <br/>release_year <br/>language_id <br/>rentall_duration <br/>rental_rate <br/>length <br/>replacement_cost <br/>rating <br/>last_update <br/>special_features <br/>fulltext |

<br />

```SQL
SELECT
  A.TITLE,
  B.TITLE,
  A.LENGTH
FROM 
  FILM A
INNER JOIN
  FILM B
ON A.FILM_ID != B.FILM_ID AND
   A.LENGTH = B.LENGTH
```

<img src="/images/S-SQL-Join-2/image-20201111183444264.png" alt="image-20201111183444264" style="zoom:80%;" />

<br />

<br />

## **2. FULL OUTER 조인**

### 2-1. 개념

FULL OUTER 조인은 INNER, LEFT OUTER, RIGHT OUTER 조인 집합을 모두 출력하는 조인 방식이다.  

즉, 두 테이블간 출력가능한 모든 데이터를 포함한 집합을 출력한다.

<img src="/images/S-SQL-Join-2/image-20201111192014271.png" alt="image-20201111192014271" style="zoom:50%;" />

<br />

### 2-2. FULL OUTER 조인 문법

```SQL
SELECT
  A.COL_A1, A.COL_A2, ...,
  B.COL_B1, B.COL_B2, ...
FROM 
  TABLE_A A
FULL OUTER JOIN  
  TABLE_B B
ON 
  A.COL_Z_A = B.COL_Z_B 
```

<br />

### 2-3. FULL OUTER 조인 실습

#### 2-3-1. BASKET 데이터를 활용한 간단한 실습

<img src="/images/S-SQL-Join-2/image-20201111141327969.png" alt="image-20201111141327969" style="zoom: 67%;" />

<br />

**\>> FULL OUTER JOIN**

**(1) LEFT ONLY + LEFT&RIGHT + RIGHT ONLY**

<img src="/images/S-SQL-Join-2/image-20201111193914893.png" alt="image-20201111193914893" style="zoom:50%;" />

```SQL
SELECT 
  A.ID ID_A,
  A.FRUIT FRUIT_A,
  B.ID ID_B,
  B.FRUIT FRUIT_B
FROM
  BASKET_A A
FULL OUTER JOIN
  BASKET_B B
ON 
  A.FRUIT = B.FRUIT
```

<img src="/images/S-SQL-Join-2/image-20201111193119708.png" alt="image-20201111193119708" style="zoom:80%;" />

<br />

**(2) ONLY OUTER (LEFT ONLY + RIGHT ONLY)**

<img src="/images/S-SQL-Join-2/image-20201111194125768.png" alt="image-20201111194125768" style="zoom:50%;" />

```SQL
SELECT 
  A.ID ID_A,
  A.FRUIT FRUIT_A,
  B.ID ID_B,
  B.FRUIT FRUIT_B
FROM
  BASKET_A A
FULL OUTER JOIN
  BASKET_B B
ON 
  A.FRUIT = B.FRUIT 
WHERE A.ID IS NULL    -- LEFT OUTER
   OR B.ID IS NULL    -- RIGHT OUTER
```

<img src="/images/S-SQL-Join-2/image-20201111194613680.png" alt="image-20201111194613680" style="zoom:80%;" />

<br />

#### 2-3-2. 추가 실습

**\>> 실습 준비**

```SQL
CREATE TABLE
IF NOT EXISTS DEPARTMENTS    -- 종재하지 않으면 생성
(
  DEPARTMENT_ID SERIAL PRIMARY KEY,
  DEPARTMENT_NAME VARCHAR (255) NOT NULL
);

CREATE TABLE
IF NOT EXISTS EMPLOYEES
(
  EMPLOYEE_ID SERIAL PRIMARY KEY,
  EMPLOYEE_NAME VARCHAR (255),
  DEPARTMENT_ID INTEGER
);
```

```SQL
INSERT INTO DEPARTMENTS(DEPARTMENT_NAME)
VALUES
('Sales'),
('Marketing'),
('HR'),
('IT'),
('Production');

COMMIT;

INSERT INTO EMPLOYEES(
  EMPLOYEE_NAME,
  DEPARTMENT_ID
)
VALUES
('Bette Nicholson', 1),
('Christian Gable', 1),
('Joe Swank', 2),
('Fred Costner', 3),
('Sandra Kilmer', 4),
('Julia Mcqueen', NULL);

COMMIT;
```

<br />

```SQL
SELECT * FROM DEPARTMENTS;
```

<img src="/images/S-SQL-Join-2/image-20201111200237831.png" alt="image-20201111200237831" style="zoom:80%;" />



```SQL
SELECT * FROM EMPLOYEES;
```

<img src="/images/S-SQL-Join-2/image-20201111200326518.png" alt="image-20201111200326518" style="zoom:80%;" />

<br />

**\>> FULL OUTER JOIN 실습**

```SQL
SELECT
  E.EMPLOYEE_NAME,
  D.DEPARTMENT_NAME
FROM 
  EMPLOYEES E
FULL OUTER JOIN
  DEPARTMENTS D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
```

<img src="/images/S-SQL-Join-2/image-20201111201327463.png" alt="image-20201111201327463" style="zoom:80%;" />



<br />

**\>> RIGHT OUTER ONLY 실습**

<img src="/images/S-SQL-Join-2/image-20201111202627226.png" alt="image-20201111202627226" style="zoom:50%;" />

```SQL
-- 소속한 직원이 없는 부서만 출력
-- FULL OUTER + RIGHT ONLY
SELECT
  E.EMPLOYEE_NAME,
  D.DEPARTMENT_NAME
FROM 
  EMPLOYEES E
FULL OUTER JOIN
  DEPARTMENTS D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
WHERE E.EMPLOYEE_NAME IS NULL
```

<img src="/images/S-SQL-Join-2/image-20201111202501663.png" alt="image-20201111202501663"  />

<br />

**[P.S.]** FULL OUTER JOIN+ RIGHT ONLY = RIGHT OUTER JOIN+ RIGHT ONLY

```SQL
-- RIGHT OUTER + RIGHT ONLY
SELECT
  E.EMPLOYEE_NAME,
  D.DEPARTMENT_NAME
FROM 
  EMPLOYEES E
RIGHT OUTER JOIN 
  DEPARTMENTS D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
WHERE E.EMPLOYEE_NAME IS NULL
```

![image-20201111202503508](/images/S-SQL-Join-2/image-20201111202503508.png)



<br />

**\>> LEFT OUTER ONLY 실습**

<img src="/images/S-SQL-Join-2/image-20201111202802778.png" alt="image-20201111202802778" style="zoom: 50%;" />

```SQL
-- 소속한 부서가 없는 직원만 출력
-- FULL OUTER + LEFT ONLY
SELECT
  E.EMPLOYEE_NAME,
  D.DEPARTMENT_NAME
FROM 
  EMPLOYEES E
FULL OUTER JOIN
  DEPARTMENTS D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
WHERE D.DEPARTMENT_NAME IS NULL
```

![image-20201111203302334](/images/S-SQL-Join-2/image-20201111203302334.png)

<br />

**[P.S.]** FULL OUTER JOIN+ LEFT ONLY = LEFT OUTER JOIN+ LEFT ONLY

```SQL
-- LEFT OUTER + LEFT ONLY
SELECT
  E.EMPLOYEE_NAME,
  D.DEPARTMENT_NAME
FROM 
  EMPLOYEES E
RIGHT OUTER JOIN 
  DEPARTMENTS D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
WHERE D.DEPARTMENT_NAME IS NULL
```

![image-20201111203302334](/images/S-SQL-Join-2/image-20201111203302334.png)

<br />

<br />

## **3. CROSS 조인**

### 3-1. 개념

두 개의 테이블의 CATESIAN PRODUCT 연산의 결과를 출력한다. 데이터 복제에 많이 쓰이는 기법이다.

* CATESIAN  PRODUCT:

  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Cartesian_Product_qtl1.svg/1200px-Cartesian_Product_qtl1.svg.png" alt="CARTESIAN PRODUCT" style="zoom: 25%;" />

<br />

### 3-2. CROSS 조인 문법

```SQL
SELECT
  *
FROM
  CROSS_TABLE_1
CROSS JOIN
  CROSS_TABLE_2
```

<br />

### 3-3. CROSS 조인 실습

#### 3-3-0. 실습 준비

```SQL
CREATE TABLE CROSS_T1
(
  LABEL CHAR(1) PRIMARY KEY
);

CREATE TABLE CROSS_T2
(
  SCORE INT PRIMARY KEY
);
```

```SQL
INSERT INTO CROSS_T1 (LABEL)
VALUES
('A'),
('B');

COMMIT;

INSERT INTO CROSS_T2 (SCORE)
VALUES
(1),
(2),
(3);

COMMIT;
```

<br />

```SQL
SELECT * FROM CROSS_T1
```

![image-20201112090311812](/images/S-SQL-Join-2/image-20201112090311812.png)



```SQL
SELECT * FROM CROSS_T2
```

![image-20201112090405111](/images/S-SQL-Join-2/image-20201112090405111.png)

<br />

#### 3-3-1. CROSS 조인 실습

<img src="/images/S-SQL-Join-2/image-20201112091802546.png" alt="image-20201112091802546" style="zoom: 67%;" />

```SQL
-- 방법 1
SELECT
  *
FROM 
  CROSS_T1
CROSS JOIN
  CROSS_T2
ORDER BY 
  LABEL
```

<img src="/images/S-SQL-Join-2/image-20201112091538328.png" alt="image-20201112091538328" style="zoom:80%;" />

<br />

```SQL
-- 방법 2
SELECT
  * 
FROM 
  CROSS_T1, CROSS_T2   -- INNER JOIN을 표현하는 다른 방법 (조건 없는 INNER JOIN)
ORDER BY 
  LABEL
```

<br />

* 위 두 개의 SQL 문 결과 집합이 동일하므로 같은 SQL문이라고 할 수 있다. SQL문의 목적은 집합을 출력하는 것이 때문이다.   

  즉, 추출한 정보가 같다면 SQL문 자체는 다르더라도 동일한 SQL 문이다.

<br />

<br />

## **4. NATURAL 조인**

### 4-1. 개념

두개의 테이블에서 같은 이름을 가진 컬럼 간의 INNER 조인 집합 결과를 출력한다. SQL문 자체가 간소해지는 방법이다.

<br />

### 4-2. NATURAL 조인 문법

```SQL
SELECT
  *
FROM
  TABLE_A
NATURAL JOIN    -- 자동으로 두 테이블이 동일하게 가지고 있는 컬럼을 기준으로 INNER 조인한다
  TABLE_B
```

* NATURAL 조인은 INNER 조인의 또 다른 SQL 작성 방식이다.

  즉, 조인 컬럼을 명시하지 않아도 된다.

<br />

### 4-3. NATURAL 조인 실습

#### 4-3-0. 실습 준비

```SQL
CREATE TABLE CATEGORIES
(
  CATEGORY_ID SERIAL PRIMARY KEY,
  CATEGORY_NAME VARCHAR (255) NOT NULL
);

CREATE TABLE PRODUCTS
(
  PRODUCT_ID SERIAL PRIMARY KEY,
  PRODUCT_NAME VARCHAR (255) NOT NULL,
  CATEGORY_ID INT NOT NULL,
  FOREIGN KEY (CATEGORY_ID)
  REFERENCES CATEGORIES (CATEGORY_ID)
);
```

```SQL
INSERT INTO CATEGORIES
(CATEGORY_NAME)
VALUES
  ('Smart Phone'),
  ('Laptop'),
  ('Tablet');

COMMIT;

INSERT INTO PRODUCTS
(PRODUCT_NAME, CATEGORY_ID)
VALUES
  ('iPhone', 1),
  ('Samsung Galaxy', 1),
  ('HP Elite', 2),
  ('Lenovo Thinkpad', 2),
  ('iPad', 3),
  ('Kindle Fire', 3);
  
COMMIT;
```

<br />

```SQL
SELECT * FROM CATEGORIES;
```

<img src="/images/S-SQL-Join-2/image-20201112113447690.png" alt="image-20201112113447690" style="zoom:80%;" />



```SQL
SELECT * FROM PRODUCTS;
```

<img src="/images/S-SQL-Join-2/image-20201112113548016.png" alt="image-20201112113548016" style="zoom:80%;" />

<br />

#### 4-3-1. NATURAL 조인 실습

**(1) 예제 데이터를 활용한 간단한 실습**

```SQL
SELECT
  * 
FROM
  PRODUCTS A
NATURAL JOIN
  CATEGORIES B;
```

<img src="/images/S-SQL-Join-2/image-20201112114726576.png" alt="image-20201112114726576" style="zoom:80%;" />

<br />

```SQL
-- 대체 방법 1
-- INNER JOIN으로 실현
SELECT 
  P.CATEGORY_ID,  P.PRODUCT_ID,
  P.PRODUCT_NAME, C.CATEGORY_NAME
FROM 
  PRODUCTS P
INNER JOIN 
  CATEGORIES C
ON P.CATEGORY_ID = C.CATEGORY_ID;
```

<br />

```SQL
-- 대체 방법 2  (INNER JOIN 대체 명령어)
SELECT 
  P.CATEGORY_ID,  P.PRODUCT_ID,
  P.PRODUCT_NAME, C.CATEGORY_NAME
FROM 
  PRODUCTS P,
  CATEGORIES C
WHERE P.CATEGORY_ID = C.CATEGORY_ID;
```

<br />

<img src="/images/S-SQL-Join-2/image-20201112114726576.png" alt="image-20201112114726576" style="zoom:80%;" />

<br />

**(2) "dvdrental" 데이터를 활용한 실습**

**\>> 테이블 구성**

<img src="/images/S-SQL-Join-2/image-20201112135034156.png" alt="image-20201112135034156" style="zoom:80%;" />

<br />

**>> 실습**

두 테이블이 모두 "country_id"  컬럼이 존재한다.  

이 두 테이블에 대해서 NATURAL JOIN을 진행해보면:

```sql
SELECT 
  *
FROM 
  CITY A
NATURAL JOIN
  COUNTRY B;
```

<img src="/images/S-SQL-Join-2/image-20201112135747118.png" alt="image-20201112135747118" style="zoom:80%;" />

<br />

기대와 다르게 출력 결과가 0건이다.

<br />

그 이유는:  

두 테이블 간에 동일한 이름으로 존재하는 컬럼이 COUNTRY_ID 외에 LAST_UPDATE 도 존재한다.  이런 경우 NATURAL JOIN 시에는 **LAST_UPDATE 컬럼까지 INNER조인에 성공해야만** 결과값이 나온다.  하지만 두 테이블의 LAST_UPDATE 값이 서로 다르므로 위 SQL문을 실행 후 조건에 만족하는 결과가 없다. 

<br />

따라서 NATURAL 조인이 아닌 INNER 조인을 이용해야한다.

```SQL
SELECT
  * 
FROM 
  CITY A
INNER JOIN
  COUNTRY B
ON A.COUNTRY_ID = B.COUNTRY_ID;
```

![image-20201112142508575](/images/S-SQL-Join-2/image-20201112142508575.png)

INNER 조인으로 ON절에 조인 컬럼을 명시하였고, 의도한 대로 데이터가 출력되었다.

<br />

```SQL
-- INNER JOIN 대체 명령어
SELECT
  * 
FROM 
  CITY A,
  COUNTRY B
WHERE A.COUNTRY_ID = B.COUNTRY_ID;
```

<br />

이러한 이유로 NATURAL 조인은 실무에 잘 사용되지 않는다.

<br />

<br />
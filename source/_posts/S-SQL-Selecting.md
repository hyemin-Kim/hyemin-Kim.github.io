---
title: SQL >> 데이터 조회
tags:
  - SQL
  - Selecting
categories:
  - 【STUDY - SQL】
  - SQL - 1. Data Selecting
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
description: '데이터 조회 -- SELECT 문, ORDER BY 문, SELECT DISTINCT 문'
typora-root-url: ..
abbrlink: 48406
date: 2020-11-06 14:56:21
---



# 데이터 조회

@[toc]

<br />

## **1. SELECT 문**

### 1-1. 용도

SELECT 문은 일반적으로 테이플에 저장된 데이터를 가져오는 데 쓰인다. 

SQL에서 가장 많이 쓰이는 문장이다.

<br />

### 1-2. SELECT 문법

```SQL
SELECT
  COLUMN_1,
  COLUMN_2,
  중략...
FROM
  TABLE_NAME
```

<br />

### 1-3. SELECT 문 실습

**> 전체 컬럼을 조회**

```SQL
SELECT
  *
FROM
  CUSTOMER
```

![image-20201106151704452](/images/S-SQL-Selecting/image-20201106151704452.png)

<br />

**\> 지정한 컬럼을 조회**

```SQL
SELECT
  FIRST_NAME,
  LAST_NAME,
  EMAIL
FROM
  CUSTOMER
```

![image-20201106151807348](/images/S-SQL-Selecting/image-20201106151807348.png)

**[주의]** 여러 컬럼을 조회할 때, SELECT 명령어 뒤 컬럼 이름을 입력 시:   

- 마지막 컬럼명을 제외한 모든 컬럼명 뒤에 따움표( , )를 붙여야 함
- 마지막 컬럼명 뒤에는 아무것도 입력하지 않는다

<br />

**\> 테이블 Alias(별칭) 활용하기**

테이블에 별칭을 지정하면 코드의 가독성이 높아진다.  특히 테이블이 많아  지면, 선택한 컬럼이 어느 테이블에서 추출한 건지를 햇갈릴 수 있다. 테이블 별칭을 활용하면 보다 쉽게 구별할 수 있다.

```SQL
SELECT
  A.FIRST_NAME,
  A.LAST_NAME,
  A.EMAIL
FROM 
  CUSTOMER A -- OR "CUSTOMER AS A"
```

**[주의]** 테이블 Alias는 현재의 SELECT 문장에 대해서만 유효하다.

<br />

<br />

## **2. ORDER BY 문**

### 2-1. 용도

ORDER BY 문은 SELECT 문에서 가져온 데이터를 정렬하는 데 사용한다. 

업무 처리상 매우 중요한 기능이다.

<br />

### 2-2. ORDER BY 문법

ORDER BY를 활용하면 가져온 데이터를 특정 컬럼을 기준으로 오름차순(ASC) 혹은 내림차순(DESC)으로 정렬할 수 있다. 

* 컬럼명 뒤에 ```ASC```를 불이면 -- 오름차순으로 정렬

* 컬럼명 뒤에 ```DESC```를 불이면 -- 내림차순으로 정렬
* 컬럼명 뒤에 아무것도 안 불이면 -- Default로 오름차순으로 정렬

```sql
SELECT
  COLUMN_1,
  COLUMN_2
FROM
  TAL_NAME
ORDER BY   -- Default: 오름차순(ASC)
  COLUMN_1 ASC,    -- 오름차순 정렬
  COLUMN_2 DESC   -- 내림차순 정렬
```

<br />

### 2-3. ORDER BY 문 실습

#### 1) 단일 기준 정렬

단일 컬럼을 기준으로 한 번의 정렬만 실시함.

<br />

**> ASC(오름차순) 정렬**

* ORDER BY 미사용 시 (미정렬)

  ```sql
  SELECT
    FIRST_NAME,
    LAST_NAME
  FROM
    CUSTOMER
  ```

  <img src="/images/S-SQL-Selecting/image-20201106152037841.png" alt="image-20201106152037841" style="zoom:80%;" />

  <br />

* "FIRST_NAME" 기준으로 오름차순 정렬

  ```SQL
  -- ASC 명령어 명시
  SELECT
    FIRST_NAME,
    LAST_NAME
  FROM
    CUSTOMER
  ORDER BY
    FIRST_NAME ASC
  ```

  ```SQL
  -- Default로 정렬
  SELECT
    FIRST_NAME,
    LAST_NAME
  FROM
    CUSTOMER
  ORDER BY
    FIRST_NAME
  ```

  <img src="/images/S-SQL-Selecting/image-20201106152244978.png" alt="image-20201106152244978" style="zoom:80%;" />



<br />

**\> DESC(내림차순) 정렬 **

* "FIRST_NAME"기준으로 내림차순 정렬

  ```SQL
  SELECT
    FIRST_NAME,
    LAST_NAME
  FROM
    CUSTOMER
  ORDER BY
    FIRST_NAME DESC
  ```

  <img src="/images/S-SQL-Selecting/image-20201106152323551.png" alt="image-20201106152323551" style="zoom:80%;" />

<br />

<br />

#### 2) 다중 기준 N차 정렬

여러 컬럼을 기준으로 N차 정렬을 실시함.

* COLUMN_1 기준으로 1차 정렬한 다음,

* COLUMN_1의 값이 동일한 데이터에 대해서 COLUMN_2 기준으로 2차 정렬을 실시한다,

* (위 규칙대로 계속 실행)...

<br />

**\> ASC(오름차순) + DESC(내림차순) 정렬**

* 먼저 FIRST_NAME 오름차순으로 정렬, FIRST_NAME이 동일한 데이터는 LAST_NAME 내림차순으로 정렬

  ```SQL
  SELECT
    FIRST_NAME,
    LAST_NAME
  FROM
    CUSTOMER
  ORDER BY
    FIRST_NAME DESC,  -- 1차 정렬 (FIRST_NAME 내림차순)
    LAST_NAME ASC  -- 2차 정렬 (LAST_NAME 오름차순)
  ```

  <img src="/images/S-SQL-Selecting/image-20201106152444007.png" alt="image-20201106152444007" style="zoom:80%;" />

<br />

* ORDER BY 기준을 정할 때, 컬럼명 내신에 SELECT 시 컬럼이 들어오는 순서로 대체해도 된다. (하지만 가독성을 위해 위 방법 더 추천)

  ```SQL
  SELECT
    FIRST_NAME,
    LAST_NAME
  FROM
    CUSTOMER
  ORDER BY
    1 DESC,  -- 1: FIRST_NAME (내림차순)
    2 ASC    -- 2: LAST_NAME (오름차순)
  ```

<br />

<br />


## **3. SELECT DISTINCT 문**

### 3-1. 용도

SELECT 시 DISTINCT를 사용하면 중복 값을 제외한 결과값이 출력된다. 즉 같은 결과의 행이라면 중복을 제거할 수 있다. 

<br />

### 3-2. SELECT DISTINCT 문법

#### 1) 단일 컬럼

* **단일 컬럼**을 추출할 때 **해당 컬럼의 값이 중복된 행을 제거**하여 추출

  ```SQL
  -- COLUMN_1의 값이 중복 값 존재 시 중복 값을 제거
  SELECT
    DISTINCT COLUMN_1
  FROM TABLE_NAME
  ```

<br />

#### 2) 다중 컬럼

* **다중 컬럼**을 추출할 때 **<font color = 'red'>모든 컬럼의 값이 모두 중복 된 행</font>을 제거**하여 추출

  ```SQL
  -- COLUMN_1 + COLUMN_2의 값이 중복 값 존재 시 중복 값을 제거 
  SELECT
    DISTINCT COLUMN_1, COLUMN_2
  FROM
    TABLE_NAME
  ```

  <br />

  \>> 중복 값 제거 후 정렬하여 추출

  ```SQL
  -- 결과를 명확하게 하기 위해 ORDER BY 절 사용
  SELECT
    DISTINCT COLUMN_1, COLUMN_2
  FROM 
    TABLE_NAME
  ORDER BY
    COLUMN_1,   -- default로 오름차순 정렬
    COLUMN_2    -- default로 오름차순 정렬
  ```

<br />


* **다중 컬럼**을 추출할 때 **<font color = 'red'>특정 컬럼의 값을 기준으로</font> 중복된 행을 제거**하여 추출 (DISTINCT ON 절)

  **[제거 규칙]**  기준 컬럼의 값이 동일한 행 중에서 하나의 행만 보류  

  ​                         \- 기본적으로 중복된 행 중의 첫 번째를 보류 

  ​                         \- ORDER BY 문을 사용할 경우 정렬 후의 첫 번째 행을 보류

  ```SQL
  SELECT 
    DISTINCT ON (COLUMN_1)
                 COLUMN_1, COLUMN_2
  FROM 
    TABLE_NAME
  ```

  ```SQL
  SELECT 
    DISTINCT ON (COLUMN_1)
                 COLUMN_1, COLUMN_2
  FROM 
    TABLE_NAME
  ORDER BY 
    COLUMN_1 
    COLUMN_2
  ```

<br />

<br />

### 3-3.  SELECT DISTINCT 문 실습

#### 0) 실습 준비 (데이터 생성)

```SQL
CREATE TABLE T1 (ID SERIAL NOT NULL PRIMARY KEY, BCOLOR VARCHAR, FCOLOR VARCHAR);
INSERT
  INTO T1(BCOLOR, FCOLOR)
VALUES
  ('red', 'red'),
  ('red', 'red'),
  ('red', NULL),
  (NULL, 'red'),
  ('red', 'green'),
  ('red', 'blue'),
  ('green', 'red'),
  ('green', 'blue'),
  ('green', 'green'),
  ('blue', 'red'),
  ('blue', 'green'),
  ('blue', 'blue')
; 
```

```sql
SELECT
  *
FROM 
  T1
```

<img src="/images/S-SQL-Selecting/image-20201106152615942.png" alt="image-20201106152615942" style="zoom:80%;" />

<br />

#### 1) 단일 컬럼 

* BCOLOR 컬럼의 값이 중복된 행을 제거 + BCOLOR 기준으로 정렬하여 추출

  ```SQL
  SELECT
    DISTINCT BCOLOR
  FROM 
    T1
  ORDER BY 
    BCOLOR
  ```


​                                                               ![image-20201106152737312](/images/S-SQL-Selecting/image-20201106152737312.png)

<br />

#### 2) 다중 컬럼

* BCOLOR & FCOLOR 두 컬럼을 추출 시:

  1.  **두 컬럼 의 값이 <font color='red'>모두 중복된 행</font>을 제거**

  2.  BCOLOR & FCOLOR 기준으로 **정렬하여 추출**

  ```SQL
  SELECT
    DISTINCT BCOLOR, 
             FCOLOR
  FROM 
    T1
  ORDER BY
    BCOLOR,
    FCOLOR
  ```


​                                            <img src="/images/S-SQL-Selecting/image-20201106160613919.png" alt="image-20201106160613919" style="zoom:80%;" />

<br />

* BCOLOR & FCOLOR 두 컬럼을 추출 시:

  1.  **<font color='red'>BCOLOR의  값</font>을 기준으로 <font color='red'>중복된 행</font>을 제거**

  2.  * 미정렬 시 BCOLOR값이 동일한 행 중에 첫 번째 행만 보류

      * BCOLOR, FCOLOR 기준으로 정렬 시 FCOLOR의 첫 번째 값을 가진 행만 보류

  ```SQL
  -- 미정렬 시
  SELECT
    DISTINCT ON (BCOLOR)
                 BCOLOR, FCOLOR
  FROM
    T1
  ```

  ​                                     <img src="/images/S-SQL-Selecting/image-20201106160706340.png" alt="image-20201106160706340" style="zoom:80%;" />

  <br />

  ```SQL
  -- BCOLOR, FCOLOR 기준으로 정렬  (FCOLOR 오름차순)
  SELECT
    DISTINCT ON (BCOLOR)
                 BCOLOR, FCOLOR
  FROM 
    T1
  ORDER BY
    BCOLOR, 
    FCOLOR
  ```

  ​                                     <img src="/images/S-SQL-Selecting/image-20201106160800896.png" alt="image-20201106160800896" style="zoom:80%;" /> 

  <br />

  ```SQL
  -- BCOLOR, FCOLOR 기준으로 정렬  (FCOLOR 내림차순)
  SELECT
    DISTINCT ON (BCOLOR)
                 BCOLOR, FCOLOR
  FROM 
    T1
  ORDER BY
    BCOLOR, 
    FCOLOR DESC
  ```

  ​                                     <img src="/images/S-SQL-Selecting/image-20201106160853425.png" alt="image-20201106160853425" style="zoom:80%;" />

<br />

<br />
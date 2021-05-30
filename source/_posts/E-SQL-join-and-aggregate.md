---
title: 【실습】 SQL >> 조인과 집계 데이터
tags:
  - SQL
  - Join
  - Aggregate
categories:
  - 【EXERCISE】
  - SQL
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
typora-root-url: ..
abbrlink: 2640
date: 2020-11-19 15:44:46
---

# 【실습】 조인과 집계 데이터

<br />

#### **[1] RENTAL 테이블을 이용하여 연, 연월, 연월일, 전체 각각의 기준으로 RENTAL_ID 기준 렌탈이 일어난 횟수를 출력하라. (전체 데이터 기준으로 모든 행을 출력)**

<br />

<img src="/images/E-SQL-join-and-aggregate/image-20201119085019530.png" alt="image-20201119085019530" style="zoom: 67%;" />

<br />

<br />

**\>> 문제 풀이**

```SQL
SELECT * FROM RENTAL;
```

<img src="/images/E-SQL-join-and-aggregate/image-20201119085317448.png" alt="image-20201119085317448" style="zoom:80%;" />

<br />

```SQL
SELECT
  TO_CHAR(RENTAL_DATE, 'YYYY'),
  TO_CHAR(RENTAL_DATE, 'MM'),
  TO_CHAR(RENTAL_DATE, 'DD'),
  COUNT (RENTAL_ID)
FROM
  RENTAL
GROUP BY
  ROLLUP (TO_CHAR(RENTAL_DATE, 'YYYY'),
          TO_CHAR(RENTAL_DATE, 'MM'),
  		  TO_CHAR(RENTAL_DATE, 'DD'));
```

<img src="/images/E-SQL-join-and-aggregate/image-20201119130425101.png" alt="image-20201119130425101" style="zoom:67%;" />

<img src="/images/E-SQL-join-and-aggregate/image-20201119130531222.png" alt="image-20201119130531222" style="zoom:67%;" />

<br />

<br />

### [2] RENTAL과 CUSTOMER 테이블을 이용하여 현재까지 가장 많이 RENTAL을 한 고객의 고객ID, 렌탈순위, 누적렌탈횟수, 이름을 출력하라.

<br />

<img src="/images/E-SQL-join-and-aggregate/image-20201119131041452.png" alt="image-20201119131041452" style="zoom:67%;" />

<br />

<br />

**\>> 문제 풀이**

**(1) 가장 먼저 RENTAL 순위를 구해야 한다.**

* 고객 별로 렌탈 횟수 구함
* ROW_NUMBER() 를 이용해 순위 번호 생성 (렌탈 횟수를 내림차순으로 정렬한 후 생성)

```SQL
SELECT 
  CUSTOMER_ID,
  ROW_NUMBER() OVER(ORDER BY COUNT(RENTAL_ID) DESC) AS RENTAL_RANK,
  COUNT(RENTAL_ID) AS RENTAL_COUNT
FROM
  RANTAL
GROUP BY 
  CUSTOMER_ID;
  
-- CUSTOMER_ID 기준으로 GROUP BY 했기 때문에 ROW_NUMBER()에서 PARTITION BY가 생략되었다.
```

<img src="/images/E-SQL-join-and-aggregate/image-20201119143530660.png" alt="image-20201119143530660" style="zoom:80%;" />

<br />

<br />

**(2) 이 상태에서 첫번째 순위인 데이처를 추출 (가장 많이 RENTAL 한 고객의 데이터)**

* ORDER BY + LIMIT 이용

```SQL
SELECT 
  CUSTOMER_ID,
  ROW_NUMBER() OVER(ORDER BY COUNT(RENTAL_ID) DESC) AS RENTAL_RANK,
  COUNT(RENTAL_ID) AS RENTAL_COUNT
FROM
  RENTAL
GROUP BY 
  CUSTOMER_ID
ORDER BY 
  RENTAL_COUNT DESC
LIMIT 1;
```

<img src="/images/E-SQL-join-and-aggregate/image-20201119144824759.png" alt="image-20201119144824759"  />

<br />

<br />

**(3) 마지막으로 CUSTOMER 테이블과 조인하여 해당 고객의 이름을 출력한다**

1. 직접 조인

   * CUSTOMER_ID 기준으로 GROUP BY 되어 있으므로 FIRST_NAME, LAST_NAME에 MAX함수를 사용해서 출력한다.

   ```SQL
   SELECT 
    A.CUSTOMER_ID,
    ROW_NUMBER() OVER(ORDER BY COUNT(A.RENTAL_ID) DESC) AS RENTAL_RANK,
    COUNT(A.RENTAL_ID) AS RENTAL_COUNT,
    MAX(B.FIRST_NAME) AS FIRST_NAME,
    MAX(B.LAST_NAME) AS LAST_NAME
   FROM
    RENTAL A, CUSTOMER B
   WHERE 
    A.CUSTOMER_ID = B.CUSTOMER_ID
   GROUP BY 
    A.CUSTOMER_ID
   ORDER BY 
    RENTAL_COUNT DESC
   LIMIT 1;
   ```

   ![image-20201119144959120](/images/E-SQL-join-and-aggregate/image-20201119144959120.png)

<br />

2. 서브커리 활용

   ```SQL
   SELECT
     B.CUSTOMER_ID,
     B.RENTAL_RANK,
     B.RENTAL_COUNT,
     C.FIRST_NAME,
     C.LAST_NAME
   FROM
   (
   SELECT 
     A.CUSTOMER_ID,
     ROW_NUMBER() OVER(ORDER BY COUNT(A.RENTAL_ID) DESC) AS RENTAL_RANK,
     COUNT(A.RENTAL_ID) AS RENTAL_COUNT
   FROM RENTAL A
   GROUP BY
     CUSTOMER_ID
   ORDER BY
     RENTAL_COUNT DESC
   LIMIT 1
   ) B, CUSTOMER C
   WHERE B.CUSTOMER_ID = C.CUSTOMER_ID;
   ```

   ![image-20201119144959120](/images/E-SQL-join-and-aggregate/image-20201119144959120.png)

<br />

<br />
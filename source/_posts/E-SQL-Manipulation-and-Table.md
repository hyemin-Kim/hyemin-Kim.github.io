---
title: 【실습】 SQL >> 데이터 조작 및 테이블 관리
tags:
  - SQL
  - Manipulation
  - Table
categories:
  - 【EXERCISE】
  - SQL
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
typora-root-url: ..
abbrlink: 44352
date: 2020-12-22 18:48:12
---

# 【실습】 데이터 조작 및 테이블 관리

<br />

### [1]  DVD렌탈 시스템의 관리자가 고객별 매출 순위를 알고 싶다. 신규 테이블을 생성해서 고객의 매출 순위를 관리하고 싶으며 신규 테이블의 이름은 CUSTOMER_RANK이고 테이블 구성은 CUSTOMER_ID, CUSTOMER_RANK로 정했다. CTAS 기법을 이용하여 신규 테이블을 생성하면서 데이터를 입력해라.

<img src="/images/E-SQL-Manipulation-and-Table/image-20201222171831673.png" alt="image-20201222171831673" style="zoom:80%;" />

<br />

**\>> 문제 풀이**

```SQL
SELECT * FROM PAYMENT LIMIT 10;
```

<img src="/images/E-SQL-Manipulation-and-Table/image-20201222175413890.png" alt="image-20201222175413890" style="zoom:80%;" />

<br />

<br />

1. **우선 고객별 총 매출액을 계산한다**

   ```SQL
     SELECT CUSTOMER_ID,
            SUM(AMOUNT) AS AMOUNT_SUM
       FROM PAYMENT
   GROUP BY CUSTOMER_ID
   ORDER BY AMOUNT_SUM DESC;
   ```

   <img src="/images/E-SQL-Manipulation-and-Table/image-20201222172206108.png" alt="image-20201222172206108" style="zoom:80%;" />

   <br />

   <br />

2. **그 다음 고객 총매출 순위를 매긴다 (내림차순)**

   ```SQL
   SELECT A.CUSTOMER_ID,
          RANK() OVER(ORDER BY A.AMOUNT_SUM DESC) AS CUSTOMER_RANK
     FROM (
             SELECT CUSTOMER_ID,
             		 SUM(AMOUNT) AS AMOUNT_SUM
       	    FROM PAYMENT
           GROUP BY CUSTOMER_ID
           ORDER BY AMOUNT_SUM DESC
          ) A;
   ```

   <img src="/images/E-SQL-Manipulation-and-Table/image-20201222172543446.png" alt="image-20201222172543446" style="zoom:80%;" />

<br />

3. **마지막으로 CTAS 문을 이용하여 CUSTOMER_RANK 테이블 생성하고 데이터를 입력한다.**

   ```SQL
   CREATE TABLE CUSTOMER_RANK (CUSTOMER_ID, CUSTOMER_RANK) AS
   SELECT A.CUSTOMER_ID,
          RANK() OVER(ORDER BY A.AMOUNT_SUM DESC) AS CUSTOMER_RANK
     FROM (
             SELECT CUSTOMER_ID,
             		 SUM(AMOUNT) AS AMOUNT_SUM
       	    FROM PAYMENT
           GROUP BY CUSTOMER_ID
           ORDER BY AMOUNT_SUM DESC
          ) A;
   ```

   ```SQL
   SELECT * FROM CUSTOMER_RANK;
   ```

   <img src="/images/E-SQL-Manipulation-and-Table/image-20201222172543446.png" alt="image-20201222172543446" style="zoom:80%;" />

<br />

<br />

<br />

### [2] DVD렌탈 시스템의 관리자는 매달 마다 매출 순위 1위를 한 고객에게 특별한 선물을 주고자 한다. 이러한 업무를 달성하기 위해서 CUSTOMER_RANK_YYYYMM이라는 테이블을 CTAS 기법으로 생성하는 SQL문을 작성하라. (단 선물 제공 기준을 정하기 위해 고객별 총 매출액도 저장하라)

<img src="/images/E-SQL-Manipulation-and-Table/image-20201222185331599.png" alt="image-20201222185331599" style="zoom:80%;" />

<br />

**\>> 문제 풀이**

```SQL
SELECT * FROM PAYMENT LIMIT 10;
```

<img src="/images/E-SQL-Manipulation-and-Table/image-20201222175413890.png" alt="image-20201222175413890" style="zoom:80%;" />

<br />

<br />

1. **먼저 년월별 고객별 총 매출액을 계산한다**

   ```SQL
     SELECT CUSTOMER_ID,
            TO_CHAR(PAYMENT_DATE, 'YYYYMM') AS YYYYMM,
            SUM(AMOUNT) AS AMOUNT_SUM
       FROM PAYMENT
   GROUP BY TO_CHAR(PAYMENT_DATE, 'YYYYMM'),
            CUSTOMER_ID
   ORDER BY YYYYMM, AMOUNT_SUM DESC;
   ```

   <img src="/images/E-SQL-Manipulation-and-Table/image-20201222184237522.png" alt="image-20201222184237522" style="zoom:80%;" />

<br />

2. **총 매출액 기준으로 년월별 고객 순위를 매긴다**

   ```SQL
   SELECT A.CUSTOMER_ID,
          A.YYYYMM,
          A.AMOUNT_SUM,
          RANK() OVER(PARTITION BY A.YYYYMM ORDER BY AMOUNT_SUM DESC) AS RANK_YYYYMM
     FROM (
   		  SELECT CUSTOMER_ID,
   		         TO_CHAR(PAYMENT_DATE, 'YYYYMM') AS YYYYMM,
   		         SUM(AMOUNT) AS AMOUNT_SUM
   		    FROM PAYMENT
   		GROUP BY TO_CHAR(PAYMENT_DATE, 'YYYYMM'),
   		         CUSTOMER_ID
   		ORDER BY YYYYMM, AMOUNT_SUM DESC 
          ) A;
   ```

   <img src="/images/E-SQL-Manipulation-and-Table/image-20201222184359999.png" alt="image-20201222184359999" style="zoom:80%;" />

<br />

3. **마지막으로 CTAS 문을 이용하여 CUSTOMER_RANK_YYYYMM테이블 생성하고 데이터를 입력한다.**

   ```SQL
   CREATE TABLE CUSTOMER_RANK_YYYYMM AS      
   SELECT A.CUSTOMER_ID,
          A.YYYYMM,
          A.AMOUNT_SUM,
          RANK() OVER(PARTITION BY A.YYYYMM ORDER BY AMOUNT_SUM DESC) AS RANK_YYYYMM
     FROM (
   		  SELECT CUSTOMER_ID,
   		         TO_CHAR(PAYMENT_DATE, 'YYYYMM') AS YYYYMM,
   		         SUM(AMOUNT) AS AMOUNT_SUM
   		    FROM PAYMENT
   		GROUP BY TO_CHAR(PAYMENT_DATE, 'YYYYMM'),
   		         CUSTOMER_ID
   		ORDER BY YYYYMM, AMOUNT_SUM DESC 
          ) A;
   ```

   ```SQL
   SELECT * FORM CUSTOMER_RANK_YYYYMM;
   ```

   <img src="/images/E-SQL-Manipulation-and-Table/image-20201222184557948.png" alt="image-20201222184557948" style="zoom:80%;" />

<br />

<br />


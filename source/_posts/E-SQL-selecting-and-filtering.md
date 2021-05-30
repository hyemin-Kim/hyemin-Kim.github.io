---
title: 【실습】 SQL >> 데이터 조회 및 필터링
tags:
  - SQL
  - Selecting
  - Filtering
categories:
  - 【EXERCISE】
  - SQL
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
typora-root-url: ..
abbrlink: 6842
date: 2020-11-10 21:01:42
---

# 【실습】 데이터 조회 및 필터링

<br />

### **[1] PAYMENT 테이블에서 단일 거래의 AMOUNT의 액수가 가장 많은 고객들의 CUSTOMER_ID를 추출하라. 단, CUSTOMER_ID의 값은 유일해야 한다.**



|                           payment                            |
| :----------------------------------------------------------: |
| \* payment_id <br/>customer_id <br/>staff_id <br/>rental_id <br/>amount <br/>payment_date |

<br />

**\>> 문제 풀이**

1. 우선 전체 거래 중 AMOUNT의 액수가 가장 큰 AMOUNT를 구한다.

   ```SQL
   SELECT AMOUNT
     FROM PAYMENT
   ORDER BY AMOUNT DESC
   LIMIT 1
   ```

   ![](/images/E-SQL-selecting-and-filtering/image-20201110202739100.png)

   <br />

2. 그 다음 PAYMENT 테이블에서 가장 큰 AMOUNT를 가진 CUMSTOMER_ID를 구하고 중복을 제거한다

   ```SQL
   SELECT
     DISTINCT A.CUSTOMER_ID
   FROM PAYMENT A
   WHERE A.AMOUNT = (
            SELECT B.AMOUNT
              FROM PAYMENT B
            ORDER BY B.AMOUNT DESC
       	 LIMIT 1
   )
   ```

   <img src="/images/E-SQL-selecting-and-filtering/image-20201110203211887.png" alt="image-20201110203211887" style="zoom:80%;" />



<br />

<br />

### **[2]  고객들에게 단체 이메일을 전송하고자 한다.  CUSTOMER 테이블에서 고객의 EMAIL 주소를 추출하고, 이메일 형식에 맞지 않은 이메일 주소는 제외시켜라.**  

**(이메일 형식은: '@'가 존재해야 하고; '@'로 시작하지 말아야 하고; '@'로 끝나지 말아야 한다.)**



|                           customer                           |
| :----------------------------------------------------------: |
| \* customer_id <br>store_id <br>first_name <br/>email <br/>address_id <br/>activebool <br/>create_date <br/>last_update <br/>active |

<br />

**\>> 문제 풀이**

```SQL
SELECT EMAIL
  FROM CUSTOMER
WHERE  EMAIL LIKE '%@%'
   AND EMAIL NOT LIKE '@%'
   AND EMAIL NOT LIKE '%@'
```

<img src="/images/E-SQL-selecting-and-filtering/image-20201110205604326.png" alt="image-20201110205604326" style="zoom:80%;" />

<br />

<br />
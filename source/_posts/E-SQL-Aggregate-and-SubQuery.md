---
title: 【실습】 SQL >> 집합 연산자와 서브쿼리
tags:
  - SQL
  - SubQuery
categories:
  - 【EXERCISE】
  - SQL
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
typora-root-url: ..
abbrlink: 10270
date: 2020-12-01 11:19:23
---

# 【실습】 집합 연산자와 서브쿼리

<br />

### **[1] 아래 SQL문은 FILM 테이블을 2번 스캔하고 RENTAL_RATE가 평균 이상인 FILM의 ID, 제목과 RENTAL_RATE를 출력했다. FILM 테이블을 한번만 SCAN하여 동일한 결과 집합을 구하는 SQL을 작성하라.**

<img src="/images/E-SQL-Aggregate-and-SubQuery/image-20201201093133569.png" alt="image-20201201093133569" style="zoom:80%;" />

<br />

<br />

**\>> 두 번 스캔**

```SQL
SELECT
  FILM_ID,
  TITLE,
  RENTAL_RATE
FROM  
  FILM
WHERE 
  RENTAL_RATE >
(
  SELECT
    AVG(RENTAL_RATE)
  FROM FILM
);
```

<img src="/images/E-SQL-Aggregate-and-SubQuery/image-20201201095113118.png" alt="image-20201201095113118" style="zoom:80%;" />

<br />

<br />

**\>> 한 번만 스캔**

**1) 우선 분석함수 AVG를 사용해서 평균을 구한다.**

```SQL
SELECT
  FILM_ID,
  TITLE,
  RENTAL_RATE,
  AVG(RENTAL_RATE) OVER() AS AVG_RENTAL_RATE
FROM
  FILM
```

<img src="/images/E-SQL-Aggregate-and-SubQuery/image-20201201101435553.png" alt="image-20201201101435553" style="zoom:80%;" />

<br />

<br />

**2) 1번에서 구한 집합을 인라인뷰로 감싸서 평균보다 큰 값을 구한다.**

```SQL
SELECT
  FILM_ID, TITLE, RENTAL_RATE
FROM
(
  SELECT
    FILM_ID,
    TITLE,
    RENTAL_RATE,
    AVG(RENTAL_RATE) OVER() AS AVG_RENTAL_RATE
  FROM
    FILM
) A
WHERE A.RENTAL_RATE > A.AVG_RENTAL_RATE; 
```

<img src="/images/E-SQL-Aggregate-and-SubQuery/image-20201201095113118.png" alt="image-20201201095113118" style="zoom:80%;" />

<br />

* 똑같은 결과가 나오는 것을 확인할 수 있다

<br />

<br />

### **[2] 아래 SQL문은 EXCEPT 연산을 사용하여 재고가 없는 영화를 구하고 있다. 해당 SQL문은 EXCEPT연산을 사용하지 말고 같은 결과를 도출하라.**

<img src="/images/E-SQL-Aggregate-and-SubQuery/image-20201201103003214.png" alt="image-20201201103003214" style="zoom:80%;" />

<br />

<br />

**\>> EXCEPT 연산 사용**

```SQL
SELECT
  FILM_ID, TITLE
FROM
  FILM
EXCEPT
SELECT DISTINCT
  INVENTORY.FILM_ID, TITLE
FROM
  INVENTORY
INNER JOIN
  FILM
ON FILM.FILM_ID = INVENTORY.FILM_ID
ORDER BY TITLE;
```

<img src="/images/E-SQL-Aggregate-and-SubQuery/image-20201201105357613.png" alt="image-20201201105357613" style="zoom:80%;" />

<br />

<br />

**\>> NOT EXISTS 연산 사용**

```SQL
SELECT 
  FILM_ID, 
  TITLE
FROM 
  FILM F
WHERE 
NOT EXISTS 
(
  SELECT *
    FROM INVENTORY I
   WHERE F.FILM_ID = I.FILM_ID
);
```

<img src="/images/E-SQL-Aggregate-and-SubQuery/image-20201201105357613.png" alt="image-20201201105357613" style="zoom:80%;" />

<br />

* 똑같은 결과가 나오는 것을 확인할 수 있다

<br />

<br />
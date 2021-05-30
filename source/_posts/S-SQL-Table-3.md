---
title: SQL >> 테이블 관리 (3)
tags:
  - SQL
categories:
  - 【STUDY - SQL】
  - SQL - 9. Table
description: '테이블 제거, 임시 테이블, TRUNCATE'
cover: 'https://s1.ax1x.com/2020/11/06/Bf13kR.png'
typora-root-url: ..
abbrlink: 64441
date: 2020-12-21 18:13:02
---

# 테이블 관리 (3)

@[toc]

<br />

## **1. 테이블 제거**

### 1-1. 개념

존재하는 테이블을 제거할 수 있다. 하지반 테이블 제거 시는 항상 주의해야하고 FK (Foreign Key) 관계도 유의해야 한다.

<br />

### 1-2. 테이블 제거 문법

```SQL
DROP TABLE TABLE_NAME 
```

<br />

### 1-3. 테이블 제거 실습

#### >>  실습 준비

```SQL
CREATE TABLE DIRECTOR
(
  DIRECTOR_ID INT NOT NULL PRIMARY KEY,
  FIRSTNAME VARCHAR (50),
  LASTNAME VARCHAR (50)
);


CREATE TABLE FILMS
(
  FILM_ID SERIAL PRIMARY KEY,
  TITLE VARCHAR (255) NOT NULL,
  PREMIERE_DAY DATE,
  DIRECTOR_ID INT NOT NULL,
  FOREIGN KEY (DIRECTOR_ID) REFERENCES DIRECTOR (DIRECTOR_ID)
);
```

```SQL
INSERT INTO DIRECTOR
VALUES (1, '준호', '봉');

INSERT INTO FILMS
VALUES (1, '기생충', '2019-05-30', 1);

COMMIT;
```

```SQL
SELECT * FROM DIRECTOR;
```

![image-20201218235703439](/images/S-SQL-Table-3/image-20201218235703439.png)

```SQL
SELECT * FROM FILMS;
```

![image-20201218235726706](/images/S-SQL-Table-3/image-20201218235726706.png)

<br />

![image-20201219000405118](/images/S-SQL-Table-3/image-20201219000405118.png)

<br />

<br />

#### >> 테이블 제거 실습

**[MISSION 1]**  부모 테이블 (DIRECTOR 테이블)을 제거하기

> 부모 테이블은 바로 제거할 수 없다. 부모 테이블의 컬럼이 자식 테이블에서 첨조되고 있기 때문에 참조 누락성 제약조건으로 인해 제거할 수 없다. 굳이 제거하고 싶으면 CASCADE 옵션을 사용해야한다.

```SQL
DROP TABLE DIRECTOR;
```

<img src="/images/S-SQL-Table-3/image-20201219001645684.png" alt="image-20201219001645684" style="zoom:80%;" />

<br />

지금 DIRECTOR 테이블의 DIRECTOR_ID 컬럼이 FILMS 테이블에서 FK로 참조되고 있기 때문에 FK 제약 조건으로 인해 테이블 제거할 수 없다.

이 경우에 ```DROP TABLE ... CASCADE``` 명령어를 이용하여 해당 테이블과 관계된 모든 개체를 함계 삭제한다.

```SQL
DROP TABLE DIRECTOR CASCADE;  -- CASCADE 옵션으로 제거 성공
```

```SQL
-- 제거 성공 확인
SELECT * FROM DIRECTOR;
```

<img src="/images/S-SQL-Table-3/image-20201219002930259.png" alt="image-20201219002930259" style="zoom:80%;" />

<br />

부모 테이블이 제거된 경우 자식 테이블의 행은 존재하지반 FK 제약 조건은 삭제됨.



![image-20201219003312930](/images/S-SQL-Table-3/image-20201219003312930.png)

<br />

<img src="/images/S-SQL-Table-3/image-20201219003236123.png" alt="image-20201219003236123" style="zoom:80%;" />

<br />

<br />

**[MISSION 2]**  자식 테이블 (FILMS 테이블)을 제거하기

> 자식 테이블은 바로 제거할 수 있다.

두 테이블을 다시 생성한 후 자식 테이블 (FILMS 테이블)을 먼저 제거 한다.


```SQL
DROP TABLE FILMS;  -- 자식 테이블 제거 성공
```

```SQL
-- 제거 성공 확인
SELECT * FROM FILMS;  
```

<img src="/images/S-SQL-Table-3/image-20201219004411124.png" alt="image-20201219004411124" style="zoom:80%;" />

<br />

<br />

## **2. 임시 테이블**

### 2-1. 개념

임시 테이블은 DB 접속 세션의 활동 기간 동안 존재하는 테이블이다. 세션이 종료되면 임시 테이블은 자동으로 소멸된다.

<br />

### 2-2. 임시 테이블 생성 문법

```SQL
CREATE TEMP TABLE 
  TABLE_NAME (COLUMN);
```

<br />

### 2-3. 임시 테이블 실습

**[실습 1]  임시 테이블 생성 후 세션 재접속**  

> 세션을 종료 후 재접속을 하면 임시 테이블이 소멸된다.

<br />

1. 임시 테이블 생성

   ```SQL
   CREATE TEMP TABLE 
     TB_CUST_TEMP_TEST (CUST_ID INT);
   ```

   ```SQL
   SELECT * FROM TB_CUST_TEMP_TEST;
   ```

   ![image-20201219145857043](/images/S-SQL-Table-3/image-20201219145857043.png)

<br />

2. 테이블에 값을 입력하기

   ```SQL
   INSERT INTO TB_CUST_TEMP_TEST
   VALUES (1);
   ```

   ![image-20201219150041690](/images/S-SQL-Table-3/image-20201219150041690.png)

   <br />

3. 세션 종료 후 재접속

   <img src="/images/S-SQL-Table-3/image-20201219152332829.png" alt="image-20201219152332829" style="zoom:67%;" />

<br />

4. 임시 테이블 불러오기

   ```SQL
   SELECT * FROM TB_CUST_TEMP_TEST;
   ```

   <img src="/images/S-SQL-Table-3/image-20201219152608366.png" alt="image-20201219152608366" style="zoom:80%;" />

   <br />

* 세션을 종료 후 재접속을 하면 임시 테이블이 소멸된 것을 확인할 수 있다.

<br />

<br />

**[실습 2]  기존에 존재하는 테이블과 같은 이름으로 임시 테이블 생성 후 제거**

>같은 이름의 일반 테이블과 임시 테이블이 동시에 존재할 경우:
>
>* SELECT 문으로 테이블 조회할 때 **임시 테이블**을 볼러온다
>
>* DROP 문으로 테이블 제거할 때도 **임시 테이블**을 먼저 제거한다.

<br />

1. 일반 테이블 생성

   ```SQL
   CREATE TABLE TB_CUST_TEMP_TEST
   (
     CUST_ID SERIAL PRIMARY KEY,
     CUST_NAME VARCHAR NOT NULL
   );
   ```

<br />

2. 같은 이름의 임시 테이블 생성

   ```SQL
   CREATE TEMP TABLE TB_CUST_TEMP_TEST
   ( CUST_ID INT );
   ```

<br />

3. 테이블 조회

   ```SQL
   SELECT * FROM TB_CUST_TEMP_TEST;
   ```

   ![image-20201219164733538](/images/S-SQL-Table-3/image-20201219164733538.png)

   

   * 임시 테이블을 불러오는 것을 확인할 수 있다

<br />

4. 테이블 제거

   ```SQL
   DROP TABLE TB_CUST_TEMP_TEST;
   ```

   ```SQL
   SELECT * FROM TB_CUST_TEMP_TEST;
   ```

   ![image-20201219164935024](/images/S-SQL-Table-3/image-20201219164935024.png)

   

   * 임시 테이블이 제거되고 일반 테이블이 그대로 남아있는 것을 확인할 수 있다.

<br />

<br />

## **3. TRUNCATE**

### 3-1. 개념

대용량의 테이블을 빠르게 지우는 방법으로 TRUNCATE가 있다. 테이블의 세그먼트 자체를 바로 지우기 때문에 빠르게 데이터가 지워진다.

<br />

**>> DELETE  <font color='red'>VS</font>  TRUNCATE**

<img src="/images/S-SQL-Table-3/image-20201221144141568.png" alt="image-20201221144141568" style="zoom: 50%;" />

<br />

| DELETE                                              | TRUNCATE                                                     |
| :--------------------------------------------------- | :------------------------------------------------------------ |
| 데이터가 지워지지만 테이블 용량이 줄어 들지 않는다. | 테이블을 삭제하지 않고 데이터만 삭제하지만, 테이블 용량이 줄어 든다. |
| 원하는 데이터만 지울 수 있다.                       | 한꺼번에 다 지워야 한다.                                     |
| 삭제 후 잘못 삭제한 것을 되돌릴 수 있다.            | 삭제 후 되돌릴 수 없다.                                      |
| 속도가 느리다.                                      | 속도가 빠르다.                                               |

<br />

### 3-2. TRUNCATE 문법

```SQL
-- 1개의 테이블 데이터를 빠라게 삭제
TRUNCATE TABLE BIG_TABLE;
```

```SQL
-- N개의 테이블 데이터를 빠르게 삭제
TRUNCATE TABLE BIG_TABLE_1, BIG_TABLE_2;
```

<br />

### 3-3. TRUNCATE 실습

먼저 ACCOUNT 테이블과 동일한 새로운 테이블 BIG_TABLE를 만든다.

```SQL
CREATE TABLE BIG_TABLE AS
  SELECT * FORM ACCOUNT;
```

![image-20201221150858588](/images/S-SQL-Table-3/image-20201221150858588.png)

<br />

이제 TRUNCATE 문을 이용하여 BIG_TABLE의 데이터를 모두 삭제한다.

```SQL
TRUNCATE TABLE BIG_TABLE;

SELECT * FROM BIG_TABLE;
```

![image-20201221151023059](/images/S-SQL-Table-3/image-20201221151023059.png)

<br />

\* ROLLBACK을 통해 데이터를 다시 복원할 수 없다.

```SQL
ROLLBACK;
SELECT * FORM BIG_TABLE;
```

![image-20201221151023059](/images/S-SQL-Table-3/image-20201221151023059.png)

<br />

<br />
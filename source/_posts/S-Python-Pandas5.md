---
title: Python >> Pandas 데이터 파악 - (5) 범위선택
tags:
  - Python
  - Pandas
  - 데이터파악
categories:
  - 【STUDY - Python】
  - Python - 2. Pandas
description: index & column의 범위선택과 조건범위선택
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
abbrlink: 39213
date: 2020-05-24 21:58:03
---



# 범위선택

@[toc]

<br />


```python
import pandas as pd
```


```python
df = pd.read_csv('korean-idol.csv')
```

<br />  

## **1. 단일 column을 선택하는 방법**

> * *df_name* [ '*col_name* ' ]
> * *df_name* [ "*col_name* " ]
> * *df_name* .*col_name*


```python
df.head()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
  </tbody>
</table>

</div>



  


```python
df['이름']
```

  


```python
df["이름"]
```

  


```python
df.이름
```




    0       지민
    1     지드래곤
    2     강다니엘
    3        뷔
    4       화사
    5       정국
    6       민현
    7       소연
    8        진
    9      하성운
    10      태연
    11     차은우
    12      백호
    13      JR
    14      슈가
    Name: 이름, dtype: object



<br /><br />   

## **2. index & column 범위 선택 (range selection)**


```python
df
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> 

### 2-1. 단순 index에 대한 범위 선택


```python
df[:3]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
  </tbody>
</table>

</div>



  


```python
df.head(3)
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
  </tbody>
</table>

</div>



  <br />

### 2-2. index & column 범위선택 -- loc

> *df_name* **.loc** [행(index) 범위, (열)column 범위]

* **행 범위는**  
  ":"  
  ":b"  
  "a:b"  
  등 형식을 사용

* **열 범위는**  
  '*column name* '  
  ['*column name1* ', '*column name2* ']  
  '*column name1* ' : '*column name2* '  
  등 형식을 사용

> <font color='red'> **주의:**  </font> 
>
> * <font color='red'>pandas의 loc</font>에서 범위 a : b는 <font color='blue'>**index a & index b 모두 포함**</font>  
> * <font color='red'>numpy</font>에서는 <font color='blue'>**index a 포함, index b 미포함**</font>


```python
df.loc[:, '이름']
```


    0       지민
    1     지드래곤
    2     강다니엘
    3        뷔
    4       화사
    5       정국
    6       민현
    7       소연
    8        진
    9      하성운
    10      태연
    11     차은우
    12      백호
    13      JR
    14      슈가
    Name: 이름, dtype: object




```python
df.loc[:, ['이름', '생년월일']]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>생년월일</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>1995-10-13</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>1988-08-18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>1996-12-10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>1995-12-30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>1995-07-23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>1997-09-01</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>1995-08-09</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>1998-08-26</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>1992-12-04</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>1994-03-22</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>1989-03-09</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>1997-03-30</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>1995-07-21</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>1995-06-08</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>1993-03-09</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.loc[3:8, ['이름', '생년월일']]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>생년월일</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>1995-12-30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>1995-07-23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>1997-09-01</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>1995-08-09</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>1998-08-26</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>1992-12-04</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.head()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.loc[2:5, '이름':'생년월일']
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> 

### 2-3. index & column 범위선택 -- iloc (position으로 색인)

> 행(index) 범위 선택은 loc와 동일
>
> 열(column) 범위는 'column 명'대신 column position을 사용



* **행 범위는**  
  ":"  
  ":b"  
  "a:b"  
  등 형식을 사용

* **열 범위는**  
  "c"  
  "[c, d]"  
  "c:d"  
  등 형식을 사용

> <font color='red'> **주의:**  </font> 
>
> * pandas의 <font color='red'>iloc</font>에서 범위 a : b는 <font color='blue'>**index a 포함, index b 미포함**</font> (<font color='red'>numpy</font>와 동일)
> * pandas의 <font color='red'>loc</font>에서 범위 a : b는 <font color='blue'>**index a & index b 모두 포함**</font>  


```python
df.iloc[:, [0, 2]]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>소속사</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>빅히트</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>YG</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>커넥트</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>빅히트</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>RBW</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>빅히트</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>플레디스</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>큐브</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>빅히트</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>스타크루이엔티</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>SM</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>판타지오</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>플레디스</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>플레디스</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>빅히트</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.iloc[1:5, [0, 2]]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>소속사</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>YG</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>커넥트</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>빅히트</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>RBW</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.head()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.iloc[1:5, 0:4]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
    </tr>
  </tbody>
</table>

</div>

<br />

<br />  

## **3. index & column 조건범위선택 -- Boolean Indexing**

Boolean indexing은 Numpy에서의 Boolean indexing과 같은 원리다


```python
df.head()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

### 3-1. 조건에 만족한 row들의 모든 column을 추출

> df [*조건* ]


```python
df['키'] > 180
```


    0     False
    1     False
    2     False
    3     False
    4     False
    5     False
    6      True
    7     False
    8     False
    9     False
    10    False
    11     True
    12    False
    13    False
    14    False
    Name: 키, dtype: bool




```python
df[df['키'] > 180]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
  </tbody>
</table>

</div>



  <br />

### 3-2. 조건에 만족한 row들의 특정 column들을 추출

>  **방법 1.** *df_name* [*조건* ] [*column범위* ]


```python
df[ df['키'] > 180 ] ['이름']
```


    6      민현
    11    차은우
    Name: 이름, dtype: object




```python
df [ df['키'] > 180 ] [['이름', '키']]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>키</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>182.3</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>183.0</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

>  **방법 2.** loc를 활용: *df_name*.loc[ *조건* , *column범위*  ]       <font color='blue'> *【추천】* </font> 


```python
df.loc[ df['키'] > 180, '이름' ]
```


    6      민현
    11    차은우
    Name: 이름, dtype: object




```python
df.loc[ df['키'] > 180, ['이름', '그룹'] ]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.loc[ df['키'] > 180, '이름' : '성별']
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
    </tr>
  </tbody>
</table>

</div>



<br /> <br /> 

## **4. index & column 조건범위선택 -- inis을 활용란 색인**

column값이 미리 정의한 list에 속한다는 조건을 걸고자 할 때 사용한다


```python
my_condition = ['플레디스', 'SM']
```


```python
df['소속사'].isin(my_condition)
```


    0     False
    1     False
    2     False
    3     False
    4     False
    5     False
    6      True
    7     False
    8     False
    9     False
    10     True
    11    False
    12     True
    13     True
    14    False
    Name: 소속사, dtype: bool




```python
df.loc[ df['소속사'].isin(my_condition) ]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.loc[ df['소속사'].isin(my_condition) , ['이름', '소속사'] ]
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>소속사</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>플레디스</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>SM</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>플레디스</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>플레디스</td>
    </tr>
  </tbody>
</table>

</div>



<br />

<br />
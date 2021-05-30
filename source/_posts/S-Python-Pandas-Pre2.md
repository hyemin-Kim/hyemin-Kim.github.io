---
title: Python >> Pandas 전처리 - (2) 결측값 및 중복값 처리
tags:
  - Python
  - Pandas
  - 전처리
categories: 
  - [【STUDY - Python】, Python - 2. Pandas]
  - [【STUDY - Python】, Python - 전처리]
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
abbrlink: 27861
date: 2020-06-18 00:07:04
---

# 결측값 및 중복값 처리

@[toc]

<br />


```python
import pandas as pd
```


```python
df = pd.read_csv('korean-idol.csv')
```

  

  <br />

## **1. 결측값을 제거하기 -- dropna()**

> * 결측값이 있는 행을 제거:   
>   (1) *df_name* **.dropna()**  
>   (2) *df_name* **.dropna(axis=0)**
> * 결측값이 있는 열을 제거: *df_name* **.dropna(axis=1)**
> * NA가 하나라도 있는 경우 제거: *df_name* **.dropna**(axis=0, **how = 'any'**) 
> * 모두가 NA인 경우 제거: *df_name* **.dropna**(axis=0, **how = 'all'**)


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15 entries, 0 to 14
    Data columns (total 8 columns):
     #   Column   Non-Null Count  Dtype  
    ---  ------   --------------  -----  
     0   이름       15 non-null     object 
     1   그룹       14 non-null     object 
     2   소속사      15 non-null     object 
     3   성별       15 non-null     object 
     4   생년월일     15 non-null     object 
     5   키        13 non-null     float64
     6   혈액형      15 non-null     object 
     7   브랜드평판지수  15 non-null     int64  
    dtypes: float64(1), int64(1), object(6)
    memory usage: 1.1+ KB



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

<table>
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

**(1) 결측값이 있는 행 제거**


```python
df.dropna()
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

<table>
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




```python
df.dropna(axis = 0)
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

<table>
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

**(2) 결측 값이 있는 열 제거**


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15 entries, 0 to 14
    Data columns (total 8 columns):
     #   Column   Non-Null Count  Dtype  
    ---  ------   --------------  -----  
     0   이름       15 non-null     object 
     1   그룹       14 non-null     object 
     2   소속사      15 non-null     object 
     3   성별       15 non-null     object 
     4   생년월일     15 non-null     object 
     5   키        13 non-null     float64
     6   혈액형      15 non-null     object 
     7   브랜드평판지수  15 non-null     int64  
    dtypes: float64(1), int64(1), object(6)
    memory usage: 1.1+ KB



```python
df.dropna(axis=1)
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

<table>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

**(3) NA가 하나라도 있는 경우 행 제거**


```python
df.dropna(axis=0, how = 'any')
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

<table>
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

**(4) 모두가 NA인 경우 행 제거**


```python
import numpy as np
```


```python
df.iloc[10] = np.nan
```


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

<table>
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
      <td>10523260.0</td>
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
      <td>9916947.0</td>
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
      <td>8273745.0</td>
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
      <td>8073501.0</td>
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
      <td>7650928.0</td>
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
      <td>5208335.0</td>
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
      <td>4989792.0</td>
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
      <td>4668615.0</td>
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
      <td>4570308.0</td>
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
      <td>4036489.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <td>3506027.0</td>
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
      <td>3301654.0</td>
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
      <td>3274137.0</td>
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
      <td>2925442.0</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.dropna(axis=0, how = 'all')
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

<table>
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
      <td>10523260.0</td>
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
      <td>9916947.0</td>
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
      <td>8273745.0</td>
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
      <td>8073501.0</td>
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
      <td>7650928.0</td>
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
      <td>5208335.0</td>
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
      <td>4989792.0</td>
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
      <td>4668615.0</td>
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
      <td>4570308.0</td>
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
      <td>4036489.0</td>
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
      <td>3506027.0</td>
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
      <td>3301654.0</td>
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
      <td>3274137.0</td>
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
      <td>2925442.0</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> <br />

  

## **2. 결측값을 채워주기 -- fillna**

> *df_name* [ '*na_col_name* ' ] **.fillna(*fill_value*)**  

> 결측값을 채운 데이터프레임을 유지시키려면:  
> (1) inplace = True 옵션을 추가함  
> (2) 원 dataframe에 다시 대입함


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15 entries, 0 to 14
    Data columns (total 8 columns):
     #   Column   Non-Null Count  Dtype  
    ---  ------   --------------  -----  
     0   이름       15 non-null     object 
     1   그룹       14 non-null     object 
     2   소속사      15 non-null     object 
     3   성별       15 non-null     object 
     4   생년월일     15 non-null     object 
     5   키        13 non-null     float64
     6   혈액형      15 non-null     object 
     7   브랜드평판지수  15 non-null     int64  
    dtypes: float64(1), int64(1), object(6)
    memory usage: 1.1+ KB


"키"에 2개의 데이터가 누락, "그룹"에 1개의 데이터가 누락된 것을 확인할 수 있다

  <br />

### 2-1. NA값을 특정 숫자로 채우기

> * *df_name*[ '*na_col_name* ' ] **.fillna** (*new_value*, inplace = True)
> * *df_name*[ '*na_col_name* ' ] = *df_name*[ '*na_col_name* ' ] **.fillna** (*new_value*)

<br />

**e.g.** 누락된 '키' 값을 '-1'로 채워줌


```python
df['키'].fillna(-1)
```


    0     173.6
    1     177.0
    2     180.0
    3     178.0
    4     162.1
    5     178.0
    6     182.3
    7      -1.0
    8     179.2
    9     167.1
    10     -1.0
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64



<br />  

이때는 원 데이터가 변화되지 않음.


```python
df['키']
```


    0     173.6
    1     177.0
    2     180.0
    3     178.0
    4     162.1
    5     178.0
    6     182.3
    7       NaN
    8     179.2
    9     167.1
    10      NaN
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64



 <br />

수정된 데이터를 유지시키려면:

<방법1>


```python
df2 = df.copy()
```


```python
df2['키'].fillna(-1, inplace = True)
```


```python
df2['키']
```


    0     173.6
    1     177.0
    2     180.0
    3     178.0
    4     162.1
    5     178.0
    6     182.3
    7      -1.0
    8     179.2
    9     167.1
    10     -1.0
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64

<br />

  

<방법2>


```python
df2 = df.copy()
```


```python
df2['키'] = df2['키'].fillna(-1)
```


```python
df2['키']
```


    0     173.6
    1     177.0
    2     180.0
    3     178.0
    4     162.1
    5     178.0
    6     182.3
    7      -1.0
    8     179.2
    9     167.1
    10     -1.0
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64

<br />

  

### 2-2. NA값을 통계값으로 채우기

> * *df_name*[ '*na_col_name* ' ] **.fillna** (*df_name*[ '*na_col_name* ' ] **.mean()**, inplace = True)
> * *df_name*[ '*na_col_name* ' ] = *df_name*[ '*na_col_name* ' ] **.fillna** (*df_name*[ '*na_col_name* ' ] **.mean()**)


```python
df2 = df.copy()
```


```python
df2['키']
```


    0     173.6
    1     177.0
    2     180.0
    3     178.0
    4     162.1
    5     178.0
    6     182.3
    7       NaN
    8     179.2
    9     167.1
    10      NaN
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64



 <br /> 

**(1) 평균으로 대체**


```python
df2['키'].mean()
```


    175.79230769230767

<br />


```python
df2['키'].fillna(df2['키'].mean(), inplace = True)
```


```python
df2['키'] = df2['키'].fillna(df2['키'].mean())
```


```python
df2['키']
```


    0     173.600000
    1     177.000000
    2     180.000000
    3     178.000000
    4     162.100000
    5     178.000000
    6     182.300000
    7     175.792308
    8     179.200000
    9     167.100000
    10    175.792308
    11    183.000000
    12    175.000000
    13    176.000000
    14    174.000000
    Name: 키, dtype: float64



 <br /> 

**(2) 중위값으로 대체**


```python
df2 = df.copy()
```


```python
df2['키'].median()
```


    177.0

<br />


```python
df2['키'].fillna(df2['키'].median(), inplace = True)
```


```python
df2['키'] = df2['키'].fillna(df2['키'].median())
```


```python
df2['키']
```


    0     173.6
    1     177.0
    2     180.0
    3     178.0
    4     162.1
    5     178.0
    6     182.3
    7     177.0
    8     179.2
    9     167.1
    10    177.0
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64



<br />  <br />

  

## **3. 중복된 값을 제거하기 -- drop_duplicates**


```python
df = pd.read_csv('korean-idol.csv')
```


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

<table>
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

### 3-1. column의 중복값 제거

> *df_name* ["*col_name*"] **.drop_duplicates( keep = .. )**

> * 여러 개 중복값 (NaN 포함) 중에서 기본적으로 첫번째 것만 유지시키고 나머지는 다 제거한다  
> * 하지만 keep 옵션으로 유지하고 싶은 데이터를 선택할 수 있다. [keep: 'first' / 'last']
> * 이때는 해당 위치의 값만 삭제되고 행 자체는 유지된다

<br />

**(1) 중복값 중의 첫번째를 유지시킴  <font color = 'blue'> (default) </font>**


```python
df['키']
```


    0     173.6
    1     177.0
    2     180.0
    3       NaN
    4     162.1
    5     178.0
    6     182.3
    7       NaN
    8     179.2
    9     167.1
    10      NaN
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64




```python
df['키'].drop_duplicates()  # remove 2nd "178.0" & 2nd "NaN"
```


    0     173.6
    1     177.0
    2     180.0
    3       NaN
    4     162.1
    5     178.0
    6     182.3
    8     179.2
    9     167.1
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64




```python
df['키'].drop_duplicates(keep='first')
```


    0     173.6
    1     177.0
    2     180.0
    3       NaN
    4     162.1
    5     178.0
    6     182.3
    8     179.2
    9     167.1
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64



<br />  

**(2) 중복값 중의 마지막을 유지시킴**


```python
df['키']
```


    0     173.6
    1     177.0
    2     180.0
    3     178.0
    4     162.1
    5     178.0
    6     182.3
    7       NaN
    8     179.2
    9     167.1
    10      NaN
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64




```python
df['키'].drop_duplicates(keep='last')
```


    0     173.6
    1     177.0
    2     180.0
    4     162.1
    5     178.0
    6     182.3
    8     179.2
    9     167.1
    10      NaN
    11    183.0
    12    175.0
    13    176.0
    14    174.0
    Name: 키, dtype: float64



 <br /> 

**이때는 해당위치의 값만 제거되고 행 자체는 유지됨**


```python
df['키'] = df['키'].drop_duplicates(keep='last')
```


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

<table>
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
      <td>NaN</td>
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

### 3-2. 행 전체 제거

> *df_name* **.drop_duplicates**("*col_name*", keep = ..)

> 지정한 column에서 중복값이 포함되어 있으면 중복값을 포함한 행을 전체 제거


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

<table>
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
      <td>NaN</td>
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




```python
df['그룹']
```


    0     방탄소년단
    1        빅뱅
    2       NaN
    3     방탄소년단
    4       마마무
    5     방탄소년단
    6      뉴이스트
    7       아이들
    8     방탄소년단
    9        핫샷
    10     소녀시대
    11     아스트로
    12     뉴이스트
    13     뉴이스트
    14    방탄소년단
    Name: 그룹, dtype: object




```python
df.drop_duplicates('그룹')
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

<table>
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
  </tbody>
</table>

</div>




```python
df.drop_duplicates('그룹', keep = 'last')
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

<table>
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

<br />
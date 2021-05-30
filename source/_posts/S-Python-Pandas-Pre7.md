---
title: Python >> Pandas 전처리 - (7) 기타
tags:
  - Python
  - Pandas
  - 전처리
categories: 
  - [【STUDY - Python】, Python - 2. Pandas]
  - [【STUDY - Python】, Python - 전처리]
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
description: 데이터 타입별 column 선택; One-hot-encoding (dummy 변환)
abbrlink: 48472
date: 2020-06-20 22:28:42
---

# 기타

  @[toc]

<br />


```python
import pandas as pd
```


```python
df = pd.read_csv("korean-idol.csv")
```


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

  <br />

  

## **1. 데이터 타입별 column 선택 (select_dtypes)**


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

<br />


###  문자열이 있는 column만 선택 / 배제

> * *df_name* **.select_dtypes (include = 'object')**
> * *df_name* **.select_dtypes (exclude = 'object')**

<br />  

**(1) 문자열 column만 선택**


```python
df.select_dtypes(include = 'object')
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
      <th>혈액형</th>
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
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>A</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>A</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>AB</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>A</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>A</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>O</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>B</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>O</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>A</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>A</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>B</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>AB</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>O</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>O</td>
    </tr>
  </tbody>
</table>

</div>

<br />

  

**(2) 문자열 column 배제 (문자열이 아닌 column만 선택)**


```python
df.select_dtypes(exclude = 'object')
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
      <th>키</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>173.6</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>177.0</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>180.0</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>178.0</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>162.1</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>178.0</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>182.3</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>179.2</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>167.1</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>183.0</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>175.0</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>176.0</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>174.0</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>

<br />

  

**문자열이 포함된 DataFrame의 연산으로 발생되는 Error문제는 이 방법을 이용하여 해결할 수 있다**


```python
df + 10
```


    ---------------------------------------------------------------------------
    
    TypeError                                 Traceback (most recent call last)
    
    D:\Anaconda\lib\site-packages\pandas\core\ops\array_ops.py in na_arithmetic_op(left, right, op, str_rep)
        148     try:
    --> 149         result = expressions.evaluate(op, str_rep, left, right)
        150     except TypeError:


    D:\Anaconda\lib\site-packages\pandas\core\computation\expressions.py in evaluate(op, op_str, a, b, use_numexpr)
        207     if use_numexpr:
    --> 208         return _evaluate(op, op_str, a, b)
        209     return _evaluate_standard(op, op_str, a, b)


    D:\Anaconda\lib\site-packages\pandas\core\computation\expressions.py in _evaluate_numexpr(op, op_str, a, b)
        120     if result is None:
    --> 121         result = _evaluate_standard(op, op_str, a, b)
        122 


    D:\Anaconda\lib\site-packages\pandas\core\computation\expressions.py in _evaluate_standard(op, op_str, a, b)
         69     with np.errstate(all="ignore"):
    ---> 70         return op(a, b)
         71 


    TypeError: can only concatenate str (not "int") to str


​    <br />

```python
df.select_dtypes(exclude = 'object') + 10
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
      <th>키</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183.6</td>
      <td>10523270</td>
    </tr>
    <tr>
      <th>1</th>
      <td>187.0</td>
      <td>9916957</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190.0</td>
      <td>8273755</td>
    </tr>
    <tr>
      <th>3</th>
      <td>188.0</td>
      <td>8073511</td>
    </tr>
    <tr>
      <th>4</th>
      <td>172.1</td>
      <td>7650938</td>
    </tr>
    <tr>
      <th>5</th>
      <td>188.0</td>
      <td>5208345</td>
    </tr>
    <tr>
      <th>6</th>
      <td>192.3</td>
      <td>4989802</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>4668625</td>
    </tr>
    <tr>
      <th>8</th>
      <td>189.2</td>
      <td>4570318</td>
    </tr>
    <tr>
      <th>9</th>
      <td>177.1</td>
      <td>4036499</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>3918671</td>
    </tr>
    <tr>
      <th>11</th>
      <td>193.0</td>
      <td>3506037</td>
    </tr>
    <tr>
      <th>12</th>
      <td>185.0</td>
      <td>3301664</td>
    </tr>
    <tr>
      <th>13</th>
      <td>186.0</td>
      <td>3274147</td>
    </tr>
    <tr>
      <th>14</th>
      <td>184.0</td>
      <td>2925452</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> 

**(3) "문자열 column" / "비문자열 column" 의 column명을 추출**


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

<br />

```python
obj_cols = df.select_dtypes(include = 'object').columns
obj_cols
```


    Index(['이름', '그룹', '소속사', '성별', '생년월일', '혈액형'], dtype='object')

<br />


```python
num_cols = df.select_dtypes(exclude = 'object').columns
num_cols
```


    Index(['키', '브랜드평판지수'], dtype='object')

<br />


```python
df[num_cols]
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
      <th>키</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>173.6</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>177.0</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>180.0</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>178.0</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>162.1</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>178.0</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>182.3</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>179.2</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>167.1</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>183.0</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>175.0</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>176.0</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>174.0</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> <br />

  

## **2. One-hot-encoding (원핫인코딩)**

> **One-hot-encoding:** Categorical data를 dummy data로 변환시키는 방법  
>
> * Dummy data로 변환 시 한개의 요소는 True (1) 로, 나머지 요소는 Flase (0) 로 변환시킨다

> **pd.get_dummies** (*df_name* [ '*col_name*' ], prefix = "...")
>
> * prefix: dummy data 로 분리된 새 column들의 column name에 접두사 붙이기

  <br />


```python
df['혈액형']
```


    0      A
    1      A
    2      A
    3     AB
    4      A
    5      A
    6      O
    7      B
    8      O
    9      A
    10     A
    11     B
    12    AB
    13     O
    14     O
    Name: 혈액형, dtype: object

<br />


```python
pd.get_dummies(df['혈액형'])
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
      <th>A</th>
      <th>AB</th>
      <th>B</th>
      <th>O</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
pd.get_dummies(df['혈액형'], prefix = '혈액형')
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
      <th>혈액형_A</th>
      <th>혈액형_AB</th>
      <th>혈액형_B</th>
      <th>혈액형_O</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> 

> **categorical data의 각 카테고리가 숫자형식으로 표현됐을 때 one-hot-encoding이 더 중요해지는 이유:**  
>
> * categorical data의 각 카테고리를 상징하는 숫자들은 **그저 분류의 의미를 가질 뿐**, 숫자의 크기 자체는 아무 의미도 없고, 숫자들의 연산도 역시 무의미하다. 
> * 하지만 이를 one-hot-encoding 작업 없이 머신러닝 알고리즘에 바로 넣으면 컴퓨터가 이 숫자들을 **대소비교가 가능하고 연산이 가능하는 "숫자"로 인식**하게 되므로 카테고리 간에 **잘못된 관계**를 맺을 수 있음.
> * 따라서 이런 경우에는 one-hot-encoding 작업이 꼭 필요하다

<br />  


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


```python
blood_map = {
    'A': 0,
    'B': 1,
    'AB': 2,
    'O': 3,
}
```


```python
df["혈액형_code"] = df["혈액형"].map(blood_map)
```


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
      <th>혈액형_code</th>
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
      <td>0</td>
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
      <td>0</td>
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
      <td>0</td>
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
      <td>2</td>
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
      <td>0</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
df["혈액형_code"].value_counts()
```


    0    7
    3    4
    2    2
    1    2
    Name: 혈액형_code, dtype: int64

<br />

  


```python
df["혈액형_code"]
```


    0     0
    1     0
    2     0
    3     2
    4     0
    5     0
    6     3
    7     1
    8     3
    9     0
    10    0
    11    1
    12    2
    13    3
    14    3
    Name: 혈액형_code, dtype: int64

<br />


```python
pd.get_dummies(df[ "혈액형_code" ])
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
pd.get_dummies(df["혈액형_code"], prefix = "혈액형")
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
      <th>혈액형_0</th>
      <th>혈액형_1</th>
      <th>혈액형_2</th>
      <th>혈액형_3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

</div>

<br />

<br />
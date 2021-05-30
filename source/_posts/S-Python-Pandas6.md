---
title: Python >> Pandas 데이터 파악 - (6) 결측값 확인 및 추출
tags:
  - Python
  - Pandas
  - 데이터파악
categories:
  - 【STUDY - Python】
  - Python - 2. Pandas
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
abbrlink: 65377
date: 2020-06-12 01:21:05
---

# 결측값 확인 및 추출

@[toc]

<br />


```python
import pandas as pd
```


```python
df = pd.read_csv('korean-idol.csv')
```



<br />

## **1. 결측값에 대하여**

* Null 값은 **비어있는 값, 고급 언어로 결측값**이다

* pandas 에서는 NaN => Not a Number 로 표기 된다

  <br />


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

  <br />

## **2. column별 (비)결측값 개수 확인 -- info()**

info() 로 각 column별의 결측값(NaN) 개수를 쉽게 확인할 수 있다.

<br />


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

<br />


## **3. (비)결측값 위치 확인**

* .isna()

* .isnull()

* .notna()

* .notnull()

  <br />

### 3-1. 전체 Data

>  *df_name* .명령어

<br />

**(1) 결측값 = True**


```python
df.isna()
```

<br />


```python
df.isnull()
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
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>13</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>14</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>

<br />

**(2) 비결측값 = True**


```python
df.notna()
```

<br />


```python
df.notnull()
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
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>7</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>8</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>9</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>10</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>11</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>12</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>13</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>14</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



<br /> <br /> 

### 3-2. 특정 column

> *df_name* [ '*col_name*' ] .명령어

<br />

**(1) 결측값 = True**


```python
df['그룹'].isna()
```


<br />


```python
df['그룹'].isnull()
```




    0     False
    1     False
    2      True
    3     False
    4     False
    5     False
    6     False
    7     False
    8     False
    9     False
    10    False
    11    False
    12    False
    13    False
    14    False
    Name: 그룹, dtype: bool

<br />

**(2) 비결측값 = True**


```python
df['그룹'].notna()
```

<br />


```python
df['그룹'].notnull()
```




    0      True
    1      True
    2     False
    3      True
    4      True
    5      True
    6      True
    7      True
    8      True
    9      True
    10     True
    11     True
    12     True
    13     True
    14     True
    Name: 그룹, dtype: bool



 <br />

<br />  

## **4. (비)결측값 추출**

### 4-1. 해당 column만 추출

> 결측값: *df_name* [ '*col_name*']  [ *df_name* [ '*col_name*' ] .isna() / isnull() ] 
> 비결측값: *df_name* [ '*col_name*' ]  [*df_name* [ '*col_name*' ] .notna() / notnull()] 



  <br />


```python
df['그룹'][df['그룹'].isna()]
```




    2    NaN
    Name: 그룹, dtype: object

<br />


```python
df['그룹'][df['그룹'].notnull()]
```




    0     방탄소년단
    1        빅뱅
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



  <br />

<br />

### 4-2. 전체 column 추출

> 결측값: *df_name* .loc [*df_name* [ '*col_name*' ] .isna() / isnull() ]
>
> 비결측값: *df_name* .loc [*df_name* ['*col_name*] .notna() / notnull() ]



<br />


```python
df.loc[df['그룹'].isna()]
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


```python
df.loc[df['그룹'].notnull()]
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

<br />  

### 4-3. 지정한 column 추출 

> 결측값: *df_name* .loc [*df_name* [ '*na_col_name*' ] .isna() / isnull() , ['*col_name1*', '*col_name2*', ...]]
>
> 비결측값: *df_name* .loc [*df_name* ['*na_col_name*] .notna() / notnull() , ['*col_name1*', '*col_name2*', ...]]



<br />


```python
df.loc[df['그룹'].isna(), ['이름', '소속사']]
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
      <th>2</th>
      <td>강다니엘</td>
      <td>커넥트</td>
    </tr>
  </tbody>
</table>
</div>

<br />


```python
df.loc[df['그룹'].notnull(), ['이름', '소속사']]
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



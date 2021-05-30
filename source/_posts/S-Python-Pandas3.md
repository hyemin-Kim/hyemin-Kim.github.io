---
title: 'Python >> Pandas 데이터 파악 - (3) 기본정보 & 통계정보 파악'
tags:
  - Python
  - Pandas
  - 데이터파악
categories:
  - 【STUDY - Python】
  - Python - 2. Pandas
description: '기본 행&열 정보, 통계값 알아보기'
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
abbrlink: 36020
date: 2020-05-24 17:06:08
---

# 기본정보 & 통계정보 파악

  @[toc]

  <br />


```python
import pandas as pd
```

## **1. 파일 읽어오기 (csv)**


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

## **2. 기본 행&열 정보 알아보기  (column, index, info)**

### 2-1. column (열) 이름 출력하기

> *df_name* **.columns**


```python
df.columns
```


    Index(['이름', '그룹', '소속사', '성별', '생년월일', '키', '혈액형', '브랜드평판지수'], dtype='object')



​    <br />

### 2-2. column (열) 이름 재정의하기

**(1) 전체 column 이름**

> *df_name* **.columns** = [...]

**예:** "이름" --> "name":


```python
new_col = ['name', '그룹', '소속사', '성별', '생년월일', '키', '혈액형', '브랜드평판지수']
```


```python
df.columns = new_col
```


```python
df.columns
```


    Index(['name', '그룹', '소속사', '성별', '생년월일', '키', '혈액형', '브랜드평판지수'], dtype='object')



​    <br />

**(2) 개별 column 이름**

> *df_name* **.rename** ( columns = { "*old_name*" : "*new_name*" } )

​    <br />  


```python
df = pd.read_csv('korean-idol.csv')
```


```python
df.columns
```


    Index(['이름', '그룹', '소속사', '성별', '생년월일', '키', '혈액형', '브랜드평판지수'], dtype='object') 

​    <br />

```python
df = df.rename(columns = {"이름" : "name"})  
```


```python
df.columns
```


    Index(['name', '그룹', '소속사', '성별', '생년월일', '키', '혈액형', '브랜드평판지수'], dtype='object')

​    <br />

### 2-3. index (행) 정보 출력하기

> *df_name* **.index**


```python
df.index
```


    RangeIndex(start=0, stop=15, step=1)



   <br />

### 2-4. info (기본적인 column 정보와 데이터 타입)

> *df_name* **.info()**  

> **Tip:** info메소드는 주로 빠진 값 (null 값)과 데이터 타입을 볼 때 활용함


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15 entries, 0 to 14
    Data columns (total 8 columns):
     #   Column   Non-Null Count  Dtype  
    ---  ------   --------------  -----  
     0   name     15 non-null     object 
     1   그룹       14 non-null     object 
     2   소속사      15 non-null     object 
     3   성별       15 non-null     object 
     4   생년월일     15 non-null     object 
     5   키        13 non-null     float64
     6   혈액형      15 non-null     object 
     7   브랜드평판지수  15 non-null     int64  
    dtypes: float64(1), int64(1), object(6)
    memory usage: 1.1+ KB


"object" type은 주로 문자형 데이터를 가리킴.

  <br />  

## **3. 형태 (shape) 알아보기**

> shape는 tuple형태로 반환되며, 첫번째는 row, 두번째는 column의 숫자를 의미함.


```python
df.shape
```


    (15, 8)



  <br />

## **4. 상위 5개, 하위 5개의 정보만 보기**

> 상위 5개 row:  *df_name* **.head()**   
> 하위 5개 row:  *df_name* **.tail()**   
> 상위 n개 row:  *df_name* **.head(n)**  
> 하위 n개 row:  *df_name* **.tail(n)**  


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
      <th>name</th>
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
df.tail()
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
      <th>name</th>
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
      <th>name</th>
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
df.tail(2)
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
      <th>name</th>
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

  

## **5. 통계 정보 알아보기**

> 통계값은 산술 연산이 가능한 숫자형 (float / int) 인 column을 다룬다

### 5-1. 전체 통계 정보

>  *df_name* **.describe()**

산술 연산이 가능한 column만 출력됨


```python
df.describe()
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
      <th>count</th>
      <td>13.000000</td>
      <td>1.500000e+01</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>175.792308</td>
      <td>5.655856e+06</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.820576</td>
      <td>2.539068e+06</td>
    </tr>
    <tr>
      <th>min</th>
      <td>162.100000</td>
      <td>2.925442e+06</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>174.000000</td>
      <td>3.712344e+06</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>177.000000</td>
      <td>4.668615e+06</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>179.200000</td>
      <td>7.862214e+06</td>
    </tr>
    <tr>
      <th>max</th>
      <td>183.000000</td>
      <td>1.052326e+07</td>
    </tr>
  </tbody>
</table>

</div>



   <br />

### 5-2. 최소값(min),  최대값(max), 중앙값(median), 최빈값(mode)

> 최소값: *df_name* [ '*col_name*' ] **.min()**  
> 최대값: *df_name* [ '*col_name*' ] **.max()**  
> 중앙값: *df_name* [ '*col_name*' ] **.median()**  
> 최빈값: *df_name* [ '*col_name*' ] **.mode()**


```python
df['키'].min()
```


    162.1




```python
df['키'].max()
```


    183.0




```python
df['키'].median()
```


    177.0




```python
df['키'].mode()
```


    0    178.0
    dtype: float64



 <br />

### 5-3. 합계(sum), 평균(mean), 분산(var), 표준편차(std)

> 합계(sum): *df_name* [ '*col_name*' ] **.sum()**  
> 평균(mean): *df_name* [ '*col_name*' ] **.mean()**  
> 분산(variance): *df_name* [ '*col_name*' ] **.var()**  
> 표준편차(standard deviation): *df_name* [ '*col_name*' ] **.std()**


```python
df['키'].sum()
```


    2285.3

 













```python
df['키'].mean()
```


    175.7923076923077




```python
df['키'].var()
```


    33.879102564102595




```python
df['키'].std()
```


    5.820575793175672



<br />

### 5-4. 갯수를 세는 count

> *df_name* [ '*col_name*' ] **.count**


```python
df['키'].count()
```


    13

  <br />

  <br />
---
title: Python >> Pandas 데이터 파악 - (7) 기타
description: '피벗테이블, GroupBy, Multi-Index'
tags:
  - Python
  - Pandas
  - 데이터파악
categories:
  - 【STUDY - Python】
  - Python - 2. Pandas
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
abbrlink: 61241
date: 2020-06-17 15:12:40
---

# 기타

@[toc]

<br />


```python
import pandas as pd
```


```python
df = pd.read_csv('korean-idol.csv')
```

  <br />

## **1. 피벗테이블**

* 데이터 열 중에서 **두 개의 열을 각각 행 인덱스, 열 인덱스로 사용**하여 데이터를 조회하여 펼쳐놓은 건을 의미함
* 왼쪽에 나타나는 인덱스를 **행 인덱스, 상단에 나타나는 인덱스를 열 인덱스**라고 부른다

> pd.pivot_table(*df_name*, index = "*col_name_분류기준1*", columns = "*col_name_분류기준2*", values = "*col_name_조회대상*", aggfunc = ...)
>
> * index는 행 인덱스
> * columns는 열 인덱스
> * values는 조회하고 싶은 값
> * aggfunc는 value를 산출하는 연산법   
>   (1) e.g.: aggfunc = np.sum / np.mean  
>   (2) 설정하지 않은 경우 기본적으로 평균값을 구한다


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
pd.pivot_table(df, index = "소속사", columns = "혈액형", values = "키")
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
      <th>혈액형</th>
      <th>A</th>
      <th>AB</th>
      <th>B</th>
      <th>O</th>
    </tr>
    <tr>
      <th>소속사</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>RBW</th>
      <td>162.1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>YG</th>
      <td>177.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>빅히트</th>
      <td>175.8</td>
      <td>178.0</td>
      <td>NaN</td>
      <td>176.60</td>
    </tr>
    <tr>
      <th>스타크루이엔티</th>
      <td>167.1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>커넥트</th>
      <td>180.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>판타지오</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>183.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>플레디스</th>
      <td>NaN</td>
      <td>175.0</td>
      <td>NaN</td>
      <td>179.15</td>
    </tr>
  </tbody>
</table>

</div>




```python
import numpy as np
```


```python
pd.pivot_table(df, index = "그룹", columns = "혈액형", values  = "브랜드평판지수", aggfunc = np.sum)
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
      <th>혈액형</th>
      <th>A</th>
      <th>AB</th>
      <th>B</th>
      <th>O</th>
    </tr>
    <tr>
      <th>그룹</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>뉴이스트</th>
      <td>NaN</td>
      <td>3301654.0</td>
      <td>NaN</td>
      <td>8263929.0</td>
    </tr>
    <tr>
      <th>마마무</th>
      <td>7650928.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>방탄소년단</th>
      <td>15731595.0</td>
      <td>8073501.0</td>
      <td>NaN</td>
      <td>7495750.0</td>
    </tr>
    <tr>
      <th>빅뱅</th>
      <td>9916947.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>소녀시대</th>
      <td>3918661.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>아스트로</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>3506027.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>아이들</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>4668615.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>핫샷</th>
      <td>4036489.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

</div>



<br /><br />   

## **2. GroupBy (그룹으로 묶어 보기)**

* groupby는 데이터를 **그룹으로 묶어 분석**할 때 활용한다
* **소속사**별 키의 평균, **성별** 키의 평균 등 특정, 그룹별 통계 및 데이터의 성질을 확인하고자 할 때 활용한다

> groupby와 함께
>
> * count() - 갯수
> * sum() - 합계
> * mean() - 평균
> * var() - 분산
> * std() -표준편차
> * min() / max() - 최소값, 최대값


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
df.groupby("소속사")
```


    <pandas.core.groupby.generic.DataFrameGroupBy object at 0x0000024E760EC288>




```python
df.groupby('소속사').count()
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
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
    <tr>
      <th>소속사</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>RBW</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>SM</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>YG</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>빅히트</th>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>스타크루이엔티</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>커넥트</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>큐브</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>판타지오</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>플레디스</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>



<br /> 

산술 통계는 자동으로 산술통계가 가능한 열만 출력됨.


```python
df.groupby('그룹').mean()
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
    <tr>
      <th>그룹</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>뉴이스트</th>
      <td>177.766667</td>
      <td>3.855194e+06</td>
    </tr>
    <tr>
      <th>마마무</th>
      <td>162.100000</td>
      <td>7.650928e+06</td>
    </tr>
    <tr>
      <th>방탄소년단</th>
      <td>176.560000</td>
      <td>6.260169e+06</td>
    </tr>
    <tr>
      <th>빅뱅</th>
      <td>177.000000</td>
      <td>9.916947e+06</td>
    </tr>
    <tr>
      <th>소녀시대</th>
      <td>NaN</td>
      <td>3.918661e+06</td>
    </tr>
    <tr>
      <th>아스트로</th>
      <td>183.000000</td>
      <td>3.506027e+06</td>
    </tr>
    <tr>
      <th>아이들</th>
      <td>NaN</td>
      <td>4.668615e+06</td>
    </tr>
    <tr>
      <th>핫샷</th>
      <td>167.100000</td>
      <td>4.036489e+06</td>
    </tr>
  </tbody>
</table>

</div>




```python
df.groupby('성별').sum()
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
    <tr>
      <th>성별</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>남자</th>
      <td>2123.2</td>
      <td>68599637</td>
    </tr>
    <tr>
      <th>여자</th>
      <td>162.1</td>
      <td>16238204</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

특정 열만 출력하고 싶다면?


```python
df.groupby('혈액형')['키'].mean()
```


    혈액형
    A     172.966667
    AB    176.500000
    B     183.000000
    O     177.875000
    Name: 키, dtype: float64



<br />

<br /> 

## **3. Multi-Index (복합 인덱스)**

### 3-1. Multi-Index 적용

행 인덱스를 복합적으로 구성하고 싶은 경우는 인덱스를 리스트로 만들어 준다

> *df_name* **.groupby(['*col_name_1*','*col_name_2*'])** .*mean()*   
>
> * 데이터를 먼저 col_1기준으로 분류한 다음, col_2기준으로 한번 더 분류한다. 2번 분류 후의 데이터에 대해 산술통계값을 구한다 


```python
df.groupby(['혈액형', '성별']).mean()
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
      <th></th>
      <th>키</th>
      <th>브랜드평판지수</th>
    </tr>
    <tr>
      <th>혈액형</th>
      <th>성별</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>남자</th>
      <td>175.140</td>
      <td>7591755.20</td>
    </tr>
    <tr>
      <th>여자</th>
      <td>162.100</td>
      <td>5784794.50</td>
    </tr>
    <tr>
      <th>AB</th>
      <th>남자</th>
      <td>176.500</td>
      <td>5687577.50</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>남자</th>
      <td>183.000</td>
      <td>3506027.00</td>
    </tr>
    <tr>
      <th>여자</th>
      <td>NaN</td>
      <td>4668615.00</td>
    </tr>
    <tr>
      <th>O</th>
      <th>남자</th>
      <td>177.875</td>
      <td>3939919.75</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

### 3-2. Multi-Index 데이터 프레임을 피벗테이블로 변환

Multi-Index로 된 데이터프레임을 피벗테이블 형태로 다시 변환해줄 수 있다

> *df_name* **.unstack( *'col_열'* )**
>
> * col_열: groupby에서 선택한 두 column중 pivot table의 열인덱스로 지정해주고 싶은 column명을 입력


```python
df2 = df.groupby(['혈액형', '성별']).mean()
```


```python
df2
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
      <th></th>
      <th>키</th>
      <th>브랜드평판지수</th>
    </tr>
    <tr>
      <th>혈액형</th>
      <th>성별</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>남자</th>
      <td>175.140</td>
      <td>7591755.20</td>
    </tr>
    <tr>
      <th>여자</th>
      <td>162.100</td>
      <td>5784794.50</td>
    </tr>
    <tr>
      <th>AB</th>
      <th>남자</th>
      <td>176.500</td>
      <td>5687577.50</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>남자</th>
      <td>183.000</td>
      <td>3506027.00</td>
    </tr>
    <tr>
      <th>여자</th>
      <td>NaN</td>
      <td>4668615.00</td>
    </tr>
    <tr>
      <th>O</th>
      <th>남자</th>
      <td>177.875</td>
      <td>3939919.75</td>
    </tr>
  </tbody>
</table>

</div>




```python
df2.unstack('혈액형')
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead tr th {
        text-align: left;
    }
    
    .dataframe thead tr:last-of-type th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">키</th>
      <th colspan="4" halign="left">브랜드평판지수</th>
    </tr>
    <tr>
      <th>혈액형</th>
      <th>A</th>
      <th>AB</th>
      <th>B</th>
      <th>O</th>
      <th>A</th>
      <th>AB</th>
      <th>B</th>
      <th>O</th>
    </tr>
    <tr>
      <th>성별</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>남자</th>
      <td>175.14</td>
      <td>176.5</td>
      <td>183.0</td>
      <td>177.875</td>
      <td>7591755.2</td>
      <td>5687577.5</td>
      <td>3506027.0</td>
      <td>3939919.75</td>
    </tr>
    <tr>
      <th>여자</th>
      <td>162.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5784794.5</td>
      <td>NaN</td>
      <td>4668615.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

</div>




```python
df2.unstack('성별')
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead tr th {
        text-align: left;
    }
    
    .dataframe thead tr:last-of-type th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">키</th>
      <th colspan="2" halign="left">브랜드평판지수</th>
    </tr>
    <tr>
      <th>성별</th>
      <th>남자</th>
      <th>여자</th>
      <th>남자</th>
      <th>여자</th>
    </tr>
    <tr>
      <th>혈액형</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>175.140</td>
      <td>162.1</td>
      <td>7591755.20</td>
      <td>5784794.5</td>
    </tr>
    <tr>
      <th>AB</th>
      <td>176.500</td>
      <td>NaN</td>
      <td>5687577.50</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>B</th>
      <td>183.000</td>
      <td>NaN</td>
      <td>3506027.00</td>
      <td>4668615.0</td>
    </tr>
    <tr>
      <th>O</th>
      <td>177.875</td>
      <td>NaN</td>
      <td>3939919.75</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

### 3-3. 인덱스 초기화 (reset_index)

reset_index() 는 Multi-Index로 구성된 데이터 프레임의 **인덱스를 초기화**해 준다

그 의미는 Multi-Index로 구성된 데이터 프레임 중의 index들을 dataframe의 column으로 변환시키는 것

> *df_name* = *df_name* **.reset_index()**


```python
df2
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
      <th></th>
      <th>키</th>
      <th>브랜드평판지수</th>
    </tr>
    <tr>
      <th>혈액형</th>
      <th>성별</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>남자</th>
      <td>175.140</td>
      <td>7591755.20</td>
    </tr>
    <tr>
      <th>여자</th>
      <td>162.100</td>
      <td>5784794.50</td>
    </tr>
    <tr>
      <th>AB</th>
      <th>남자</th>
      <td>176.500</td>
      <td>5687577.50</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>남자</th>
      <td>183.000</td>
      <td>3506027.00</td>
    </tr>
    <tr>
      <th>여자</th>
      <td>NaN</td>
      <td>4668615.00</td>
    </tr>
    <tr>
      <th>O</th>
      <th>남자</th>
      <td>177.875</td>
      <td>3939919.75</td>
    </tr>
  </tbody>
</table>

</div>




```python
df2 = df2.reset_index()
```


```python
df2
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
      <th>혈액형</th>
      <th>성별</th>
      <th>키</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>남자</td>
      <td>175.140</td>
      <td>7591755.20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>여자</td>
      <td>162.100</td>
      <td>5784794.50</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AB</td>
      <td>남자</td>
      <td>176.500</td>
      <td>5687577.50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>B</td>
      <td>남자</td>
      <td>183.000</td>
      <td>3506027.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>B</td>
      <td>여자</td>
      <td>NaN</td>
      <td>4668615.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>O</td>
      <td>남자</td>
      <td>177.875</td>
      <td>3939919.75</td>
    </tr>
  </tbody>
</table>

</div>



<br />

<br />
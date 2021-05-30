---
title: Python >> Pandas 데이터 파악 - (1) Series와 DataFrame
tags:
  - Python
  - Pandas
  - 데이터파악
categories:
  - 【STUDY - Python】
  - Python - 2. Pandas
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
abbrlink: 51068
date: 2020-05-22 20:37:46
---

# **Series & DataFrame**

@[toc]

<br />


## **1. pandas 패키지 로드**


```python
import pandas
```

별칭은 주로 pd로 사용한다


```python
import pandas as pd
```


```python
pd
```


    <module 'pandas' from 'D:\\Anaconda\\lib\\site-packages\\pandas\\__init__.py'>

<br />

 <br /> 

## **2. pandas의 Series 와 DataFrame**

**1차원, 1개의 column은 Series라고 한다**

### 2-1. Series

**Series 생성:** 
* pd.Series("list")

* pd.Series("list_name")

  <br />

(1) pd.Series("list")


```python
pd.Series([1, 2, 3, 4])
```


    0    1
    1    2
    2    3
    3    4
    dtype: int64

<br />

(2) pd.Series("list_name")


```python
a = [1, 2, 3, 4]
```


```python
pd.Series(a)
```


    0    1
    1    2
    2    3
    3    4
    dtype: int64

<br />


```python
mylist = [1, 2, 3, 4]
```


```python
pd.Series(mylist)
```


    0    1
    1    2
    2    3
    3    4
    dtype: int64

<br />

 <br />   

### 2-2. DataFrame

#### 방법 1. list로 만들기


```python
company1 = [['삼성', 2000, '스마트폰'],
           ['현대', 1000, '자동차'],
           ['네이버', 500, '포털']]
```


```python
pd.DataFrame(company1)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>삼성</td>
      <td>2000</td>
      <td>스마트폰</td>
    </tr>
    <tr>
      <th>1</th>
      <td>현대</td>
      <td>1000</td>
      <td>자동차</td>
    </tr>
    <tr>
      <th>2</th>
      <td>네이버</td>
      <td>500</td>
      <td>포털</td>
    </tr>
  </tbody>
</table>
</div>

<br />

<활용을 하기 위해 DataFrame을 변수에 지정하기>


```python
df1 = pd.DataFrame(company1)
```


```python
df1
```
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;<br />
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>삼성</td>
      <td>2000</td>
      <td>스마트폰</td>
    </tr>
    <tr>
      <th>1</th>
      <td>현대</td>
      <td>1000</td>
      <td>자동차</td>
    </tr>
    <tr>
      <th>2</th>
      <td>네이버</td>
      <td>500</td>
      <td>포털</td>
    </tr>
  </tbody>
</table>
</div>


<br />

<제목컬럼 만들기> -- "dfname.column = [ ]"


```python
df1.columns = ['기업명', '매출액', '업종']
```


```python
df1
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
      <th>기업명</th>
      <th>매출액</th>
      <th>업종</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>삼성</td>
      <td>2000</td>
      <td>스마트폰</td>
    </tr>
    <tr>
      <th>1</th>
      <td>현대</td>
      <td>1000</td>
      <td>자동차</td>
    </tr>
    <tr>
      <th>2</th>
      <td>네이버</td>
      <td>500</td>
      <td>포털</td>
    </tr>
  </tbody>
</table>
</div>

<br />

* **주의:** column명의 개수는 반드시 DataFrame의 column수와 동일해야 함   
<br />

#### 방법 2. dict로 만들기


```python
company2 = {'기업명': ['삼성', '현대', '네이버'],  
            '매출액': [2000, 1000, 500],  
            '업종':   ['스므트폰', '자동차', '포털']
            }
```


```python
df2 = pd.DataFrame(company2)
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
      <th>기업명</th>
      <th>매출액</th>
      <th>업종</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>삼성</td>
      <td>2000</td>
      <td>스므트폰</td>
    </tr>
    <tr>
      <th>1</th>
      <td>현대</td>
      <td>1000</td>
      <td>자동차</td>
    </tr>
    <tr>
      <th>2</th>
      <td>네이버</td>
      <td>500</td>
      <td>포털</td>
    </tr>
  </tbody>
</table>
</div>



<br />  

### 2-3. index를 특정column으로 지정하기

"dfname.index = [ ]" 명령을 사용한다


```python
df1
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
      <th>기업명</th>
      <th>매출액</th>
      <th>업종</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>삼성</td>
      <td>2000</td>
      <td>스마트폰</td>
    </tr>
    <tr>
      <th>1</th>
      <td>현대</td>
      <td>1000</td>
      <td>자동차</td>
    </tr>
    <tr>
      <th>2</th>
      <td>네이버</td>
      <td>500</td>
      <td>포털</td>
    </tr>
  </tbody>
</table>
</div>

<br />


```python
df1.index = df1['기업명']
```


```python
df1
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
      <th>기업명</th>
      <th>매출액</th>
      <th>업종</th>
    </tr>
    <tr>
      <th>기업명</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>삼성</th>
      <td>삼성</td>
      <td>2000</td>
      <td>스마트폰</td>
    </tr>
    <tr>
      <th>현대</th>
      <td>현대</td>
      <td>1000</td>
      <td>자동차</td>
    </tr>
    <tr>
      <th>네이버</th>
      <td>네이버</td>
      <td>500</td>
      <td>포털</td>
    </tr>
  </tbody>
</table>
</div>



<br />  

### 2-4. column = Series


```python
df1['매출액']
```


    기업명
    삼성     2000
    현대     1000
    네이버     500
    Name: 매출액, dtype: int64

<br />


```python
type(df1['매출액'])
```


    pandas.core.series.Series

<br />

<br />
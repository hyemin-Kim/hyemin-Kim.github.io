---
title: Python >> Pandas 전처리 - (5) column 값을 변환시키는 방법
tags:
  - Python
  - Pandas
  - 전처리
categories: 
  - [【STUDY - Python】, Python - 2. Pandas]
  - [【STUDY - Python】, Python - 전처리]
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
description: apply (일반 함수 / lambda 함수); map (map 함수)
abbrlink: 57472
date: 2020-06-19 21:11:52
---

# DataFrame의 column 값을 변환시키는 방법

@[toc]

<br />


```python
import pandas as pd
```


```python
df = pd.read_csv('korean-idol.csv')
```

  <br />

## **1. apply + 일반 함수**

> apply는 Series나 DataFrame에 좀 더 **구체적인 로직**을 적용하고 싶은 경우 활용한다
>
> * apply를 적용하기 위해서는 함수가 먼저 정의되어야한다
> * apply는 정의한 로직 함수를 인자로 넘겨준다

> * **Series에 적용할 경우:**  
>   *df_name* [ "*col_name*" ] **.apply( *func* )**
>
> * **DataFrame에 적용할 경우:**  
>   *df_name* **.apply( *func*, axis = 1)** 

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

<table  >
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

### 1-1. (목표) '성별' column의 "남자" / "여자"를 1 / 2로 바꾼다

**변환 규칙:**  
남자: 1   여자: 2   기타: -1 

<br />

**(1) 로직 함수 정의**

**[주의] 반드시 return 값이 존재**하여야한다


```python
def male_or_female(x):
    if x == "남자":
        return 1
    elif x == "여자":
        return 2
```

 <br /> 

**(2) apply로 DataFrame에 적용**


```python
df["성별_NEW"] = df["성별"].apply(male_or_female)
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

<table  >
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
      <th>성별_NEW</th>
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
      <td>1</td>
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
      <td>1</td>
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
      <td>1</td>
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
      <td>1</td>
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
      <td>2</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

### 1-2. (목표) cm당 브랜드 평판지수를 구한다 (브랜드평판지수 / 키)

**변환 규칙:**  
키: 178  브랜드평판지수: 99000  
값: 99000 / 178

<br />

**(1) 로직 함수 정의**


```python
def cm_to_brand(df):
    value = df["브랜드평판지수"] / df["키"]
    return value
```

  <br />

**(2) apply로 DataFrame에 적용**


```python
df.apply(cm_to_brand, axis = 1)
```


    0     60617.857143
    1     56027.949153
    2     45965.250000
    3     45356.747191
    4     47198.815546
    5     29260.308989
    6     27371.321997
    7              NaN
    8     25503.950893
    9     24156.128067
    10             NaN
    11    19158.617486
    12    18866.594286
    13    18603.051136
    14    16812.885057
    dtype: float64



 <br />

<br /> 

## **2. apply + lamda 함수**

> *df_name* [ "*col_name*" ] **.apply (*lambda_func*)**

> * lambda는 1줄로 작성하는 간단 함수식이다
> * return을 별도로 멱기하지 않는다

 <br /> 

**(1) male_or_female 함수**


```python
male_or_female = lambda x: 1 if x == "남자" else 0
```


```python
df["성별"].apply(male_or_female)
```


    0     1
    1     1
    2     1
    3     1
    4     0
    5     1
    6     1
    7     0
    8     1
    9     1
    10    0
    11    1
    12    1
    13    1
    14    1
    Name: 성별, dtype: int64



<br />  

**(2) 실제로는 간단한 계산식을 적용하려는 경우에 많이 사용한다**


```python
df["키/2"] = df["키"].apply(lambda x: x / 2)
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

<table  >
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
      <th>성별_NEW</th>
      <th>키/2</th>
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
      <td>1</td>
      <td>86.80</td>
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
      <td>1</td>
      <td>88.50</td>
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
      <td>1</td>
      <td>90.00</td>
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
      <td>1</td>
      <td>89.00</td>
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
      <td>2</td>
      <td>81.05</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> 

apply에 함수식을 만들어서 적용해주는 것과 동일하기 때문에, **복잠한 조건식은 <함수>로, 간단한 계산식은 < lambda > 로** 적용하면 된다

 <br /><br /> 

## **3. map + map 함수**

> *df_name* [ "*col_name*" ] **.map ( *map_func* )**

> **Step 1:** dictionary 형식으로 map 함수를 정의하기  
> **Step 2:** DataFrame / Series에 map 함수를 적용 

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

<table  >
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
      <th>성별_NEW</th>
      <th>키/2</th>
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
      <td>1</td>
      <td>86.80</td>
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
      <td>1</td>
      <td>88.50</td>
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
      <td>1</td>
      <td>90.00</td>
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
      <td>1</td>
      <td>89.00</td>
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
      <td>2</td>
      <td>81.05</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
my_map = {
    "남자": "male",
    "여자": "female"
}
```


```python
df["성별"].map(my_map)
```


    0       male
    1       male
    2       male
    3       male
    4     female
    5       male
    6       male
    7     female
    8       male
    9       male
    10    female
    11      male
    12      male
    13      male
    14      male
    Name: 성별, dtype: object

<br />

<br />
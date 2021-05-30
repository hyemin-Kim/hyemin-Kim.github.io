---
title: Python >> Pandas 전처리 - (4) Series의 Type 변환하기
tags:
  - Python
  - Pandas
  - 전처리
categories: 
  - [【STUDY - Python】, Python - 2. Pandas]
  - [【STUDY - Python】, Python - 전처리]
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
descroption: 일반 타입의 변환; 날짜 (datatime) 타입의 변환
abbrlink: 31584
date: 2020-06-19 15:53:13
---

# Series의 Type 변환하기

  @[toc]

<br />


```python
import pandas as pd
```


```python
df = pd.read_csv('korean-idol.csv')
```

 <br /> 

## **1. Series의 Type**

### 1-1. Type 확인하기

> ***df_name*.info()** 명령어를 사용하여 Dataframe의 Series Type을 확인할 수 있다  
> ***df_name* [ "*col_name*" ] .dtypes** 명령어를 사용하여 특정 Series의 Type을 확인할 수 있다

> **Series Type**
>
> * object: 일반 문자영 타입
> * float: 실수
> * int: 정수
> * category: 카테고리
> * datatime: 시간

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
  </tbody>
</table>

</div>




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
df["이름"].dtypes
```


    dtype('O')

<br />

  

### 1-2. Type 변환하기

> *df_name* [ "*col_name*" ] **.astype(...)**

<br />

**e.g.**  "키" column을 float에서 int로 변환해보기 


```python
df["키"].astype(int)
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-12-c145a39acdb2> in <module>
    ----> 1 df["키"].astype(int)


    D:\Anaconda\lib\site-packages\pandas\core\generic.py in astype(self, dtype, copy, errors)
       5696         else:
       5697             # else, only a single dtype is given
    -> 5698             new_data = self._data.astype(dtype=dtype, copy=copy, errors=errors)
       5699             return self._constructor(new_data).__finalize__(self)
       5700 


    D:\Anaconda\lib\site-packages\pandas\core\internals\managers.py in astype(self, dtype, copy, errors)
        580 
        581     def astype(self, dtype, copy: bool = False, errors: str = "raise"):
    --> 582         return self.apply("astype", dtype=dtype, copy=copy, errors=errors)
        583 
        584     def convert(self, **kwargs):


    D:\Anaconda\lib\site-packages\pandas\core\internals\managers.py in apply(self, f, filter, **kwargs)
        440                 applied = b.apply(f, **kwargs)
        441             else:
    --> 442                 applied = getattr(b, f)(**kwargs)
        443             result_blocks = _extend_blocks(applied, result_blocks)
        444 


    D:\Anaconda\lib\site-packages\pandas\core\internals\blocks.py in astype(self, dtype, copy, errors)
        623             vals1d = values.ravel()
        624             try:
    --> 625                 values = astype_nansafe(vals1d, dtype, copy=True)
        626             except (ValueError, TypeError):
        627                 # e.g. astype_nansafe can fail on object-dtype of strings


    D:\Anaconda\lib\site-packages\pandas\core\dtypes\cast.py in astype_nansafe(arr, dtype, copy, skipna)
        866 
        867         if not np.isfinite(arr).all():
    --> 868             raise ValueError("Cannot convert non-finite values (NA or inf) to integer")
        869 
        870     elif is_object_dtype(arr):


    ValueError: Cannot convert non-finite values (NA or inf) to integer

<br />

"키" column에 NaN값이 존재하기 때문에 Error 발생!

<br />

> **column에 NaN 값이 있는 경우:** 면저 NaN 값을 다른 값으로 대체한 후 Type을 변환할 수 있다


```python
df["키"] = df["키"].fillna(-1)
```


```python
df["키"]
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


```python
df["키"].astype(int)
```


    0     173
    1     177
    2     180
    3     178
    4     162
    5     178
    6     182
    7      -1
    8     179
    9     167
    10     -1
    11    183
    12    175
    13    176
    14    174
    Name: 키, dtype: int32



<br />

  

### 1-3. 날짜 (datatime) 타입 변환하기

**(1) datetime 타입으로 변환하기**

> **pd.to_datetime** ( *df_name* [ "*col_nema*"] )


```python
df["생년월일"]
```


    0     1995-10-13
    1     1988-08-18
    2     1996-12-10
    3     1995-12-30
    4     1995-07-23
    5     1997-09-01
    6     1995-08-09
    7     1998-08-26
    8     1992-12-04
    9     1994-03-22
    10    1989-03-09
    11    1997-03-30
    12    1995-07-21
    13    1995-06-08
    14    1993-03-09
    Name: 생년월일, dtype: object

<br />


```python
pd.to_datetime(df["생년월일"])
```


    0    1995-10-13
    1    1988-08-18
    2    1996-12-10
    3    1995-12-30
    4    1995-07-23
    5    1997-09-01
    6    1995-08-09
    7    1998-08-26
    8    1992-12-04
    9    1994-03-22
    10   1989-03-09
    11   1997-03-30
    12   1995-07-21
    13   1995-06-08
    14   1993-03-09
    Name: 생년월일, dtype: datetime64[ns]

<br />변환된 것을 **원래 column에 다시 대입을 해줘야** 정상적으로 변환된 값이 들어간다


```python
df["생년월일"] = pd.to_datetime(df["생년월일"])
df["생년월일"]
```


    0    1995-10-13
    1    1988-08-18
    2    1996-12-10
    3    1995-12-30
    4    1995-07-23
    5    1997-09-01
    6    1995-08-09
    7    1998-08-26
    8    1992-12-04
    9    1994-03-22
    10   1989-03-09
    11   1997-03-30
    12   1995-07-21
    13   1995-06-08
    14   1993-03-09
    Name: 생년월일, dtype: datetime64[ns]



<br />  

**(2) datatime 타입을 활용하기**

> ***df_name* [ "*datetime_col*" ] .dt**  
> 을 활용하여 매우 손쉽게 **년, 월, 일, 요일** 등등 날짜 정보를 세부적으로 **추출**해낼 수 있다

> * 년: *df_name* [ "*datetime_col*" ] **.dt.year**
> * 월: *df_name* [ "*datetime_col*" ] **.dt.month**
> * 일: *df_name* [ "*datetime_col*" ] **.dt.day**
> * 요일: *df_name* [ "*datetime_col*" ] **.dt.dayofweek**
> * 주: *df_name* [ "*datetime_col*" ] **.dt.weekofyear**

<br />

```python
df["생년월일"]
```


    0    1995-10-13
    1    1988-08-18
    2    1996-12-10
    3    1995-12-30
    4    1995-07-23
    5    1997-09-01
    6    1995-08-09
    7    1998-08-26
    8    1992-12-04
    9    1994-03-22
    10   1989-03-09
    11   1997-03-30
    12   1995-07-21
    13   1995-06-08
    14   1993-03-09
    Name: 생년월일, dtype: datetime64[ns]



  <br />

**년 추출:**


```python
df["생년월일"].dt.year
```


    0     1995
    1     1988
    2     1996
    3     1995
    4     1995
    5     1997
    6     1995
    7     1998
    8     1992
    9     1994
    10    1989
    11    1997
    12    1995
    13    1995
    14    1993
    Name: 생년월일, dtype: int64

<br />

**월 추출:**


```python
df["생년월일"].dt.month
```


    0     10
    1      8
    2     12
    3     12
    4      7
    5      9
    6      8
    7      8
    8     12
    9      3
    10     3
    11     3
    12     7
    13     6
    14     3
    Name: 생년월일, dtype: int64



<br />  

**일 추출:**


```python
df["생년월일"].dt.day
```


    0     13
    1     18
    2     10
    3     30
    4     23
    5      1
    6      9
    7     26
    8      4
    9     22
    10     9
    11    30
    12    21
    13     8
    14     9
    Name: 생년월일, dtype: int64



 <br /> 

**요일 추출:**

> 월 [0],  화 [1],  수 [2],  목 [3],  금 [4],  토 [5],  일 [6]


```python
df["생년월일"].dt.dayofweek
```


    0     4
    1     3
    2     1
    3     5
    4     6
    5     0
    6     2
    7     2
    8     4
    9     1
    10    3
    11    6
    12    4
    13    3
    14    1
    Name: 생년월일, dtype: int64



 <br /> 

**주 추출:**


```python
df["생년월일"].dt.weekofyear
```


    0     41
    1     33
    2     50
    3     52
    4     29
    5     36
    6     32
    7     35
    8     49
    9     12
    10    10
    11    13
    12    29
    13    23
    14    10
    Name: 생년월일, dtype: int64



<br />

<br />
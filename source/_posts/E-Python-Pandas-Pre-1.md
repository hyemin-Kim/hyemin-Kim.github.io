---
title: 【실습】 Python >> Pandas 전처리 -- 부동산 데이터
tags:
  - Python
  - Pandas
  - 전처리
categories:
  - 【EXERCISE】
  - Python
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
description: column 이름 제정의; Data Overview; 특수부호 처리; 데이터 타입 바꾸기; groupby; 피벗테이블
abbrlink: 38036
date: 2020-06-22 19:14:57
---

# <Pandas 전처리> 실습 -- 부동산 데이터

@[toc]

<br />


```python
import pandas as pd
```

  <br />

## **0. 샘플데이터**

[공공데이터포털](https://www.data.go.kr/) 에서 제공하는 공공데이터 "민간 아파트 가격동향" 를 활용한다.

<br />


```python
df = pd.read_csv("seoul_house_price.csv")
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격(㎡)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>전용면적 60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4500</th>
      <td>제주</td>
      <td>전체</td>
      <td>2020</td>
      <td>2</td>
      <td>3955</td>
    </tr>
    <tr>
      <th>4501</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>4039</td>
    </tr>
    <tr>
      <th>4502</th>
      <td>제주</td>
      <td>전용면적 60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3962</td>
    </tr>
    <tr>
      <th>4503</th>
      <td>제주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4504</th>
      <td>제주</td>
      <td>전용면적 102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>3601</td>
    </tr>
  </tbody>
</table>
<p>4505 rows × 5 columns</p>

</div>



<br /><br />    

## **1. column 이름 제정의 (rename)**

**[목표] 분양가격 column의 이름을 재정의:**

> "분양가격(m^2^)​" --> "분양가격"

<br />

```python
df = df.rename(columns = {"분양가격(㎡)" : "분양가격"})
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>전용면적 60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4500</th>
      <td>제주</td>
      <td>전체</td>
      <td>2020</td>
      <td>2</td>
      <td>3955</td>
    </tr>
    <tr>
      <th>4501</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>4039</td>
    </tr>
    <tr>
      <th>4502</th>
      <td>제주</td>
      <td>전용면적 60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3962</td>
    </tr>
    <tr>
      <th>4503</th>
      <td>제주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4504</th>
      <td>제주</td>
      <td>전용면적 102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>3601</td>
    </tr>
  </tbody>
</table>
<p>4505 rows × 5 columns</p>

</div>

<br />

 <br />

  

## **2. Data Overview**

### 2-1. Data Shape 확인하기


```python
df.shape
```


    (4505, 5)

<br />

  

### 2-2. 걸측값과 Data Type 확인하기


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4505 entries, 0 to 4504
    Data columns (total 5 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   지역명     4505 non-null   object
     1   규모구분    4505 non-null   object
     2   연도      4505 non-null   int64 
     3   월       4505 non-null   int64 
     4   분양가격    4210 non-null   object
    dtypes: int64(2), object(3)
    memory usage: 176.1+ KB

<br />


### 2-3. 통계값 확인하기


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

<table>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>연도</th>
      <th>월</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4505.000000</td>
      <td>4505.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2017.452830</td>
      <td>6.566038</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.311432</td>
      <td>3.595519</td>
    </tr>
    <tr>
      <th>min</th>
      <td>2015.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2016.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2017.000000</td>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2019.000000</td>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2020.000000</td>
      <td>12.000000</td>
    </tr>
  </tbody>
</table>


</div>

<br />

 <br />

  

## **3. 데이터 타입 변환**

**[목표] <object 타입>으로 되어있는 "분양가격"을 <int 타입>으로 변환하기**

<br />


```python
df["분양가격"].astype(int)
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-193-5870dcdf031c> in <module>
    ----> 1 df["분양가격"].astype(int)


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
        872         # work around NumPy brokenness, #1987
        873         if np.issubdtype(dtype.type, np.integer):
    --> 874             return lib.astype_intsafe(arr.ravel(), dtype).reshape(arr.shape)
        875 
        876         # if we have a datetime/timedelta array of objects


    pandas\_libs\lib.pyx in pandas._libs.lib.astype_intsafe()


    ValueError: invalid literal for int() with base 10: '  '

<br />


> !! "분양가격" column에 <font color = "blue">"2칸 공백" 값이 있어서</font> Error가 납니다

  <br />

### 3-1. str.strip()을 활용하여 공백이 있는 데이터의 공백 없애기 

> *df_name* [ "*col_name*" ] **.str.strip()**

<br />

```python
df.loc[df["분양가격"] == '  ']
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>28</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>29</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>34</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>81</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>113</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>114</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>119</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>166</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>198</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>199</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>204</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>251</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>283</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>284</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>289</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>336</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
df["분양가격"] = df["분양가격"].str.strip('  ')
```


```python
df.loc[df["분양가격"] == "  "]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

</div>



<br />  

### 3-2. 빈 공백에 0을 넣어주기 


```python
df.loc[df["분양가격"] == '', "분양가격"] = 0
```


```python
df["분양가격"].astype(int)
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-198-5870dcdf031c> in <module>
    ----> 1 df["분양가격"].astype(int)


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
        872         # work around NumPy brokenness, #1987
        873         if np.issubdtype(dtype.type, np.integer):
    --> 874             return lib.astype_intsafe(arr.ravel(), dtype).reshape(arr.shape)
        875 
        876         # if we have a datetime/timedelta array of objects


    pandas\_libs\lib.pyx in pandas._libs.lib.astype_intsafe()


    ValueError: cannot convert float NaN to integer

<br />


> !! "분양가격" column에 <font color = 'blue'>"NaN" 값이 있어서</font> Error가 또 납니다 ㅠㅠ

<br />  

### 3-3. NaN 값은 fillna로 채워주기


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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>전용면적 60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4500</th>
      <td>제주</td>
      <td>전체</td>
      <td>2020</td>
      <td>2</td>
      <td>3955</td>
    </tr>
    <tr>
      <th>4501</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>4039</td>
    </tr>
    <tr>
      <th>4502</th>
      <td>제주</td>
      <td>전용면적 60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3962</td>
    </tr>
    <tr>
      <th>4503</th>
      <td>제주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4504</th>
      <td>제주</td>
      <td>전용면적 102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>3601</td>
    </tr>
  </tbody>
</table>
<p>4505 rows × 5 columns</p>

</div>

<br />


```python
df.loc[df["분양가격"].isna()]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>368</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>369</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>374</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>388</th>
      <td>강원</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>421</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4461</th>
      <td>세종</td>
      <td>전용면적 60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4488</th>
      <td>전남</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4493</th>
      <td>경북</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4499</th>
      <td>경남</td>
      <td>전용면적 102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4503</th>
      <td>제주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>295 rows × 5 columns</p>

</div>

<br />


```python
df["분양가격"] = df["분양가격"].fillna(0)
```


```python
df.loc[df["분양가격"].isna()]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

</div>

<br />

  


```python
df["분양가격"].astype(int)
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-203-5870dcdf031c> in <module>
    ----> 1 df["분양가격"].astype(int)


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
        872         # work around NumPy brokenness, #1987
        873         if np.issubdtype(dtype.type, np.integer):
    --> 874             return lib.astype_intsafe(arr.ravel(), dtype).reshape(arr.shape)
        875 
        876         # if we have a datetime/timedelta array of objects


    pandas\_libs\lib.pyx in pandas._libs.lib.astype_intsafe()


    ValueError: invalid literal for int() with base 10: '6,657'

<br />


> !! 이번에는 <font color='blue'>","가 들어간</font> 데이터가 문제네요..

  <br />

### 3-4. str.replace() 를 활용하여 콤마를 제거하기


```python
df.loc[df["분양가격"] == "6,657"]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2125</th>
      <td>서울</td>
      <td>전체</td>
      <td>2017</td>
      <td>11</td>
      <td>6,657</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
df["분양가격"] = df["분양가격"].str.replace(',', '')
```


```python
df["분양가격"].astype(int)
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-206-5870dcdf031c> in <module>
    ----> 1 df["분양가격"].astype(int)


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
        872         # work around NumPy brokenness, #1987
        873         if np.issubdtype(dtype.type, np.integer):
    --> 874             return lib.astype_intsafe(arr.ravel(), dtype).reshape(arr.shape)
        875 
        876         # if we have a datetime/timedelta array of objects


    pandas\_libs\lib.pyx in pandas._libs.lib.astype_intsafe()


    ValueError: cannot convert float NaN to integer

<br />


> !! 다시 NaN값이 생겨서 fillna로 채워줍니다.


```python
df["분양가격"] = df["분양가격"].fillna(0)
```


```python
df["분양가격"].astype(int)
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-208-5870dcdf031c> in <module>
    ----> 1 df["분양가격"].astype(int)


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
        872         # work around NumPy brokenness, #1987
        873         if np.issubdtype(dtype.type, np.integer):
    --> 874             return lib.astype_intsafe(arr.ravel(), dtype).reshape(arr.shape)
        875 
        876         # if we have a datetime/timedelta array of objects


    pandas\_libs\lib.pyx in pandas._libs.lib.astype_intsafe()


    ValueError: invalid literal for int() with base 10: '-'

<br />


> !! 이번에는 <font color = 'blue'>"-"가</font> 멀썽이네요..

 <br />

  

### 3-5. str.replace()를 활용하여 "-" 제거하기


```python
df["분양가격"] = df["분양가격"].str.replace("-", "")
```


```python
df.loc[df["분양가격"] == "", "분양가격"] = 0
```


```python
df["분양가격"].astype(int)
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-211-5870dcdf031c> in <module>
    ----> 1 df["분양가격"].astype(int)


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
        872         # work around NumPy brokenness, #1987
        873         if np.issubdtype(dtype.type, np.integer):
    --> 874             return lib.astype_intsafe(arr.ravel(), dtype).reshape(arr.shape)
        875 
        876         # if we have a datetime/timedelta array of objects


    pandas\_libs\lib.pyx in pandas._libs.lib.astype_intsafe()


    ValueError: cannot convert float NaN to integer

<br />

```python
df["분양가격"] = df["분양가격"].fillna(0)
```


```python
df["분양가격"] = df["분양가격"].astype(int)
```


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4505 entries, 0 to 4504
    Data columns (total 5 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   지역명     4505 non-null   object
     1   규모구분    4505 non-null   object
     2   연도      4505 non-null   int64 
     3   월       4505 non-null   int64 
     4   분양가격    4505 non-null   int32 
    dtypes: int32(1), int64(2), object(2)
    memory usage: 158.5+ KB

<br />


> 이제 드디어 "분양가격" column의 Type을 int로 성공적으로 바꿨습니다!!!

<br />

### 3-6. 규모구분 column에 불필요한 "전용면적" 제거하기


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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>전용면적 60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
  </tbody>
</table>

</div>

 <br />


```python
df["규모구분"] = df["규모구분"].str.replace("전용면적", "")
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

<table>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
  </tbody>
</table>

</div>

 <br />

   <br />

  

## **4. 전처리 내용 복습하기**

**방급 진행 했던 전처리 과정을 복습해봅시다!**


```python
df2 = pd.read_csv("seoul_house_price.csv")
```

   <br />

**(1) 콤마가 있는 경우**

> *df_name* [ "*col_name*" ] **.str.replace** (',', '')

 <br />

```python
df2.iloc[2125]
```


    지역명           서울
    규모구분          전체
    연도          2017
    월             11
    분양가격(㎡)    6,657
    Name: 2125, dtype: object

 <br />


```python
df2 = df2.rename(columns = {"분양가격(㎡)" : "분양가격"})
```


```python
df2["분양가격"] = df2["분양가격"].str.replace(",", "")
```


```python
df2.iloc[2125]
```


    지역명       서울
    규모구분      전체
    연도      2017
    월         11
    분양가격    6657
    Name: 2125, dtype: object

 <br />

  

**(2) - 가 있는 경우**

> *df_name* [ "*col_name*" ] **.str.replace('-', '')

 <br />

```python
df2.loc[df2["분양가격"] == "-"]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3683</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td>-</td>
    </tr>
    <tr>
      <th>3686</th>
      <td>대전</td>
      <td>전용면적 60㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td>-</td>
    </tr>
    <tr>
      <th>3688</th>
      <td>대전</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td>-</td>
    </tr>
    <tr>
      <th>3690</th>
      <td>울산</td>
      <td>전체</td>
      <td>2019</td>
      <td>5</td>
      <td>-</td>
    </tr>
    <tr>
      <th>3691</th>
      <td>울산</td>
      <td>전용면적 60㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td>-</td>
    </tr>
    <tr>
      <th>3692</th>
      <td>울산</td>
      <td>전용면적 60㎡초과 85㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td>-</td>
    </tr>
    <tr>
      <th>3693</th>
      <td>울산</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td>-</td>
    </tr>
    <tr>
      <th>3694</th>
      <td>울산</td>
      <td>전용면적 102㎡초과</td>
      <td>2019</td>
      <td>5</td>
      <td>-</td>
    </tr>
    <tr>
      <th>3696</th>
      <td>세종</td>
      <td>전용면적 60㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td>-</td>
    </tr>
  </tbody>
</table>

</div>

 <br />


```python
df2["분양가격"] = df2["분양가격"].str.replace("-", "")
```


```python
df2.loc[df2["분양가격"] == "-"]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

</div>

 <br />

  

**(3) 공백이 2개 들어간 경우**

> *df_name* [ "*col_name*" ] **.str.strip("  ")

 <br />

```python
df2.loc[df2["분양가격"] == "  "]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>28</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>29</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>34</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>81</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>113</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>114</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>119</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>166</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>198</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>199</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>204</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>251</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>283</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>284</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>289</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>336</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
  </tbody>
</table>

</div>

 <br />


```python
df2["분양가격"] = df2["분양가격"].str.strip("  ")
```


```python
df2.loc[df2["분양가격"] == "  "]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

</div>



  <br /> 

**(4) 빈 칸을 0으로 채우기**

> *df_name*.loc [ *df_name* [ "*col_name*" ] == "" , "*col_name*"] = 0

 <br />

```python
df2.loc[df2["분양가격"] == ""]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>28</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>29</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>34</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>81</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td></td>
    </tr>
    <tr>
      <th>113</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>114</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>119</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>166</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>11</td>
      <td></td>
    </tr>
    <tr>
      <th>198</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>199</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>204</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>251</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2015</td>
      <td>12</td>
      <td></td>
    </tr>
    <tr>
      <th>283</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>284</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>289</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>336</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2016</td>
      <td>1</td>
      <td></td>
    </tr>
    <tr>
      <th>3683</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td></td>
    </tr>
    <tr>
      <th>3686</th>
      <td>대전</td>
      <td>전용면적 60㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td></td>
    </tr>
    <tr>
      <th>3688</th>
      <td>대전</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td></td>
    </tr>
    <tr>
      <th>3690</th>
      <td>울산</td>
      <td>전체</td>
      <td>2019</td>
      <td>5</td>
      <td></td>
    </tr>
    <tr>
      <th>3691</th>
      <td>울산</td>
      <td>전용면적 60㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td></td>
    </tr>
    <tr>
      <th>3692</th>
      <td>울산</td>
      <td>전용면적 60㎡초과 85㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td></td>
    </tr>
    <tr>
      <th>3693</th>
      <td>울산</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td></td>
    </tr>
    <tr>
      <th>3694</th>
      <td>울산</td>
      <td>전용면적 102㎡초과</td>
      <td>2019</td>
      <td>5</td>
      <td></td>
    </tr>
    <tr>
      <th>3696</th>
      <td>세종</td>
      <td>전용면적 60㎡이하</td>
      <td>2019</td>
      <td>5</td>
      <td></td>
    </tr>
  </tbody>
</table>

</div>

 <br />


```python
df2.loc[df2["분양가격"] == "", "분양가격"] = 0
```


```python
df2.loc[df2["분양가격"] == ""]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

</div>



 <br />  

**(5) NaN 값을 0으로 바꾸기**

> *df_name*.loc [ *df_name* [ "*col_name*" ] **.isna()** ]  
> *df_name* [ "*col_name*" ].fillna(0)

 <br />

```python
df2.loc[df2["분양가격"].isna()]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>368</th>
      <td>광주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>369</th>
      <td>광주</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>374</th>
      <td>대전</td>
      <td>전용면적 102㎡초과</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>388</th>
      <td>강원</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>421</th>
      <td>제주</td>
      <td>전용면적 60㎡이하</td>
      <td>2016</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4461</th>
      <td>세종</td>
      <td>전용면적 60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4488</th>
      <td>전남</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4493</th>
      <td>경북</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4499</th>
      <td>경남</td>
      <td>전용면적 102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4503</th>
      <td>제주</td>
      <td>전용면적 85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>295 rows × 5 columns</p>

</div>

 <br />


```python
df2["분양가격"] = df2["분양가격"].fillna(0)
```


```python
df2.loc[df2["분양가격"].isna()]
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

</div>



 <br />  

**(6) column type 바꾸기** 

> *df_name* [ "*col_name*" ] **.astype(...)**

 <br />

```python
df2["분양가격"].astype(int)
```


    0       5841
    1       5652
    2       5882
    3       5721
    4       5879
            ... 
    4500    3955
    4501    4039
    4502    3962
    4503       0
    4504    3601
    Name: 분양가격, Length: 4505, dtype: int32

 <br />

   <br />

  

## **5. 지역별 분양가격을 확인해보기**


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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4500</th>
      <td>제주</td>
      <td>전체</td>
      <td>2020</td>
      <td>2</td>
      <td>3955</td>
    </tr>
    <tr>
      <th>4501</th>
      <td>제주</td>
      <td>60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>4039</td>
    </tr>
    <tr>
      <th>4502</th>
      <td>제주</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3962</td>
    </tr>
    <tr>
      <th>4503</th>
      <td>제주</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4504</th>
      <td>제주</td>
      <td>102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>3601</td>
    </tr>
  </tbody>
</table>
<p>4505 rows × 5 columns</p>

</div>

 <br />


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4505 entries, 0 to 4504
    Data columns (total 5 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   지역명     4505 non-null   object
     1   규모구분    4505 non-null   object
     2   연도      4505 non-null   int64 
     3   월       4505 non-null   int64 
     4   분양가격    4505 non-null   int32 
    dtypes: int32(1), int64(2), object(2)
    memory usage: 158.5+ KB

 <br />


### 5-1. 지역별 평균 분양가격 확인해보기


```python
df.groupby("지역명")["분양가격"].mean()
```


    지역명
    강원    2339.807547
    경기    4072.667925
    경남    2761.275472
    경북    2432.128302
    광주    2450.728302
    대구    3538.920755
    대전    2479.135849
    부산    3679.920755
    서울    7225.762264
    세종    2815.098113
    울산    1826.101887
    인천    3578.433962
    전남    2270.177358
    전북    2322.060377
    제주    2979.407547
    충남    2388.324528
    충북    2316.871698
    Name: 분양가격, dtype: float64



  <br /> 

### 5-2. 분양가격이 100보다 작은 행을 제거해보기

> 특정 조건에 만족하는 행을 제거하고자 할 때는  
>
> 1. index를 list로 가져온다 
>    * *idx* = df.loc [ *조건식* ] **.index**   
> 2. drop을 활용하여 행을 제거한다
>    * *df_name* = *df_name* **.drop** (*idx*, axis = 0) 

 <br />

```python
idx = df.loc[df["분양가격"] < 100].index
```


```python
idx
```


    Int64Index([  28,   29,   34,   81,  113,  114,  119,  166,  198,  199,
                ...
                4418, 4448, 4453, 4458, 4459, 4461, 4488, 4493, 4499, 4503],
               dtype='int64', length=320)

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

<table>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4500</th>
      <td>제주</td>
      <td>전체</td>
      <td>2020</td>
      <td>2</td>
      <td>3955</td>
    </tr>
    <tr>
      <th>4501</th>
      <td>제주</td>
      <td>60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>4039</td>
    </tr>
    <tr>
      <th>4502</th>
      <td>제주</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3962</td>
    </tr>
    <tr>
      <th>4503</th>
      <td>제주</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4504</th>
      <td>제주</td>
      <td>102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>3601</td>
    </tr>
  </tbody>
</table>
<p>4505 rows × 5 columns</p>

</div>

 <br />


```python
df = df.drop(idx, axis = 0)
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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4498</th>
      <td>경남</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3247</td>
    </tr>
    <tr>
      <th>4500</th>
      <td>제주</td>
      <td>전체</td>
      <td>2020</td>
      <td>2</td>
      <td>3955</td>
    </tr>
    <tr>
      <th>4501</th>
      <td>제주</td>
      <td>60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>4039</td>
    </tr>
    <tr>
      <th>4502</th>
      <td>제주</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3962</td>
    </tr>
    <tr>
      <th>4504</th>
      <td>제주</td>
      <td>102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>3601</td>
    </tr>
  </tbody>
</table>
<p>4185 rows × 5 columns</p>

</div>



   <br />

다시 한 번 지역명으로 group을 묶어 분양가격을 확인해보자!


```python
df.groupby("지역명")["분양가격"].mean()
```


    지역명
    강원    2412.642023
    경기    4072.667925
    경남    2814.376923
    경북    2547.486166
    광주    3049.028169
    대구    3663.335938
    대전    3128.433333
    부산    3679.920755
    서울    7225.762264
    세종    2984.004000
    울산    3043.503145
    인천    3633.275862
    전남    2304.969349
    전북    2348.648855
    제주    3432.795652
    충남    2501.604743
    충북    2316.871698
    Name: 분양가격, dtype: float64

 <br />

  

### 5-3. 지역별 "분양가격" 데이터의 갯수를 확인해보기


```python
df.groupby("지역명")["분양가격"].count()
```


    지역명
    강원    257
    경기    265
    경남    260
    경북    253
    광주    213
    대구    256
    대전    210
    부산    265
    서울    265
    세종    250
    울산    159
    인천    261
    전남    261
    전북    262
    제주    230
    충남    253
    충북    265
    Name: 분양가격, dtype: int64



 <br />  

### 5-4. 지역별 제일 비싼 분양가를 확인해보기


```python
df.groupby("지역명")["분양가격"].max()
```


    지역명
    강원     3906
    경기     5670
    경남     4303
    경북     3457
    광주     4881
    대구     5158
    대전     4877
    부산     4623
    서울    13835
    세종     3931
    울산     3594
    인천     5188
    전남     3053
    전북     3052
    제주     5462
    충남     3201
    충북     2855
    Name: 분양가격, dtype: int32



  <br />  <br />

  

## **6. 연도별 평균 분양가격을 확인해보기**


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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
  </tbody>
</table>

</div>

 <br />


```python
df.groupby("연도")["분양가격"].mean()
```


    연도
    2015    2788.707819
    2016    2934.250000
    2017    3143.311795
    2018    3326.951034
    2019    3693.422149
    2020    3853.960526
    Name: 분양가격, dtype: float64

 <br />

   <br />

  

## **7. 피벗테이블 활용하기**

* **행 인덱스:** 연도

* **열 인덱스:** 규모구분

* **값:** 분양가 (평균)

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
      <th>지역명</th>
      <th>규모구분</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>전체</td>
      <td>2015</td>
      <td>10</td>
      <td>5841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
  </tbody>
</table>

</div>

 <br />


```python
pd.pivot_table(df, index = "연도", columns = "규모구분", values = "분양가격")
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
      <th>규모구분</th>
      <th>102㎡초과</th>
      <th>60㎡이하</th>
      <th>60㎡초과 85㎡이하</th>
      <th>85㎡초과 102㎡이하</th>
      <th>전체</th>
    </tr>
    <tr>
      <th>연도</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015</th>
      <td>2980.977778</td>
      <td>2712.583333</td>
      <td>2694.490196</td>
      <td>2884.395833</td>
      <td>2694.862745</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>3148.099476</td>
      <td>2848.144279</td>
      <td>2816.965686</td>
      <td>3067.380435</td>
      <td>2816.073529</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>3427.649746</td>
      <td>3112.538071</td>
      <td>2981.950980</td>
      <td>3204.075145</td>
      <td>3008.279412</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>3468.355932</td>
      <td>3286.184783</td>
      <td>3227.458128</td>
      <td>3467.184211</td>
      <td>3235.098522</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>4039.854839</td>
      <td>3486.910112</td>
      <td>3538.545918</td>
      <td>3933.538462</td>
      <td>3515.974490</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>4187.566667</td>
      <td>3615.968750</td>
      <td>3594.852941</td>
      <td>4532.090909</td>
      <td>3603.911765</td>
    </tr>
  </tbody>
</table>

</div>



  <br />  <br />

  

## **8. 연도별, 규모별 가격을 알아보기**


```python
df.groupby(["연도", "규모구분"])["분양가격"].mean()
```


    연도    규모구분         
    2015   102㎡초과          2980.977778
           60㎡이하           2712.583333
           60㎡초과 85㎡이하     2694.490196
           85㎡초과 102㎡이하    2884.395833
          전체               2694.862745
    2016   102㎡초과          3148.099476
           60㎡이하           2848.144279
           60㎡초과 85㎡이하     2816.965686
           85㎡초과 102㎡이하    3067.380435
          전체               2816.073529
    2017   102㎡초과          3427.649746
           60㎡이하           3112.538071
           60㎡초과 85㎡이하     2981.950980
           85㎡초과 102㎡이하    3204.075145
          전체               3008.279412
    2018   102㎡초과          3468.355932
           60㎡이하           3286.184783
           60㎡초과 85㎡이하     3227.458128
           85㎡초과 102㎡이하    3467.184211
          전체               3235.098522
    2019   102㎡초과          4039.854839
           60㎡이하           3486.910112
           60㎡초과 85㎡이하     3538.545918
           85㎡초과 102㎡이하    3933.538462
          전체               3515.974490
    2020   102㎡초과          4187.566667
           60㎡이하           3615.968750
           60㎡초과 85㎡이하     3594.852941
           85㎡초과 102㎡이하    4532.090909
          전체               3603.911765
    Name: 분양가격, dtype: float64



  <br /> 

예쁘게 출력이 안되어서 보기가 힘들때는 pd.DataFrame()으로 한 번 더 감싸주면 됩니다.


```python
pd.DataFrame(df.groupby(["연도", "규모구분"])["분양가격"].mean())
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
      <th></th>
      <th>분양가격</th>
    </tr>
    <tr>
      <th>연도</th>
      <th>규모구분</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2015</th>
      <th>102㎡초과</th>
      <td>2980.977778</td>
    </tr>
    <tr>
      <th>60㎡이하</th>
      <td>2712.583333</td>
    </tr>
    <tr>
      <th>60㎡초과 85㎡이하</th>
      <td>2694.490196</td>
    </tr>
    <tr>
      <th>85㎡초과 102㎡이하</th>
      <td>2884.395833</td>
    </tr>
    <tr>
      <th>전체</th>
      <td>2694.862745</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2016</th>
      <th>102㎡초과</th>
      <td>3148.099476</td>
    </tr>
    <tr>
      <th>60㎡이하</th>
      <td>2848.144279</td>
    </tr>
    <tr>
      <th>60㎡초과 85㎡이하</th>
      <td>2816.965686</td>
    </tr>
    <tr>
      <th>85㎡초과 102㎡이하</th>
      <td>3067.380435</td>
    </tr>
    <tr>
      <th>전체</th>
      <td>2816.073529</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2017</th>
      <th>102㎡초과</th>
      <td>3427.649746</td>
    </tr>
    <tr>
      <th>60㎡이하</th>
      <td>3112.538071</td>
    </tr>
    <tr>
      <th>60㎡초과 85㎡이하</th>
      <td>2981.950980</td>
    </tr>
    <tr>
      <th>85㎡초과 102㎡이하</th>
      <td>3204.075145</td>
    </tr>
    <tr>
      <th>전체</th>
      <td>3008.279412</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2018</th>
      <th>102㎡초과</th>
      <td>3468.355932</td>
    </tr>
    <tr>
      <th>60㎡이하</th>
      <td>3286.184783</td>
    </tr>
    <tr>
      <th>60㎡초과 85㎡이하</th>
      <td>3227.458128</td>
    </tr>
    <tr>
      <th>85㎡초과 102㎡이하</th>
      <td>3467.184211</td>
    </tr>
    <tr>
      <th>전체</th>
      <td>3235.098522</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2019</th>
      <th>102㎡초과</th>
      <td>4039.854839</td>
    </tr>
    <tr>
      <th>60㎡이하</th>
      <td>3486.910112</td>
    </tr>
    <tr>
      <th>60㎡초과 85㎡이하</th>
      <td>3538.545918</td>
    </tr>
    <tr>
      <th>85㎡초과 102㎡이하</th>
      <td>3933.538462</td>
    </tr>
    <tr>
      <th>전체</th>
      <td>3515.974490</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2020</th>
      <th>102㎡초과</th>
      <td>4187.566667</td>
    </tr>
    <tr>
      <th>60㎡이하</th>
      <td>3615.968750</td>
    </tr>
    <tr>
      <th>60㎡초과 85㎡이하</th>
      <td>3594.852941</td>
    </tr>
    <tr>
      <th>85㎡초과 102㎡이하</th>
      <td>4532.090909</td>
    </tr>
    <tr>
      <th>전체</th>
      <td>3603.911765</td>
    </tr>
  </tbody>
</table>

</div>

 <br />

 <br />
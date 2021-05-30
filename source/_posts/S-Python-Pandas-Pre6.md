---
title: Python >> Pandas 전처리 - (6) 데이터프레임의 산술연산
tags:
  - Python
  - Pandas
  - 전처리
categories: 
  - [【STUDY - Python】, Python - 2. Pandas]
  - [【STUDY - Python】, Python - 전처리]
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
abbrlink: 46052
date: 2020-06-20 22:28:21
---

# 데이터프레임의 산술연산

 @[toc]

<br />


```python
import pandas as pd
```


```python
import numpy as np
```

  <br />

**예제 DataFrame 생성**


```python
df = pd.DataFrame({"통계": [60, 70, 80, 85, 75], "미술": [50, 55, 80, 100, 95], "체육": [70, 65, 50, 95, 100] })
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
      <th>통계</th>
      <th>미술</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>60</td>
      <td>50</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>70</td>
      <td>55</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>80</td>
      <td>80</td>
      <td>50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>85</td>
      <td>100</td>
      <td>95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>75</td>
      <td>95</td>
      <td>100</td>
    </tr>
  </tbody>
</table>

</div>



<br />

<br />  

## __1. Column 과 Column 간 연산 (+, -, *, /, %)__


```python
type(df["통계"])
```


    pandas.core.series.Series

즉 Series 과 Series 간의 연산

<br />


```python
df["통계"] + df["미술"] + df["체육"]
```


    0    180
    1    190
    2    210
    3    280
    4    270
    dtype: int64

<br />


```python
df["통계"] - df["미술"]
```


    0    10
    1    15
    2     0
    3   -15
    4   -20
    dtype: int64

<br />


```python
df["통계"] * df["미술"]
```


    0    3000
    1    3850
    2    6400
    3    8500
    4    7125
    dtype: int64

<br />


```python
df["통계"] / df["미술"]
```


    0    1.200000
    1    1.272727
    2    1.000000
    3    0.850000
    4    0.789474
    dtype: float64

<br />


```python
df["통계"] % df["미술"]
```


    0    10
    1    15
    2     0
    3    85
    4    75
    dtype: int64



 <br /> <br />

  

## __2. Column 과 숫자 간 연산 (+, -, *, /, %)__


```python
df["통계"]
```


    0    60
    1    70
    2    80
    3    85
    4    75
    Name: 통계, dtype: int64

<br />


```python
df["통계"] + 10
```


    0    70
    1    80
    2    90
    3    95
    4    85
    Name: 통계, dtype: int64

<br />


```python
df["통계"] - 10
```


    0    50
    1    60
    2    70
    3    75
    4    65
    Name: 통계, dtype: int64

<br />


```python
df["통계"] * 10
```


    0    600
    1    700
    2    800
    3    850
    4    750
    Name: 통계, dtype: int64

<br />


```python
df["통계"] / 10
```


    0    6.0
    1    7.0
    2    8.0
    3    8.5
    4    7.5
    Name: 통계, dtype: float64

<br />


```python
df["통계"] % 10
```


    0    0
    1    0
    2    0
    3    5
    4    5
    Name: 통계, dtype: int64

<br />

<br />

  

## **3. 복합 연산**


```python
df = pd.DataFrame({"통계": [60, 70, 80, 85, 75], "미술": [50, 55, 80, 100, 95], "체육": [70, 65, 50, 95, 100] })
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
      <th>통계</th>
      <th>미술</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>60</td>
      <td>50</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>70</td>
      <td>55</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>80</td>
      <td>80</td>
      <td>50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>85</td>
      <td>100</td>
      <td>95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>75</td>
      <td>95</td>
      <td>100</td>
    </tr>
  </tbody>
</table>

</div>

<br />

  


```python
df["통계미술+10"] = df["통계"] + df["미술"] + 10
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
      <th>통계</th>
      <th>미술</th>
      <th>체육</th>
      <th>통계미술+10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>60</td>
      <td>50</td>
      <td>70</td>
      <td>120</td>
    </tr>
    <tr>
      <th>1</th>
      <td>70</td>
      <td>55</td>
      <td>65</td>
      <td>135</td>
    </tr>
    <tr>
      <th>2</th>
      <td>80</td>
      <td>80</td>
      <td>50</td>
      <td>170</td>
    </tr>
    <tr>
      <th>3</th>
      <td>85</td>
      <td>100</td>
      <td>95</td>
      <td>195</td>
    </tr>
    <tr>
      <th>4</th>
      <td>75</td>
      <td>95</td>
      <td>100</td>
      <td>180</td>
    </tr>
  </tbody>
</table>

</div>

<br />

  


```python
df["통계"] + df["미술"] - df["체육"]
```


    0     40
    1     60
    2    110
    3     90
    4     70
    dtype: int64

<br />

  <br />

  

## **4. mean(), sum() 을 axis 기준으로 연산**


```python
df = pd.DataFrame({"통계": [60, 70, 80, 85, 75], "미술": [50, 55, 80, 100, 95], "체육": [70, 65, 50, 95, 100] })
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
      <th>통계</th>
      <th>미술</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>60</td>
      <td>50</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>70</td>
      <td>55</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>80</td>
      <td>80</td>
      <td>50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>85</td>
      <td>100</td>
      <td>95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>75</td>
      <td>95</td>
      <td>100</td>
    </tr>
  </tbody>
</table>

</div>

<br />

  

**(1) 각 column의 <font color = "blue">모든 row 값의 합</font> 구하기**


```python
df.sum(axis = 0)
```


    통계    370
    미술    380
    체육    380
    dtype: int64

<br />  

**(2) 각 column의 <font color='blue'>모든 row 값의 평균</font> 구하기**


```python
df.mean(axis = 0)
```


    통계    74.0
    미술    76.0
    체육    76.0
    dtype: float64

<br />

  

**(3) 각 row의 <font color='blue'>모든 column 값의 합</font> 구하기**


```python
df.sum(axis = 1)
```


    0    180
    1    190
    2    210
    3    280
    4    270
    dtype: int64

<br />

  

**(4) 각 row의 <font color='blue'>모든 column 값의 평균</font> 구하기**


```python
df.mean(axis = 1)
```


    0    60.000000
    1    63.333333
    2    70.000000
    3    93.333333
    4    90.000000
    dtype: float64

<br />

  <br />

  

## **5. NaN 값이 존재할 경우 연산**

> NaN 값이 포함된 모든 연산의 결과가 다 NaN 값이다

  <br />


```python
df = pd.DataFrame({"통계": [60, np.nan, 80, 85, 75], "미술": [50, 55, np.nan, 100, 95], "체육": [70, 65, 50, 95, np.nan] })
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
      <th>통계</th>
      <th>미술</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>60.0</td>
      <td>50.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>55.0</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>80.0</td>
      <td>NaN</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>85.0</td>
      <td>100.0</td>
      <td>95.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>75.0</td>
      <td>95.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

</div>

<br />

  


```python
df["통계"] / 2
```


    0    30.0
    1     NaN
    2    40.0
    3    42.5
    4    37.5
    Name: 통계, dtype: float64

<br />


```python
1000 / df["통계"]
```


    0    16.666667
    1          NaN
    2    12.500000
    3    11.764706
    4    13.333333
    Name: 통계, dtype: float64

<br />


```python
df["통계"] / np.nan
```


    0   NaN
    1   NaN
    2   NaN
    3   NaN
    4   NaN
    Name: 통계, dtype: float64

<br />


```python
np.nan / df["통계"]
```


    0   NaN
    1   NaN
    2   NaN
    3   NaN
    4   NaN
    Name: 통계, dtype: float64

<br />

 <br />  

## **6. DataFrame 과 DataFrame 간 연산**

### 6-1. 문자열이 포함된 Series / DataFrame의 연산은 불가하다


```python
df1 = pd.DataFrame({'통계': [60, 70, 80, 85, 75], '미술': [50, 55, 80, 100, 95], '체육': [70, 65, 50, 95, 100] })
```


```python
df2 = pd.DataFrame({'통계': ['good', 'bad', 'ok' , 'good', 'ok'], '미술': [50, 60 , 80, 100, 95], '체육': [70, 65, 50, 70 , 100] })
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
      <th>통계</th>
      <th>미술</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>60</td>
      <td>50</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>70</td>
      <td>55</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>80</td>
      <td>80</td>
      <td>50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>85</td>
      <td>100</td>
      <td>95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>75</td>
      <td>95</td>
      <td>100</td>
    </tr>
  </tbody>
</table>

</div>

<br />


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
      <th>통계</th>
      <th>미술</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>good</td>
      <td>50</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bad</td>
      <td>60</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ok</td>
      <td>80</td>
      <td>50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>good</td>
      <td>100</td>
      <td>70</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ok</td>
      <td>95</td>
      <td>100</td>
    </tr>
  </tbody>
</table>

</div>

<br />

  


```python
df1 + df2
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


    TypeError: unsupported operand type(s) for +: 'int' and 'str'

<br />



```python
df2 + 10
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



<br />
<br />

### 6-2. 두 DataFrame의 column 이름은 같으나 column 순서만 바뀌어 있는 경우 

> 연산시 자동으로 column 이름 기준으로 연산 된다 

<br />

```python
df1 = pd.DataFrame({'미술': [10, 20, 30, 40, 50], '통계':[60, 70, 80, 90, 100] })
df2 = pd.DataFrame({'통계': [10, 20, 30, 40, 50], '미술': [60, 70, 80, 90, 100] })
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
      <th>미술</th>
      <th>통계</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>50</td>
      <td>100</td>
    </tr>
  </tbody>
</table>

</div>

<br />


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
      <th>통계</th>
      <th>미술</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>50</td>
      <td>100</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
df1 + df2
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
      <th>미술</th>
      <th>통계</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>70</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>90</td>
      <td>90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>110</td>
      <td>110</td>
    </tr>
    <tr>
      <th>3</th>
      <td>130</td>
      <td>130</td>
    </tr>
    <tr>
      <th>4</th>
      <td>150</td>
      <td>150</td>
    </tr>
  </tbody>
</table>

</div>


<br />
<br /> 

### 6-3. 행의 갯수가 다른 경우  
> 행 index 기준으로 연산하되, 하나의 DataFrame에만 존재하는 행은 연산결과가 NaN으로 나옴

<br />

```python
df1 = pd.DataFrame({'미술': [10, 20, 30, 40, 50, 60], '통계':[60, 70, 80, 90, 100, 110] })
df2 = pd.DataFrame({'통계': [10, 20, 30, 40, 50], '미술': [60, 70, 80, 90, 100] })
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
      <th>미술</th>
      <th>통계</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>50</td>
      <td>100</td>
    </tr>
    <tr>
      <th>5</th>
      <td>60</td>
      <td>110</td>
    </tr>
  </tbody>
</table>

</div>

<br />


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
      <th>통계</th>
      <th>미술</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>50</td>
      <td>100</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
df1 * df2
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
      <th>미술</th>
      <th>통계</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>600.0</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1400.0</td>
      <td>1400.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2400.0</td>
      <td>2400.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3600.0</td>
      <td>3600.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5000.0</td>
      <td>5000.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

</div>

<br />

<br />
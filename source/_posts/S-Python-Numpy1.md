---
uuid: fab5fbb3-e4bc-4431-773f-88f2155b4106
title: Python >> Numpy - (1) Numpy. array
tags:
  - Python
  - Numpy
categories: [【STUDY - Python】, Python - 1. Numpy]
description: Numpy개요. Numpy import하기. ndarray 생성. array에서의 데이터 타입
cover: https://s1.ax1x.com/2020/05/23/Yjnp1s.png
typora-root-url: ..
abbrlink: 27530
date: 2020-05-19 00:07:32
---

Numpy개요. Numpy import하기. nd array 생성. array에서의 데이터 타입

<!-- more -->

# **목록**

@[toc]

<br />

## **1. Numpy 개요**

### 1-1. Numpy이란?

Numpy: 수학, 과학 계산용 패키지

​    <br />

### 1-2. 별칭 - np


```python
import numpy as np
```

  <br />

### 1-3. array (배열)

**배열**: 여러 값들의 그룹

<br />  

**< 1차원 배열 >**

<br />

<center><img src="/images/S-Python-Numpy1/1_array.png" alt="1_array" style="zoom:80%;"/></center>

<div style="text-align: center"> numpy.array([1, 2, 3, 4]) </div>

 <br /> 

**< 2차원 배열 >**

 <br />

<center><img src="/images/S-Python-Numpy1/2_array.png" alt="2_array" style="zoom:80%;" /></center>

<div style="text-align: center"> 
numpy.array([[1, 2, 3, 4],  
             [5, 6, 7, 8],  
             [9, 10, 11, 12],  
             [13, 14, 15, 16]]) 
</div>
<br />

**< n차원 배열 >   (nd array: *n dimention* array)**

<center><img src="/images/S-Python-Numpy1/n_array.png" alt="n_array" style="zoom:80%;" align=center/></center>

  <br />

  <br />

### 1-4. shape(차원) & axis(축)

* **shape은 <font color='red'> 차원의 수 </font> 를 확인**  
  
   (3, ) => 3 X 1의 배열  
   (4,3) => 4 X 3의 배열  
   (2,5,3) => 2 X 5 X 3의 배열  

* **axis는 기준이 되는 <font color='red'> 축 </font>** 
      
    axis는 앞에서 부터 0, 1, 2...  
    nd array의 축: axis 0, axis 1, axis 2, ... axis n

  <br />

  <br />

## **2. Numpy import하기**


```python
import numpy
```


```python
numpy
```


    <module 'numpy' from 'D:\\Anaconda\\lib\\site-packages\\numpy\\__init__.py'>

<br />

### 2-1. 별칭 (alias) 지정하기 (항상 해주세요!)


```python
import numpy as np
```


```python
np
```


    <module 'numpy' from 'D:\\Anaconda\\lib\\site-packages\\numpy\\__init__.py'>

<br />

  <br />

## **3. ndarray 생성하기 -- "np.array([...])"**


```python
arr = np.array([1,2,3,4], dtype=int)
```


```python
arr # 주의: list와 다름
```


    array([1, 2, 3, 4])

<br />


```python
[1, 2, 3, 4]  # list
```


    [1, 2, 3, 4]

<br />


```python
type(arr)
```


    numpy.ndarray

<br />

<br />  

### 3-1. list로 부터 생성하기 -- "np.array(*list_name*)"


```python
mylist1 = [1, 2, 3, 4]
```


```python
mylist2 = [[1, 2, 3, 4],
           [5, 6, 7, 8]]
```

<br />

```python
arr1 = np.array(mylist1)
```


```python
arr1
```


    array([1, 2, 3, 4])

<br />


```python
arr2 = np.array(mylist2)
```


```python
arr2
```


    array([[1, 2, 3, 4],
           [5, 6, 7, 8]])

<br />

 <br /> 

### 3-2. shape확인하기 -- "*array_name* .shape"


```python
arr1.shape
```


    (4,)

<br />


```python
arr2.shape
```


    (2, 4)

<br />

 <br />   

## **4. array에서의 data type**

**array에서는 list와 다르게 1개의 <font color='red'>단일 데이터 타입 </font> 만 허용 된다**

  <br />

### 4-1. list에서의 data type


```python
mylist = [1, 3.14, '사과', '1234']
```


```python
mylist
```


    [1, 3.14, '사과', '1234']

<br />


```python
mylist[0]
```


    1

<br />


```python
mylist[2]
```


    '사과'

<br />

 <br /> 

### 4-2. array에서의 data type

#### case 1. int와 float타입이 혼재된 경우

int와 float타입이 혼재된 경우 int(정수)가 float(실수)로 바꿔진다


```python
arr = np.array([1, 2, 3, 3.14])
```


```python
arr  # 정수가 실수로 바꿔진다
```


    array([1.  , 2.  , 3.  , 3.14])

<br />

​    

#### case 2. int와 float 타입이 혼재되었으나, dtype을 지정한 경우

int와 float 타입이 혼재되었으나, dtype가 int로 지정된 경우, float의 앞에 정수 부분만 보류된다


```python
arr = np.array([1, 2, 3, 3.14], dtype = int)
```


```python
arr
```


    array([1, 2, 3, 3])

<br />

  

#### case 3. int / float 와 str 타입이 혼재된 경우

int / float 와 float타입이 혼재된 경우 int(정수)가 str(문자열)로 바꿔진다


```python
arr = np.array([1, 3.14, '사과', '1234'])
```


```python
arr
```


    array(['1', '3.14', '사과', '1234'], dtype='<U32')

<br />


```python
arr[0] + arr[1]  #str로 되어버려서 숫자의 사칙 연산이 안됨
```


    '13.14'

<br />

  

#### case 4. int와 str 타입이 혼재되어 있고 dtype이 int로 지정한 경우

**(1) 문자내용인 str이 존재한 경우 error 발생**


```python
arr = np.array([1, 3.14, '사과', '1234', '5.8'], dtype = int)
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-50-88e75a912236> in <module>
    ----> 1 arr = np.array([1, 3.14, '사과', '1234', '5.8'], dtype = int)


    ValueError: invalid literal for int() with base 10: '사과'

<br />

**(2) 실수(float)내용인 str이 존재한 경우도 error발생**


```python
arr = np.array([1, 3.14, '1234', '5.8'], dtype = int)
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-52-98017763e514> in <module>
    ----> 1 arr = np.array([1, 3.14, '1234', '5.8'], dtype = int)


    ValueError: invalid literal for int() with base 10: '5.8'

<br />

**(3) 정수(int)내용인 str만 존재한 경우 해당 str이 자동으로 int로 바꿔짐**


```python
arr = np.array([1, 3.14, '1234'], dtype = int)
```


```python
arr
```


    array([   1,    3, 1234])

<br /><br />
---
uuid: 935c8830-fd87-d890-a6d8-23a61e6c7977
title: Python >> Numpy - (2) Slicing. 인덱싱
tags:
  - Python
  - Numpy
categories: [【STUDY - Python】, Python - 1. Numpy]
description: 배열의 부분선택 - 슬라이싱 (Slicing),  Fancy 인덱싱,  Boolean 인덱싱.
cover: https://s1.ax1x.com/2020/05/23/Yjnp1s.png
abbrlink: 50480
date: 2020-05-19 21:55:06
---

슬라이싱 (Slicing).  Fancy 인덱싱.  Boolean 인덱싱.

<!-- more -->

# **목록**

@[toc]

<br />

## **1. 슬라이싱 (Slicing)**


```python
import numpy as np
```

<br />

베열의 부분 선택 (과일을 슬라이스해서 부분만 먹듯..)


```python
arr = np.array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
```


```python
arr.shape
```


    (10,)

<br />

  

### 1-1. index 지정하여 색인

#### 1차원 array


```python
arr = np.array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
```


```python
arr[0]  # index: 앞에서 부터 0, 1, 2, ...
```


    0


```python
arr[5]
```


    5


```python
arr[10]  # index가 넘으면 error남
```


    ---------------------------------------------------------------------------
    
    IndexError                                Traceback (most recent call last)
    
    <ipython-input-7-ff656e92d79c> in <module>
    ----> 1 arr[10]


    IndexError: index 10 is out of bounds for axis 0 with size 10

<br />

```python
arr[-1]   # 뒤에서 부터 1번째.  index: 뒤에서 부터 -1, -2, -3,...
```


    9


```python
arr[-10]
```


    0


```python
arr[-11]
```


    ---------------------------------------------------------------------------
    
    IndexError                                Traceback (most recent call last)
    
    <ipython-input-10-91f133f07612> in <module>
    ----> 1 arr[-11]


    IndexError: index -11 is out of bounds for axis 0 with size 10

<br />

#### 2차원 array


```python
arr2d = np.array([[1, 2, 3, 4],
                  [5, 6, 7, 8],
                  [9, 10, 11, 12]])
```


```python
arr2d.shape
```


    (3, 4)

<br />

**arr2d[행, 열]**


```python
arr2d[0, 2]
```


    3


```python
arr2d[2, 1]
```


    10

<br />

 <br /> 

### 1-2. 범위 색인

#### 1차원 array

* **arr[a, b]** --  arr의 "index **<font color='red'>a</font>**" 부터 "index **<font color='red'>b-1</font>**"까지  <font color='red'>(a 포함, b 미포함)</font>

**index:** 1 이상


```python
arr
```


    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])


```python
arr[1:]   # index 1 포함
```


    array([1, 2, 3, 4, 5, 6, 7, 8, 9])

<br />

**index:** 5 미만


```python
arr[:5]  # index 5 미포함
```


    array([0, 1, 2, 3, 4])

<br />

**index:** 1이상 5미만


```python
arr[1:5]  # index 1 포함 & index 5 미포함
```


    array([1, 2, 3, 4])

<br />

**index:** -1까지


```python
arr[:-1]  # index -1 (index 9) 미포함
```


    array([0, 1, 2, 3, 4, 5, 6, 7, 8])

<br />

  <br />

#### 2차원 array


```python
arr2d = np.array([[1, 2, 3, 4],
                  [5, 6, 7, 8],
                  [9, 10, 11, 12]])
```

  <br />

**row(행)을 모두 가져오려는 경우**


```python
arr2d[0,:]  # 0번 행의 모든 열 가져오기
```


    array([1, 2, 3, 4])

 <br />



**colomn(열)을 모두 가져오려는 경우**


```python
arr2d[:,2]
```


    array([ 3,  7, 11])

 <br /> 

**부분적으로 가져오려는 경우**


```python
arr2d[:2, :]  # 0,1번 행의 모든 열 가져오기
```


    array([[1, 2, 3, 4],
           [5, 6, 7, 8]])

<br />


```python
arr2d[:2, 2:]  # 0,1번 행의 2,3번 열 가져오기
```


    array([[3, 4],
           [7, 8]])

<br />

 <br />   

## **2. Fancy 인덱싱**

fancy인덱싱은 범위가 아닌 **특정 index의 집합의 값을 선택하여 추출**하고 싶을 때 활용한다


```python
arr = np.array([10, 23, 2, 7, 90, 65, 32, 66, 70])
```

 <br /> 

### 2-1. 1차원 array

**방법 1:** 추출하고 싶은 index의 집합을 **[꺾쇠 괄호로]**묶어서 추출


```python
arr[[1, 3, 5]]
```


    array([23,  7, 65])

<br />

**방법 2:**  추출하고 싶은 index의 집합을 **변수에 지정한 후** 추출


```python
idx = [1, 3, 5]
```


```python
arr[index]
```


    array([23,  7, 65])

  <br />

<br />

### 2-2. 2차원 array


```python
arr2d = np.array([[1, 2, 3, 4], 
                  [5, 6, 7, 8], 
                  [9, 10, 11, 12]])
```


```python
arr2d[[0,1], :]
```


    array([[1, 2, 3, 4],
           [5, 6, 7, 8]])

<br />


```python
arr2d[:, [1,3]]
```


    array([[ 2,  4],
           [ 6,  8],
           [10, 12]])

<br />

 <br /> 

## **3. Boolean 인덱싱**

조건 필터링을 통하여 Boolean값을 이용한 색인


```python
arr = np.array([1, 2, 3, 4, 5, 6, 7])
```


```python
arr2d = np.array([[1, 2, 3, 4],
                 [5, 6, 7, 8],
                 [9, 10, 11, 12]])
```

<br />  

### 3-1. True와 False값으로 색인하기

boolean index의 수가 꼭 array의 index와 같아야 됨!


```python
myTrueFalse = [True, False, True]
```


```python
arr[myTrueFalse]
```


    ---------------------------------------------------------------------------
    
    IndexError                                Traceback (most recent call last)
    
    <ipython-input-43-9c52b39d81ae> in <module>
    ----> 1 arr[myTrueFalse]


    IndexError: boolean index did not match indexed array along dimension 0; dimension is 7 but corresponding boolean dimension is 3

<br />

```python
myTrueFalse = [True, False, True, False, True, False, True]
```


```python
arr[myTrueFalse]
```


    array([1, 3, 5, 7])

<br />

  <br />

### 3-2. 조건필터

조건 연산자를 활용하여 필터를 생성할 수 있다


```python
arr2d
```


    array([[ 1,  2,  3,  4],
           [ 5,  6,  7,  8],
           [ 9, 10, 11, 12]])

<br />


```python
arr2d > 2  # "2보다 크다"라는 조건의 만족여부에 따라 Boolean index 생성
```


    array([[False, False,  True,  True],
           [ True,  True,  True,  True],
           [ True,  True,  True,  True]])

<br />

위 Boolean index를 다시 array에 적용하여 해당 부분을 추출: **arr2d[조건필터]**


```python
arr2d[arr2d > 2]  # 1차원 array로 반환
```


    array([ 3,  4,  5,  6,  7,  8,  9, 10, 11, 12])

<br />


```python
arr2d[arr2d < 5]
```


    array([1, 2, 3, 4])

<br /><br />
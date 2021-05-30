---
uuid: b297e092-498d-d62f-b33c-e8b66f493738
title: Python >> Numpy - (4) 행렬. Broadcasting
tags:
  - Python
  - Numpy
categories: [【STUDY - Python】, Python - 1. Numpy]
description: 행렬 (덧셈, 뺄셈, 곱셈).  Broadcasting.
cover: https://s1.ax1x.com/2020/05/23/Yjnp1s.png
abbrlink: 51120
date: 2020-05-20 16:55:34
---

행렬 (덧셈, 뺄셈, 곱셈).  Broadcasting.

<!-- more -->



# **목록**

@[toc]

<br />

```python
import numpy as np
```

## **1. 행렬 - 덧셈**

**행렬의 shape이 같아야 덧셈 가능**

### 1-1. 덧셈


```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
b = np.array([[3, 4, 5],
              [1, 2, 3]])
```


```python
a + b
```


    array([[4, 6, 8],
           [3, 5, 7]])

 <br />




```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
b = np.array([[1, 2],
              [3, 4],
              [5, 6]])
```


```python
a + b    # shape이 다르면 error발생
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-7-37f7d36ad418> in <module>
    ----> 1 a + b    # shape이 다르면 error발생


    ValueError: operands could not be broadcast together with shapes (2,3) (3,2) 

<br />


### 1-2. Sum -- Matrix안의 계산

**명령어:** np.sum('array_name', axis = '0/1/...')      

**주의:** 계산할 때 **axis의 방향대로 Sum을 구한다.**  

예를 들면, 2darray에서,  
* axis = 0 이면: 수직방향으로 Sum을 구한다

* axis = 1 이면: 수평방향으로 Sum을 구한다

  <br />


```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
np.sum(a, axis = 0)
```


    array([3, 5, 7])

<br />


```python
np.sum(a, axis = 1)
```


    array([6, 9])

<br />

  <br />

## **2. 행렬 - 뺄셈**


```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
b = np.array([[3, 4, 5],
              [1, 2, 3]])
```


```python
a - b
```


    array([[-2, -2, -2],
           [ 1,  1,  1]])

 <br />




```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
b = np.array([[1, 2],
              [3, 4],
              [5, 6]])
```


```python
a - b    # shape이 다르면 error발생
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-18-e62ba154daaa> in <module>
    ----> 1 a - b    # shape이 다르면 error발생


    ValueError: operands could not be broadcast together with shapes (2,3) (3,2) 

<br />

<br />


## **3. 행렬 - 곱셈**

### 3-1. 일반 곱셈

일반곱셈은 덧셈과 뺏셈이랑 동일하게 같은 위치에 있는 애들끼리 곱한다.  
**[shape이 완전 같아야 함]**


```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
b = np.array([[3, 4, 5],
              [1, 2, 3]])
```


```python
a * b
```


    array([[ 3,  8, 15],
           [ 2,  6, 12]])

 <br />  

### 3-2. dot product / 내적곱

**[맞닿는 shape이 같아야 함]**


```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
b = np.array([[1, 2],
              [3, 4],
              [5, 6]])
```


```python
a.shape, b.shape 
```


    ((2, 3), (3, 2))

<br />

**방법 1: np.dot(a, b)**


```python
np.dot(a, b)
```


    array([[22, 28],
           [31, 40]])

<br />

**방법2: a.dot(b)**


```python
a.dot(b)
```


    array([[22, 28],
           [31, 40]])

<br />

<br />  

## **4. Broadcasting**

### 4-1. 숫자의 연산

array a 의 모든 원소에 3을 더하고 싶다면:

* 단순히 행렬 덧셈을 사용할 때:


```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
b = np.array([[3, 3, 3],
              [3, 3, 3]])
```


```python
a + b
```


    array([[4, 5, 6],
           [5, 6, 7]])

<br />

* Broadcasting 사용할 때:


```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
a + 3
```


    array([[4, 5, 6],
           [5, 6, 7]])

<br />


```python
a - 3
```


    array([[-2, -1,  0],
           [-1,  0,  1]])

<br />


```python
a * 3
```


    array([[ 3,  6,  9],
           [ 6,  9, 12]])

<br />


```python
a / 3
```


    array([[0.33333333, 0.66666667, 1.        ],
           [0.66666667, 1.        , 1.33333333]])

<br />

 <br /> 

### 4-2. array (배열)의 broadcasting

original array의 shape이 유지됨.


```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
b = np.array([[1],
              [2]])
```


```python
a.shape, b.shape
```


    ((2, 3), (2, 1))


```python
a * b
```


    array([[1, 2, 3],
           [4, 6, 8]])

 












<br />


```python
a = np.array([[1, 2, 3],
              [2, 3, 4]])
```


```python
b = np.array([1, 2, 3])
```


```python
a * b
```


    array([[ 1,  4,  9],
           [ 2,  6, 12]])
<br /><br />
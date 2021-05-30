---
uuid: 3a188c58-dd47-3d0d-3c77-cb8ae8951651
title: Python >> Numpy - (3) 수열. 정렬
tags:
  - Python
  - Numpy
categories: [【STUDY - Python】, Python - 1. Numpy]
description: 수열 생성- arange & range. 정렬- sort & argsort
cover: https://s1.ax1x.com/2020/05/23/Yjnp1s.png
abbrlink: 2955
date: 2020-05-20 02:10:54
---

arange. range. 정렬(sort & argsort)

<!-- more -->

# **목록**

@[toc]

<br />

```python
import numpy as np
```

## **1. arange란?**

arange와 range를 같이 보고 이해하면 됨

**[실제 상황 예시]**

우리는 순차적인 값을 생성할 때가 많다. 예를 들면:  
  1. 회원에 대한 가입번호 부여
  2. 100개 한정 판매 상품에 대한 고유 번호 부여  

이 밖에도 데이터 관리를 위한 인덱스를 차례대로 부여하는 것은 매우 흔한 일이다.

  <br />

### 1-1. 순서대로 리스트에 값을 생성하려면?

1~10까지 값을 생성하려면?


```python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```


```python
arr
```


    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

 <br /> 




### 1-2. arange를 사용해서 쉽게 생성하기

**np.arange(a, b):** **<font color='red'>a</font>** 부터 **<font color='red'>b-1</font>** 까지 생성한다  **<font color='red'>(a포함, b미포함)</font>**


```python
arr = np.arange(1, 11)
```


```python
arr
```


    array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])

 <br />




### 1-3. keyword인자를 사용해보기

**np.arange(start = a,  stop = b)**


```python
arr = np.arange(start=1, stop=11)
```


```python
arr
```


    array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])

<br />


```python
arr = np.arange(stop=11, start=1)  # start & stop 지정했기 때문에 순서 바꿔도 됨
```


```python
arr
```


    array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])

<br />


```python
arr = np.arange(11,1)  # start & stop 지정 안하면 순서 바꿨을 때 오류 남
```


```python
arr
```


    array([], dtype=int32)



<br />

### 1-4. 홀수의 값만 생성

1~10 사이의 값중 홀수만 생성

**step 키워드 활용**

np.arange(start, stop, step)


```python
arr = np.arange(1, 11, 2)  
```


```python
arr
```


    array([1, 3, 5, 7, 9])

<br />


```python
arr = np.arange(start=1, stop=11, step=2)
```


```python
arr
```


    array([1, 3, 5, 7, 9])

 <br />

<br />




## **2. range (Numpy와는 상관없는 Python문법)**

* range는 말 그대로 범위를 지정해 주는 것이다
* 보통 for-in 의 반복문에서 많이 사용된다
* arange와는 다르게 array형태로 저장되어있지 않고 그냥 가볍게 바로바로 쓴다

  <br />

**arange 구문 활용시**


```python
arr = np.arange(1, 11)
```


```python
arr
```


    array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])

<br />


```python
for i in arr:
    print(i)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10

<br />


**range 구문 활용시**


```python
for i in range(1, 11):
    print(i)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10

<br />

```python
for i in range(1, 11, 2):
    print(i)
```

    1
    3
    5
    7
    9

<br />

<br />

## **3. 정렬**

### 3-1. 1차원 정렬

1차원 정렬은 매우 간단함
  * 오름차순으로 정렬: np.sort(arr)
  * 내림차순으로 정렬: np.sort(arr)[::-1]


```python
arr = np.array([1, 10, 5, 8, 2, 4, 3, 6, 8, 7, 9])
```


```python
arr
```


    array([ 1, 10,  5,  8,  2,  4,  3,  6,  8,  7,  9])

<br />


```python
np.sort(arr)
```


    array([ 1,  2,  3,  4,  5,  6,  7,  8,  8,  9, 10])

<br />


```python
np.sort(arr)[::-1]
```


    array([10,  9,  8,  8,  7,  6,  5,  4,  3,  2,  1])

<br />

하지만, 그냥 이상태에서는 정렬된 이 값들이 **유지가 안됨**  
값을 sort 된 상태로 유지시키려면:  
  * 변수로 다시 지정해주기
  * np.sort(arr) 대신 arr.sort() 쓴다 [arr자체에 sort명령을 씌워줌] 


```python
arr
```


    array([ 1, 10,  5,  8,  2,  4,  3,  6,  8,  7,  9])

<br />


```python
np.sort(arr)
```


    array([ 1,  2,  3,  4,  5,  6,  7,  8,  8,  9, 10])

<br />


```python
arr    # np.sort 만 실행했을 때 유지가 안됨
```


    array([ 1, 10,  5,  8,  2,  4,  3,  6,  8,  7,  9])

<br />


```python
arr2 = np.sort(arr)   # 방법1: arr2로 지정하기
```


```python
arr2
```


    array([ 1,  2,  3,  4,  5,  6,  7,  8,  8,  9, 10])

<br />


```python
arr.sort()    # 방법2: arr.sort 사용하기
```


```python
arr
```


    array([ 1,  2,  3,  4,  5,  6,  7,  8,  8,  9, 10])

<br />

 <br /> 

### 3-2. N차원 정렬

N차원 정렬에서는 axis 중요함. (즉, 정렬 기준이 되는 축)


```python
arr2d = np.array([[5, 6, 7, 8], 
                  [4, 3, 2, 1],
                  [10, 9, 12, 11]])
```


```python
arr2d.shape
```


    (3, 4)

<br />




**열 정렬 (왼쪽에서 오른쪽으로 정렬) -- axis 1을 기준으로 삼**


```python
arr2d   # 정렬 전
```


    array([[ 5,  6,  7,  8],
           [ 4,  3,  2,  1],
           [10,  9, 12, 11]])

<br />


```python
np.sort(arr2d, axis = 1)   # 정렬 후
```


    array([[ 5,  6,  7,  8],
           [ 1,  2,  3,  4],
           [ 9, 10, 11, 12]])

  <br />




**행 정렬 (위에서 아래로 정렬) -- axis 0을 기준으로 삼**


```python
arr2d   # 정렬 전
```


    array([[ 5,  6,  7,  8],
           [ 4,  3,  2,  1],
           [10,  9, 12, 11]])

<br />


```python
np.sort(arr2d, axis = 0)   # 정렬 후
```


    array([[ 4,  3,  2,  1],
           [ 5,  6,  7,  8],
           [10,  9, 12, 11]])

<br />

<br />  

### 3-3. index를 반환하는 argsort

정렬한 결과에는 값을 반환하는 것이 아닌 index를 반환한다

 <br />

**열 정렬 (왼쪽에서 오른쪽으로 정렬)**


```python
arr2d   # 정렬 전
```


    array([[ 5,  6,  7,  8],
           [ 4,  3,  2,  1],
           [10,  9, 12, 11]])

<br />


```python
np.sort(arr2d, axis = 1)  # sort 정렬 후
```


    array([[ 5,  6,  7,  8],
           [ 1,  2,  3,  4],
           [ 9, 10, 11, 12]])

<br />


```python
np.argsort(arr2d, axis = 1)   # argsort 정렬 후
```


    array([[0, 1, 2, 3],
           [3, 2, 1, 0],
           [1, 0, 3, 2]], dtype=int64)

 <br />

<br />


**행 정렬 (위에서 아래로 정렬)**


```python
arr2d   # 정렬 전
```


    array([[ 5,  6,  7,  8],
           [ 4,  3,  2,  1],
           [10,  9, 12, 11]])

<br />


```python
np.sort(arr2d, axis = 0)   # sort 정렬 후
```


    array([[ 4,  3,  2,  1],
           [ 5,  6,  7,  8],
           [10,  9, 12, 11]])

<br />


```python
np.argsort(arr2d, axis = 0)   # argsort 정렬 후
```


    array([[1, 1, 1, 1],
           [0, 0, 0, 0],
           [2, 2, 2, 2]], dtype=int64)
<br />

<br />
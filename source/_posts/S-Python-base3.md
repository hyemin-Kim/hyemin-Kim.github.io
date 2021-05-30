---
uuid: 9ca5c22d-b8b4-08ff-d094-e86583773cc6
title: Python 기초문법 - (3) 함수
tags: 
 - Python
 - Python_Base
categories: [【STUDY - Python】, Python - 0. Base]
description: 함수의 기초
cover: https://ih1.redbubble.net/image.452049706.1381/flat,750x,075,f-pad,750x1000,f8f8f8.u5.jpg
abbrlink: 16569
date: 2020-05-13 16:16:31
---

**함수의 기초**

<!-- more -->

# **목록**

@[toc]

<br />

# **함수**

## **1. 함수란 무엇일까?**

반복적으로 사용되는 부문을 묶어서, **재사용 가능**하도록 만들어 주는 것

함수에는 **들어가는 놈 (input)**이 있고, **나오는 놈 (output 혹은 return)**이 있다. 전해진 로직(규칙)에 따라, input -> output으로 효율적으로 바꿔주는 역할을 한다

<br />

**[예시]**

**함수 없이 계산할 때**


```python
a = 1
b = 2
c = 3
```


```python
(a + b) * c
```


    9

<br />


```python
a = 2
b = 2
c = 3
```


```python
(a + b) * c
```


    12

<br />

**함수로 변경 후**


```python
def func(a, b, c):
    return (a + b) * c
```


```python
func(1, 2, 3)
```


    9

<br />


```python
func(2, 2, 3)
```


    12



  <br />

  <br />

## **2. 함수 정의: def (define)**

* 사용법: def **함수이름** (parameter1, parameter2, parameter3...): 

* parameter는 함수로 부터 **넘겨 받은 변수 또는 값**이다

* 끝에 콜론 ( : ) 빼먹지 않음에 주의 해야함!

  <br />


```python
def myfunc(var1):
    print(var1)      # 실행 명령
```


```python
myfunc("안녕하세요")
```

    안녕하세요

<br />

<br />


## **3. 함수는 값을 return할 수 있고, 안해도 됨**

**리턴이 없는 경우**


```python
def my_func(a, b):
    print(a, b)
```


```python
my_func(1,10)
```

    1 10

<br />

**리턴이 있는 경우**


```python
def my_func(a, b):
    s = a + b
    return s
```


```python
my_func(2, 3)
```


    5

<br />

**리턴이 있는 경우는 변수에 값을 다시 할당 할 수 있음**


```python
result = my_func(2,3)
```


```python
print(result)
```

    5

```python
print(result + 10)
```

    15

<br /><br />


## **4. parameter가 여러 개 있으면, 함수에 넘겨 줄 때 순서가 중요**


```python
def my_func(a, b, c):
    return (a + b) * c
```


```python
a = 10
b = 20
c = 3
```

<br />

```python
(a + b) * c
```


    90

<br />


```python
my_func(a, b, c)
```


    90

<br />


```python
my_func(c, b, a)   # (c + b) * a = (3 + 20) * 10
```


    230

<br /><br />


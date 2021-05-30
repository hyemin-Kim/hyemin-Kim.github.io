---
uuid: d2c4bf91-dc2d-d1fd-3cc0-80201f53ac45
title: Python 기초문법 - (2) 집합 형태의 데이터 타입
tags: 
 - Python
 - Python_Base
categories: [【STUDY - Python】, Python - 0. Base]
description: 집합 형태의 데이터 타입-- list, tuple, set, dict
cover: https://ih1.redbubble.net/image.452049706.1381/flat,750x,075,f-pad,750x1000,f8f8f8.u5.jpg
abbrlink: 26245
date: 2020-05-13 02:26:49
---

# **집합 형태의 데이터 타입**

@[toc]

<br />

**짐합 형태의 데이터 타입**

1. list (순서 O, 집합)

2. tuple (순서 O, 읽기 전용 집합)

3. set (순서 X, 중복 X 집합)

4. dict (key, value로 이루어진 사전형 집합)

   <br />

## **1. list (순서가 있는 집합)**

### 1-1. [ ] 형테로 표현


```python
mylist = []
```


```python
mylist
```


    []

<br />

```python
type(mylist)
```


    list

<br />


```python
mylist = [1,2,3,4,5]
mylist
```


    [1, 2, 3, 4, 5]

<br />


```python
mylist2 = [5,4,3,2,1]   # 순서가 있다
mylist2        
```


    [5, 4, 3, 2, 1]

<br />



### 1-2. 값 추가 -- ".append( )"


```python
mylist = []
mylist
```


    []

<br />


```python
mylist.append(1)
mylist
```


    [1]

<br />


```python
mylist.append(2)
mylist.append(3)
mylist
```


    [1, 2, 3]

<br />

  

**.append 함수 안에 1 argument만 들어갈 수 있다**


```python
mylist.append(4,5)
mylist
```


    ---------------------------------------------------------------------------
    
    TypeError                                 Traceback (most recent call last)
    
    <ipython-input-22-6f00703728b8> in <module>
    ----> 1 mylist.append(4,5)
          2 mylist


    TypeError: append() takes exactly one argument (2 given)

<br />



### 1-3. 값 제거 -- ".remove" / ".clear"

**부분 제거 -- ".remove"**


```python
mylist
```


    [1, 2, 3]

<br />


```python
mylist.remove(1)
mylist
```


    [2, 3]

 <br />

**전부 제거 -- ".clear"**


```python
mylist.clear()
```


```python
mylist
```


    []

<br /> 

**같은 값이 여러 개 포함되어 있을 때의 제거 순서**

앞에서 부터 순차적으로 제거 됨


```python
mylist = [1,2,3,1,2,3]
mylist
```


    [1, 2, 3, 1, 2, 3]

<br />


```python
mylist.remove(1)
mylist
```


    [2, 3, 1, 2, 3]

<br />


```python
mylist.remove(1)
mylist
```


    [2, 3, 2, 3]

  <br />



### 1-4. 인덱싱(Indexing) -> 색인

인덱스는 **0번 부터 시작**한다


```python
mylist = [1,2,3,4]  # 인덱스: 0번, 1번, 2번, 3번
```


```python
mylist[0]
```


    1

<br />


```python
mylist[3]
```


    4

<br />


```python
mylist[4]
```


    ---------------------------------------------------------------------------
    
    IndexError                                Traceback (most recent call last)
    
    <ipython-input-34-88b11041aa4f> in <module>
    ----> 1 mylist[4]


    IndexError: list index out of range

<br />

인덱스가 음수일 경우: 뒤에서 부터 n번째  


```python
mylist[-1]
```


    4

<br />

 

### 1-5. 인덱스로 접근하여 값 바꾸기


```python
mylist
```


    [1, 2, 3, 4]

<br />


```python
mylist[0]
```


    1

<br />


```python
mylist[0] = 100
```


```python
mylist
```


    [100, 2, 3, 4]

<br />



### 1-6. 길이 파악하기


```python
mylist
```


    [100, 2, 3, 4]

<br />


```python
len(mylist)  # length
```


    4

<br />

  <br />

## **2. tuple (순서가 있는 집합, 읽기 전용)**

### 2-1. ( ) 형태로 표현


```python
mytuple = (1,2,3,4,5)
```

<br />  

### 2-2. 읽기 전용이라 "값 추가", "값 제거", "값 바꾸기" 모두 안됨


```python
mytuple.append(1)    # 읽기 전용이라 값을 추가할 수 없음
```


    ---------------------------------------------------------------------------
    
    AttributeError                            Traceback (most recent call last)
    
    <ipython-input-45-d0f55ea1e3f6> in <module>
    ----> 1 mytuple.append(1)    # 읽기 전용이라 값을 추가할 수 없음


    AttributeError: 'tuple' object has no attribute 'append'

<br />

```python
mytuple.remove(1)
```


    ---------------------------------------------------------------------------
    
    AttributeError                            Traceback (most recent call last)
    
    <ipython-input-46-05a40423345b> in <module>
    ----> 1 mytuple.remove(1)


    AttributeError: 'tuple' object has no attribute 'remove'

<br />

```python
mytuple[0] = 100
```


    ---------------------------------------------------------------------------
    
    TypeError                                 Traceback (most recent call last)
    
    <ipython-input-48-4e527888818c> in <module>
    ----> 1 mytuple[0] = 100


    TypeError: 'tuple' object does not support item assignment

<br />


### 2-3. 길이 파악하기


```python
mytuple
```


    (1, 2, 3, 4, 5)

<br />


```python
len(mytuple)
```


    5

<br />

  <br />

## **3. set (순서 X, 중복 X)**

### 3-1. set의 할당: set()


```python
myset = set()
myset
```


    set()

<br />


```python
type(myset)
```


    set

<br />

### 3-2. 값 추가 --  ".add "


```python
myset.add(1)
myset.add(2)
myset.add(3)
myset
```


    {1, 2, 3}

<br />


```python
myset.add(1)  
myset.add(2)
myset.add(3)
myset.add(1)  # 중복된 값을 한번만 기록
myset.add(2)
myset.add(3)
myset
```


    {1, 2, 3}

<br />


```python
myset.add(4)
myset
```


    {1, 2, 3, 4}

<br />



### 3-3. 값 제거 -- ".remove" / ".clear"

**부분 제거 -- ".remove"**


```python
myset  
```


    {1, 2, 3, 4}

<br />


```python
myset.remove(3)
```


```python
myset
```


    {1, 2, 4}

<br /> 

**전부 제거 -- ".clear"**


```python
mylist.clear()
```


```python
mylist
```


    []

<br />

<br />

## **4. dict (사전형 집합, key와 value 쌍)**

### 4-1. { } 형태로 표헌


```python
mydict = dict()
```


```python
mydict
```


    {}

<br />


```python
type(mydict)
```


    dict

<br />



### 4-2. 값 추가 (key와 value 모두 지정)

* mydict [ " *key* " ] = *value*
* key는 문자형 (str) / 숫자형 (int & float) 모두 가능


```python
mydict["apple"] = 123
```

<br />

```python
mydict
```


    {'apple': 123}


```python
mydict["apple"]
```


    123

<br />


```python
mydict[0] = 2
```

<br />

```python
mydict
```


    {'apple': 123, 0: 2}


```python
mydict[0]
```


    2

<br />


```python
mydict[3.14] = 1
```

<br />

```python
mydict
```


    {'apple': 123, 0: 2, 3.14: 1}


```python
mydict[3.14]
```


    1

<br />



### 4-3. 값 바꾸기

새 값을 해당 key에 할당하기


```python
mydict["apple"] = "hello"
```


```python
mydict
```


    {'apple': 'hello', 0: 2, 3.14: 1}

<br />



### 4-4. 값 제거 -- ".pop" / ".clear"

**부분 제거 -- ".pop"**


```python
mydict.pop('apple')
```


    'hello'


```python
mydict
```


    {0: 2, 3.14: 1}

<br />


```python
mydict.pop(0)
```


    2


```python
mydict
```


    {3.14: 1}

<br />

**전부 제거 -- ".clear"**


```python
mydict.clear()
```


```python
mydict
```


    {}

<br />



### 4-5. 길이 파악하기

```python
mydict["apple"] = 123
mydict[0] = 2
mydict[3.14] = 1
```

<br />

```python
mydict
```


    {'apple': 'hello', 0: 2, 3.14: 1}

<br />


```python
len(mydict)
```


    3

  <br />

  <br />
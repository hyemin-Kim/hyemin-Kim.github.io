---
uuid: 0f98cf60-e893-3551-d5c8-2a6a4b4ce398
title: Python 기초문법 - (4) 비교/논리 연산자. 조건문. 반복문
tags: 
 - Python
 - Python_Base
categories: [【STUDY - Python】, Python - 0. Base]
description: 비교연산자. 조건문. 논리연산자. 반복문
cover: https://ih1.redbubble.net/image.452049706.1381/flat,750x,075,f-pad,750x1000,f8f8f8.u5.jpg
abbrlink: 42102
date: 2020-05-13 17:25:46
---

비교연산자. 조건문. 논리연산자. 반복문
<!-- more -->

# 목록

@[toc]

<br />

## **1. 비교연산자**

비교 연산자는 주로 대소비교를 할 때 사용한다.

### 1-1. 대소비교 >, >=, <, <=


```python
1 > 2
```


    False

<br />


```python
10 >= 10
```


    True

<br />


```python
9 < 10
```


    True

<br />


```python
8 <= 7
```


    False

<br /><br />

  

### 1-2. 같다 ==

* **주의:** = 는 대입연산자. == 는 비교연산자 중의 "같다"
* 숫자형 & 문자형 모두 비교 가능


```python
2 = 2
```


      File "<ipython-input-6-a8e553549e25>", line 1
        2 = 2
             ^
    SyntaxError: can't assign to literal

<br />


```python
2 == 2
```


    True

<br />


```python
2 == 3
```


    False

<br />


```python
"나" == "나"
```


    True

<br />

  <br />

### 1-3. 같지 않다 !=

* 숫자형 & 문자형 모두 비교 가능


```python
2 != 2
```


    False

<br />


```python
2 != 3
```


    True

<br />


```python
"나" != "너"
```


    True

<br />

<br />  

  

## **2. 조건문**

### 2-1. 개념

주어진 조건이 **참**인 경우 그 다음 내가 규칙(로직)을 실행하는 개념이다

  <br />

### 2-2. if

* if는 어떤 조건이 성립한다면 ~이라는 의미
* if구문 끝에는 반드시 콜론( : )이 있어야 함


```python
if 5 > 3:
    print('참')
```

    참

<br />


* if구문 뒤에 indent가 있는 명령어는 if조건이 성립하면 실행
* indent가 없으면 if의 성립여부와 무관하여 무조건 실행


```python
if 5 > 3:
    print('참')
    print('참')
   
print('끝')  
```

    참
    참
    끝

<br />

```python
if 5 < 3:
    print('참')
    print('참')
   
print('끝')  # 앞에 indent가 없으면 if의 성립여부와 무관하여 실행  
```

    끝

<br />

<br />


### 2-3. else

else는 if 조견 후에 따라오면, if가 아닌 경우에 실행 됨


```python
if 5 < 3:
    print("성립한다")
else:
    print("성립하지 않은다")
```

    성립하지 않은다

<br />

else는 꼭 if랑 같이 써야함. 단독으로 실행할 수 없음


```python
else:
    print("성립하지 않은다")
```


      File "<ipython-input-22-6c0f4debaa4b>", line 1
        else:
           ^
    SyntaxError: invalid syntax

<br />

  <br />

### 2-4. elif

elif구문은 3가지 이상 문기(조건)의 동작을 수행할 때 사용


```python
if 3 > 5:
    print('if 구문')
elif 3 < 4:
    print('elif 구문')
else:
    print('이것도 저것도 아니다')
```

    elif 구문

<br />


그럼, elif구문이 참인 여러 구문을 나열 했을 때는 어떻게 될까?


```python
if 3 > 5:
    print('if 구문')
elif 3 < 4:
    print('elif 1 구문')
elif 3 < 5:
    print('elif 2 구문')
elif 3 < 6:
    print('elif 3 구문')
else:
    print('이것도 저것도 아니다')
```

    elif 1 구문


elif구문이 참인 여러 구문을 나열 했을 때는 **첫번째 참인 elif구문만** 실행됨

 <br /><br />

### 2-5. 1이나 0은 참이나 거짓을 표현하기도 한다


```python
if 1:
    print('참')
else:
    print('거짓')
```

    참

<br />

```python
if 0:
    print('참')
else:
    print('거짓')
```

    거짓

<br />

<br />


## **3. 논리 연산자 (and, or)**

**and**나 **or**조건은 두 가지 이상 조건을 다룰 때 활용한다

  <br />

### 3-1. and

and 조건은 **모두 만족**할 때 **참**으로 인식한다


```python
True and True and True
```


    True

<br />


```python
True and False and True
```


    False

<br />


```python
if (0 < 1) and (0 < 2):
    print('모두 참')
else:
    print('거짓')
```

    모두 참

<br />

```python
if (0 < 1) and (0 > 2):
    print('모두 참')
else:
    print('거짓')
```

    거짓

<br />

<br />


### 3-2. or

or조건은 조건 중 **하나라도 만족**할 때 **참**으로 인식한다


```python
True or False or False
```


    True

<br />


```python
False or False or False
```


    False

<br />


```python
if (0 < 1) or (0 > 2):
    print('하나라도 참')
else:
    print('모두 거짓')
```

    하나라도 참

<br />

```python
if (0 > 1) or (0 > 2):
    print('하나라도 참')
else:
    print('모두 거짓')
```

    모두 거짓

<br />
<br />

## **4. 반복문**

### 4-1. 반복문이란?

* 일을 반복 처리 해준다는 것
* 대상은 반드시 list, dict, set등 집합이어야 한다

<br />

[예]

반복문 쓰지 않을 때:


```python
mylist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

mylist에 들어 닜는 모든 값들을 출력하려고 한다면?


```python
print(mylist[0])
print(mylist[1])
print(mylist[2])
print('...')
print(mylist[8])
print(mylist[9])
```

    1
    2
    3
    ...
    9
    10


반복문은 노가다를 획기적으로 줄여주는 방법이다!

  <br />

<br />

### 4-2. for 와 in을 활용하자!

**[기본 문법]**  
for 지정한 변수명 in [꺼내올 집합]:  
    명령어


```python
mylist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```


```python
for i in mylist:
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

<br />


### 4-3. 반복문에서 짝수만 출력하려면? (continue구문)


```python
mylist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

**방법1:**


```python
for i in mylist:
    if i % 2 == 0:
        print(i)
```

    2
    4
    6
    8
    10

<br />


**방법2:**  
**continue**구문을 사용하면 조건이 충족할 때 아래 명령어를 SKIP하고 다시 다음 순환으로 넘어간다


```python
for i in mylist:
    if i % 2 == 1:
        continue
    print(i)
```

    2
    4
    6
    8
    10

<br />

<br />


### 4-4. 조건을 충족시 순환에서 빠져나와보자! (break구문)


```python
mylist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

i가 6 이상이면 STOP


```python
for i in mylist:
    if i >= 6:       # i > 6 이면 6까지 출력한다 
        break
    print(i)
```

    1
    2
    3
    4
    5

<br />

<br />
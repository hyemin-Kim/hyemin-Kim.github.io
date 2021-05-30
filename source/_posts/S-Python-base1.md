---
uuid: ceaa3615-b8a8-0bc7-468d-c20f8334eb30
title: Python 기초문법 - (1) 출력. 데이터 타입. 데이터의 응용
tags: 
 - Python
 - Python - Base
categories: [【STUDY - Python】, Python - 0. Base]
description: 출력. 변수 할당. 데이터 타입. 데이터의 응용 (사칙연산, 문자열 연결). 데이터 타입의 변환.
cover: https://ih1.redbubble.net/image.452049706.1381/flat,750x,075,f-pad,750x1000,f8f8f8.u5.jpg
abbrlink: 51063
date: 2020-05-12 02:18:11
---

출력. 변수. 데이터 타입. 데이터의 응용. 데이터 타입의 변환.
<!-- more -->

# **목록**

@[toc]

<br />

## **1. 출력 (print)**

### **print( ) 함수**

1. 숫자를 출력할 때 따움표(' ' or " ") 필요없음
2. 문자를 출력할 때 따움표 필요
   *  ' ' 와 " "  차이없음
   *  '''  ''' 를 사용하면 출력시 "줄 바꿈" 형식이 보류될 수 있음 


```python
print(1)
```

    1

<br />

```python
print(1+2)
```

    3

<br />

```python
print('안녕하세요')
```

    안녕하세요

<br />

```python
print("반갑습니다")
```

    반갑습니다

<br />

```python
print('''
안녕하세요,
반갑습니다.
''')
```


    안녕하세요,
    반갑습니다.

<br />

<br />


## **2. 변수와 대입**


### 2-1. 변수의 이름

#### 【가능한 경우】 

case 1. 알파벳


```python
a = 1
```


```python
A = 1
```

case 2. 알파벳 + 숫자


```python
a1 = 1
```

case 3. 알파벳 + 언더바(_)


```python
a_ = 1
```

case 4. 언더바(_) + 알파벳


```python
_a = 1
```

<br />

#### 【불가한 경우】

**case 1. 언더바(_)를 제외한 특수문자**


```python
* = 1
```


      File "<ipython-input-23-6d0163a9fd4c>", line 1
        * = 1
          ^
    SyntaxError: invalid syntax

<br />

**case 2. 알파벳 + 언더바를 제외한 특수문자**


```python
a$ = 1
```


      File "<ipython-input-25-2501fc576aab>", line 1
        a$ = 1
         ^
    SyntaxError: invalid syntax

<br />

**case 3. 변수의 이름 사이의 공백**


```python
a b = 1
```


      File "<ipython-input-26-2bab97d7970c>", line 1
        a b = 1
          ^
    SyntaxError: invalid syntax

<br /><br />

### 2-2. 변수의 대입

변수 값을 부여할 때 "="를 사용한다


```python
a = 1
```

  <br />

### 2-3. 변수의 출력

1. print() 구문 사이에 **값을 직접** 입력하면, 바로 값이 출력됨.


```python
print(123)   # 숫자는 "" 필요없음
```

    123

<br />

```python
print("text")   # 문자는 "" 필요함
```

    text

<br />


2. print()구분 사이에 **변수 이름**을 입력하면, 변수의 값이 출력됨.


```python
a = 123
print(a)
```

    123

<br />

```python
b = "text"
print(b)
```

    text

<br />

 <br /> 

## **3. 데이터 타입**

**데이터 type:**
    1. int(정수)
    2. float(실수)
    3. str(문자열)
	4. bool(참/거짓)

<br />

### 3-1. int(정수)


```python
a = 1
```


```python
type(a)
```


    int


```python
print(a)
```

    1

<br />

**코딩에서 1은 참으로 취급, 0은 거짓으로  취급**

  다음 코딩으로 진단해보자:


```python
if 1:
    print('1은 참으로 취급')
else:
    print('1은 거짓부렁이')
```

    1은 참으로 취급

<br />

```python
if 0:
    print('0은 참으로 취급')
else:
    print('0은 거짓부렁이')
```

    0은 거짓부렁이

<br />

```python
if 123:
    print('123은 참으로 취급')
else:
    print('123은 거짓부렁이')
```

    123은 참으로 취급


[0 이외의 정수 다 참으로 취급]

<br />

<br />  

### 3-2. float(실수)


```python
a = 3.14
```


```python
type(a)
```


    float


```python
print(a)
```

    3.14

<br />


### 3-3. str 혹은 object (문자열)

1. **문자열은 반드시 ' ' 혹은 " " 로 묶어야 함**


```python
word = '안녕하세요'
```

```python
type(word)
```

    str


```python
print(word)
```

    안녕하세요

<br />

```python
word = "안녕하세요"
```

```python
type(word)
```

    str


```python
print(word)
```

    안녕하세요

<br />

2. **'" "' 를 사용하면 출력시 "줄 바꿈" 형식이 보류될 수 있음**


```python
print('''
안녕하세요,
반갑습니다.
''')
```


    안녕하세요,
    반갑습니다.

   <br /> <br />

### 3-4. bool (참/거짓)

참:   True  
거짓: False


```python
a = True
```

```python
a
```

    True


```python
type(a)
```


    bool

<br />


```python
b = False
```

```python
b
```

    False


```python
type(b)
```


    bool

<br />


```python
1 == True
```


    True

<br />


```python
0 == False
```


    True

<br />


```python
123 == True 
```


    False

* 1 이외의 정수는 조건절에서 참으로 인식되지만, bool과 비교할 때 참이 아니다 

<br />

<br />


### 3-5. 아무것도 아닌 None타입도 있다

Null값을 넣는다고도 한다.

* Null: Nullify (무효화하다) -- 사전상 의미  

Python에서는 **None** 입니다 


```python
a = None
```


```python
print(a)
```

    None

```python
type(a)
```


    NoneType

<br />

조건문에 None이라면?


```python
if None:
    print("None은 참으로 취급")
else:
    print("None은 거짓부렁이")
```

    None은 거짓부렁이

<br />

<br />


## **4. 데이터의 응용**

### 4-1. 사칙 연산자

| 연산자 |  의미  |      예      |
| :----: | :----: | :----------: |
|   +    | 더하기 |  2 + 1 -> 3  |
|   -    |  빼기  | 1 - 2 -> -1  |
|   *    | 곱하기 |  1 * 2 -> 2  |
|   /    | 나누기 | 1 / 2 -> 0.5 |
|   //   |   몫   | 5 // 2 -> 2  |
|   %    | 나머지 |  5 % 2 -> 1  |
|   **   |   멱   |  2**3 -> 8   |

  <br />

 

### 4-2. 문자열의 연결

여러 개 문자열을 "+"을 통해 연결할 수 있다


```python
subject = "나는 "
object = "치킨을 "
verb = "좋아한다"

print(subject + object + verb)
```

    나는 치킨을 좋아한다

<br />


하지만 문자열(str)과 숫자(int & float)는 *직접*  연결할 수 없다


```python
a = "내가 "
b = "친구랑 "
c = 12
d = "시에 "
e = "보기로 했다"

print(a + b + c + d + e)
```


    ---------------------------------------------------------------------------
    
    TypeError                                 Traceback (most recent call last)
    
    <ipython-input-82-34cd0f9ce519> in <module>
          5 e = "보기로 했다"
          6 
    ----> 7 print(a + b + c + d + e)


    TypeError: can only concatenate str (not "int") to str


이 때는 데이터 타입을 변환할 필요가 있다

<br />
<br />

 

## **5. 데이터 타입 변환**

### 5-1. 문자열로 변환:  "str( ) 함수"  or  "따움표"


```python
type(6)
```


    int

<br />


```python
type(str(6))
```


    str

<br />


```python
type('6')
```


    str

<br />


```python
type(3.14)
```


    float

<br />


```python
type(str(3.14))
```


    str

<br />


```python
type("3.14")
```


    str

<br />


```python
a = "내가 "
b = "친구랑 "
c = 12
d = "시에 "
e = "보기로 했다"
```


```python
print(a + b + str(c) + d + e)
```

    내가 친구랑 12시에 보기로 했다

<br />

```python
print(a + b + '12' + d + e)a
```

    내가 친구랑 12시에 보기로 했다

<br />

<br />

### 5-2. 정수로 변환: " int( ) 함수"

1. **"str" --> "int":  str( ) 안 내용이 정수일 때만 가능**


```python
type(int("2"))
```


    int

<br />


```python
number1 = "2"
number2 = "3"
```


```python
print(int(number1) + int(number2))
```

    5

<br />

```python
print(int("2.6"))
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-103-f4645c45f771> in <module>
    ----> 1 print(int("2.6"))


    ValueError: invalid literal for int() with base 10: '2.6'

<br />

2. **"float" --> "int": 소수점 버림**


```python
type(int(3.6))
```


    int

<br />


```python
print(int(3.6))
```

    3

<br />

<br />


### 5-3. 실수로 변환: "float( ) 함수"

1. **"str" --> "float":  str( ) 안 내용이 정수일 때만 가능**


```python
type(float("3.14"))
```


    float

<br />


```python
print(float("3.14"))
```

    3.14

<br />

2. **"int" --> "float": 소수점 하나 추가**


```python
type(float(178))
```


    float

<br />


```python
print(float(178))
```

    178.0

<br />

<br />
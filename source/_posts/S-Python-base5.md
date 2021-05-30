---
uuid: 7dcf94fd-a0cd-aad4-1551-157c898ec6cd
title: Python 기초문법 - (5) List Comprehension. 문자열
tags:
  - Python
  - Python_Base
categories: [【STUDY - Python】, Python - 0. Base]
description: List Comprehension.  문자열을 가지고 노는 방법.
cover: https://ih1.redbubble.net/image.452049706.1381/flat,750x,075,f-pad,750x1000,f8f8f8.u5.jpg
abbrlink: 58679
date: 2020-05-14 01:37:58
---

List Comprehension (List에 조건필터를 적용).  문자열을 가지고 노는 방법.

<!-- more -->

# **목록**

@[toc]

<br />

## **1. List Comprehension (파이썬 고유의 아름다운 문법)**

* for ~ in 구조를 기본적으로 가지고 있다

* List Comprehension 이니까 당연히 List를 사용한다

  <br />

**[실제 사례 연구]**

mylist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] 이라는 list를 만들어 주고  
우리는 이 중 짝수만 출력하고 싶으면 아래와 같이 쓸 수 있다:


```python
mylist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```


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

그럼 mylist에서 짝수만 뽑아서 **list로 만들어** 주고 싶다면:


```python
mylist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even = []

for i in mylist:
    if i % 2 == 0:
        even.append(i)

print(even)
```

    [2, 4, 6, 8, 10]

<br />

이렇게 for in 문으로 해줄 수 있다.  
하지만, 우리는 **list comprehension을 통해 더욱 쉽게 해결** 할 수 있다!! 

<br />

 <br /> 

### 1-1. list comprehension 조건필터


```python
mylist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

<br />

아래 문법이 바로 list comprehension 이다. 한 줄로 해결해 버리는 것이 매력임!


```python
even = [i for i in mylist if i % 2 == 0]
```


```python
even
```


    [2, 4, 6, 8, 10]

<br />

<br />  

### 1-2. [STEP 1] list를 만들어야 하니 일단 꺾쇠[ ]를 씌운다

* 꺾쇠 안에 **반복문이 들어간다**  
* 반복문을 돌면서 return 된 i값을 list에 넣는 원리이기 때문에 **for구분 앞에 i를 써준다**


```python
even = [i for i in mylist]
```


```python
even
```


    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

<br />

<br />  

### 1-3. [STEP 2] 조건 필터를 걸어 준다

[i for i in mylist (이곳에 조건문)] 


```python
[i for i in mylist if i % 2 == 0]
```


    [2, 4, 6, 8, 10]

<br />

이것을 변수에 다시 할당해주면 끝!


```python
even = [i for i in mylist if i % 2 == 0]
```


```python
even
```


    [2, 4, 6, 8, 10]

<br />

<br />  

### 1-4. [응용 STEP] 변수 값을 가공할 수도 있다

**예를 들어:**  

mylist의 모든 값에 +2를 하고 다시 even이라는 list에 저장하고 싶다면


```python
mylist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```


```python
even = [i+2 for i in mylist]
```


```python
even
```


    [3, 4, 5, 6, 7, 8, 9, 10, 11, 12]

<br />

<br />  

  

## **2. 문자열(string)을 가지고 놀기**

### 2-1. 문자의 길이


```python
a = 'banana'
```


```python
len(a)
```


    6

<br />


```python
a = 'banana pen'
```


```python
len(a)  # 공백도 count된다
```


    10

<br />


```python
b = '한글'
```


```python
len(b)
```


    2

<br />


```python
b = '한글 바나나'
```


```python
len(b)
```


    6

<br />

<br />  

### 2-2. 문장 쪼개기 -- ".split"

* split은 문장을 특정 규칙에 의해 쪼개 주는 기능을 한다
* **명령어:**  변수명.split('*쪼개는 기준*')
* 쪼개는 기준이 설정되어 있지 않으면 그냥 '빈칸'으로 인식된다


```python
a = 'This is a pen'
```


```python
a.split(' ')
```


    ['This', 'is', 'a', 'pen']

<br />


```python
a.split()
```


    ['This', 'is', 'a', 'pen']

<br />  

```python
b = 'This-is-a-pen'
```


```python
b.split('-')
```


    ['This', 'is', 'a', 'pen']

<br />

* return된 값을 list형식으로 저장한다


```python
aa = a.split(' ')
```

```python
aa
```


    ['This', 'is', 'a', 'pen']

<br />

```python
aa[0]
```


    'This'

<br />


```python
aa[2]
```


    'a'

<br />


```python
aa[0] + aa[2]
```


    'Thisa'

<br />

```python
c = '한글은 어떻게 될까요?'
```


```python
c.split()
```


    ['한글은', '어떻게', '될까요?']

<br />

  <br /> 

### 2-3. 대문자 / 소문자로 만들기 -- ".upper" / ".lower"


```python
a = 'My name is hyemin'
```


```python
a.upper()
```


    'MY NAME IS HYEMIN'

<br />


```python
a.lower()
```


    'my name is hyemin'

<br />


```python
b = '한글엔 대소문자가 없어요ㅠ'
```


```python
b.upper()
```


    '한글엔 대소문자가 없어요ㅠ'

<br />


```python
b.lower()
```


    '한글엔 대소문자가 없어요ㅠ'

<br />

 <br /> 

### 2.4. ~로 시작하는, ~로 끝나는 -- ".startswith" , ".endswith"


```python
a = '01-sample.png'
b = '02-sample.jpg'
c = '03-sample.pdf'
```


```python
a.startswith('01')
```


    True

<br />


```python
a.endswith('.jpg')
```


    False

<br />


```python
b.endswith('.jpg')
```


    True

<br />

조건(혹은 형식)에 맞는 파일을 추출하고 싶을 때:


```python
mylist = [a, b]
```


```python
for file in mylist:
    if file.endswith('jpg'):
        print(file)
```

    02-sample.jpg

<br />

<br />


### 2-5. 바꾸기 -- ".replace('바꿀 대상, 바꿔야할 값')"

**[예]**   file형식을 바꾸고 싶다면:


```python
a = '01-sample.png'
```


```python
a.replace('.png', '.jpg')
```


    '01-sample.jpg'

<br />

이 때 a의 값이 변하지 않아. 다시 할당 해야 함


```python
a
```


    '01-sample.png'

<br />


```python
a_new = a.replace('.png', '.jpg')  # 새로 지정
```


```python
a_new
```


    '01-sample.jpg'

<br />


```python
a = a.replace('.png', '.jpg')  # 덮어쒸우기
```


```python
a
```


    '01-sample.jpg'

<br />

<br />    

### 2-6. 불필요한 공백 제거하기 -- ".strip"

**[예]**


```python
a = '   01-sample.png'
b = '01-sample.png'
```


```python
a == b
```


    False

<br />

strip은 양 끝 불필요한 공백을 제거해 줌.


```python
a.strip()
```


    '01-sample.png'

<br />


```python
a.strip() == b
```


    True

<br /><br />
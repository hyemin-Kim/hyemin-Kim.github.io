---
title: Python >> Matplotlib - (1) 기본 canvas 그리기 및 스타일링
tags:
  - Python
  - Matplotlib
  - 시각화
categories: 
  - [【STUDY - Python】, Python - 3. Matplotlib]
  - [【STUDY - Python】, Python - 시각화]
cover: 'https://s1.ax1x.com/2020/06/28/NgUVOS.png'
typora-root-url: ..
abbrlink: 10197
date: 2020-06-28 14:12:24
---

# 기본적인 canvas 그리기 및 스타일링

  @[toc]

<br />

>  ***reference:*** [pyplot 공식 Document 살펴보기](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot)

<br />

```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
```


```python
# plt.rcParams["figure.figsize"] = (12, 9)  # figure size 설정
```

  <br />

## **1. 밑 그림 그리기**

### 1-1. 단일 그래프 (single graph)

> **plt.plot**(*df_name*)  
> **plt.show()** 


```python
## data 생성
data = np.arange(1, 100)

## plot
plt.plot(data)

## 그래프만 보여주는 코드 (타 실행 결과 생략하고 그래프만 보여줌)
plt.show()
```


![png](/images/S-Python-Matplotlib1/output_10_0.png)

<br />

### 1-2. 다중 그래프 (multiple graphs)

> * **여러 그래프를 같은 canvas 안에 그리기:**  
>    명령어 ```plt.plot(df_name)``` 를 연속 사용
> * **새 그래프를 새로운 canvas 안에 그리기:**  
>    세 그래프를 그리기 전에 ```plt.figure()```명령어를 추가

<br />

**(1) 1개의 canvas 안에 다중 그래프 그리기**


```python
data1 = np.arange(1, 51)
data2 = np.arange(51, 101)


plt.plot(data1)
plt.plot(data2)
plt.plot(data2 + 50)

plt.show()
```


![png](/images/S-Python-Matplotlib1/output_15_0.png)

<br />


**(2) 새로운 canvas에서 새 그래프를 그리기**

* figure()는 새로운 그래프 canvas를 생성한다


```python
data1 = np.arange(100, 201)
data2 = np.arange(200, 301)

plt.plot(data)

plt.figure()   # figure() 명령어를 추가
plt.plot(data2)
plt.plot(data2 + 50)

plt.show()
```


![png](/images/S-Python-Matplotlib1/output_19_0.png)



![png](/images/S-Python-Matplotlib1/output_19_1.png)

<br />

### 1-3. 그래프 배열 (subplot / subplots)

> 여러 개 plot을 지정된 행,열수에 따라 배열해주기:
>
> * plt.subplot(row, column, index)   <font color = 'blue'># 각 plot의 좌표 설정</font>
> * plt.subplots(행의 갯수, 열의 갯수)  <font color = 'blue'># 행,열수 설정</font>

  <br />

**(1) subplot (plot의 좌표를 설정하기)**

이 방법은 **그래프마다 설정**해줘야 함

> **plt.subplot**(row, column, index)  <font color = 'blue'># 콤마를 제거해도 됨</font>

```python
data1 = np.arange(100, 201)
plt.subplot(2, 1, 1)
plt.plot(data1)

data2 = np.arange(200, 301)
plt.subplot(2, 1, 2)
plt.plot(data2)

plt.show()
```


![png](/images/S-Python-Matplotlib1/output_27_0.png)

<br />


위의 코드와 동일하나, "콤마"를 제거한 상태


```python
data1 = np.arange(100, 201)
plt.subplot(211)   # 콤마를 생략함: 211 -> row : 2, col: 1, index : 1
plt.plot(data1)

data2 = np.arange(200, 301)
plt.subplot(212)   # 콤마를 생략함
plt.plot(data2)

plt.show()
```


![png](/images/S-Python-Matplotlib1/output_30_0.png)

<br />



```python
data1 = np.arange(100, 201)
plt.subplot(1, 3, 1)
plt.plot(data1)

data2 = np.arange(200, 301)
plt.subplot(1, 3, 2)
plt.plot(data2)

data3 = np.arange(300, 401)
plt.subplot(1, 3, 3)
plt.plot(data3)

plt.show()
```


![png](/images/S-Python-Matplotlib1/output_32_0.png)

<br />


**(2) subplots (배열 기준인 행,열수를 지정하기)**

subplot와 다르게 **subplots()명령어는 한번만 설정**해주면 됨

> **plt.subplots**(행의 갯수, 열의 갯수)

```python
data = np.arange(1, 51)

# 밑 그림
fig, axes = plt.subplots(2, 3)

# plot
axes[0, 0].plot(data)
axes[0, 1].plot(data * data)
axes[0, 2].plot(data ** 3)  # data^3
axes[1, 0].plot(data % 10)
axes[1, 1].plot(-data)
axes[1, 2].plot(data // 20)

plt.tight_layout()
plt.show()
```


![png](/images/S-Python-Matplotlib1/output_37_0.png)

<br />

<br />


## **2. 주요 스타일 옵션**


```python
from IPython.display import Image

# 출처: matplotlib.org
Image('https://matplotlib.org/_images/anatomy.png')
```



<img src="/images/S-Python-Matplotlib1/output_41_0.png" alt="png" style="zoom:67%;" />



<br />  

### 2-1. 타이틀

> * **타이틀 추가:** plt.title("...")
> * **타이틀 fontsize 설정:**  plt.title("...",  fontsize = .. ) 


```python
plt.plot([1,2,3], [3,6,9])
plt.plot([1,2,3], [2,4,9])

plt.title("이것은 타이틀 입니다")
```


    Text(0.5, 1.0, '이것은 타이틀 입니다')




![png](/images/S-Python-Matplotlib1/output_46_1.png)



<br />

```python
plt.plot([1,2,3], [3,6,9])
plt.plot([1,2,3], [2,4,9])

plt.title("타이틀 fontsize를 키웁니다", fontsize = 20)
```


    Text(0.5, 1.0, '타이틀 fontsize를 키웁니다')




![png](/images/S-Python-Matplotlib1/output_48_1.png)

<br />

### 2-2. X, Y축 Label 설정

> * **plt.xlabel** ( "*x_name*", fontsize = ..)
> * **plt.ylabel** ( "*y_name*", fontsize = ..)

```python
plt.plot([1,2,3], [3,6,9])
plt.plot([1,2,3], [2,4,9])

# 타이틀 설정
plt.title("Label 설정 예제", fontsize = 16)

# X축 & Y축 Label 설정
plt.xlabel("X축", fontsize = 16)
plt.ylabel("Y축", fontsize = 16)
```


    Text(0, 0.5, 'Y축')




![png](/images/S-Python-Matplotlib1/output_52_1.png)

<br />


### 2-3. X, Y축 Tick 조정 (rotation)

Tick은 X, Y축에 위치한 눈금을 말한다  
rotation 명령어를 통해 Tick의 각도를 조절할 수 있다



> * **plt.xticks** ( *rotation = ..* )
> * **plt.yticks** ( *rotation = ..* )  
>   Rotation 각도는 <font color = 'blue'>역시개방향 회전각도</font>를 말한다

 <br /> 


```python
plt.plot(np.arange(10), np.arange(10)*2)
plt.plot(np.arange(10), np.arange(10)**2)
plt.plot(np.arange(10), np.log(np.arange(10)))

# title
plt.title("X, Y축 Tick 조정", fontsize = 16)

# X축, Y축 Label 설정
plt.xlabel("X축", fontsize = 16)
plt.ylabel("Y축", fontsize = 16)

# X tick, Y tick rotation 조정
plt.xticks(rotation = 90)
plt.yticks(rotation = 30)
```

    D:\Anaconda\lib\site-packages\ipykernel_launcher.py:3: RuntimeWarning: divide by zero encountered in log
      This is separate from the ipykernel package so we can avoid doing imports until
    
    (array([-10.,   0.,  10.,  20.,  30.,  40.,  50.,  60.,  70.,  80.,  90.]),
     <a list of 11 Text yticklabel objects>)

<br />


![png](/images/S-Python-Matplotlib1/output_58_2.png)

<br />

### 2-4. 범례 (Legend) 설정

> **plt.legend** ( [ "*name1*" , "*name2*" , ... ], fontsize = ...)


```python
plt.plot(np.arange(10), np.arange(10)*2)
plt.plot(np.arange(10), np.arange(10)**2)
plt.plot(np.arange(10), np.log(np.arange(10)))

# title
plt.title("범례(Legend) 설정", fontsize = 16)

# X축, Y축 Label 설정
plt.xlabel("X축", fontsize = 16)
plt.ylabel("Y축", fontsize = 16)

# X tick, Y tick rotation 조정
plt.xticks(rotation = 90)
plt.yticks(rotation = 30)

# legend 설정
plt.legend(["2x", "x^2", "logx"], fontsize = 14)
            
```

    D:\Anaconda\lib\site-packages\ipykernel_launcher.py:3: RuntimeWarning: divide by zero encountered in log
      This is separate from the ipykernel package so we can avoid doing imports until
    
    <matplotlib.legend.Legend at 0x173a5712888>




![png](/images/S-Python-Matplotlib1/output_63_2.png)

<br />


### 2-5. X와 Y의 한계점(Limit) 설정

> * **plt.xlim** ( *a, b* )
> * **plt.ylim** ( *c, d* )


```python
plt.plot(np.arange(10), np.arange(10)*2)
plt.plot(np.arange(10), np.arange(10)**2)
plt.plot(np.arange(10), np.log(np.arange(10)))

# title
plt.title("X축, Y축 Limit 설정", fontsize = 16)

# X축, Y축 Label 설정
plt.xlabel("X축", fontsize = 16)
plt.ylabel("Y축", fontsize = 16)

# X tick, Y tick rotation 조정
plt.xticks(rotation = 90)
plt.yticks(rotation = 30)

# legend 설정
plt.legend(["2x", "x^2", "logx"], fontsize = 14)

# x, y limit 설정
plt.xlim(0, 5)
plt.ylim(0, 20)
```

    D:\Anaconda\lib\site-packages\ipykernel_launcher.py:3: RuntimeWarning: divide by zero encountered in log
      This is separate from the ipykernel package so we can avoid doing imports until
    
    (0, 20)




![png](/images/S-Python-Matplotlib1/output_68_2.png)

<br />


### 2-6. 스타일 세부 설정 - 마커, 라인, 컬러

> ***reference:***  [세부 Document 확인하기](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot)

스타일 세부 설정은 마커, 선의 동류 설정, 드리고 컬러가 있으며, 문다열로 세부설정을 하게 된다

  <br />

**(1) marker의 종류**

* '.'	point marker
* ','	pixel marker
* 'o'	circle marker
* 'v'	triangle_down marker
* '^'	triangle_up marker
* '<'	triangle_left marker
* '>'	triangle_right marker
* '1'	tri_down marker
* '2'	tri_up marker
* '3'	tri_left marker
* '4'	tri_right marker
* 's '	square marker
* 'p'	pentagon marker
* '*'	star marker
* 'h'	hexagon1 marker
* 'H'	hexagon2 marker
* '+'	plus marker
* 'x'	x marker
* 'D'	diamond marker
* 'd'	thin_diamond marker
* '|'	vline marker
* '_'	hline marker


```python
# marker 스타일 설정
plt.plot(np.arange(10), np.arange(10)*2, marker='o', markersize=5)
plt.plot(np.arange(10), np.arange(10)*2 - 10, marker='v', markersize=10)
plt.plot(np.arange(10), np.arange(10)*2 - 20, marker='+', markersize=15)
plt.plot(np.arange(10), np.arange(10)*2 - 30, marker='*', markersize=20)

# 타이틀 & font 설정
plt.title('마커 스타일 예제', fontsize=20)

# X축 & Y축 Label 설정
plt.xlabel('X축', fontsize=20)
plt.ylabel('Y축', fontsize=20)
```


    Text(0, 0.5, 'Y축')




![png](/images/S-Python-Matplotlib1/output_75_1.png)

<br />


**(2) line의 종류**

* '-' solid line style
* '--' dashed line style
* '-.' dash-dot line style
* ':' dotted line style


```python
# line 스타일 설정
plt.plot(np.arange(10), np.arange(10)*2, marker='o', linestyle='')
plt.plot(np.arange(10), np.arange(10)*2 - 10, marker='o', linestyle='-')
plt.plot(np.arange(10), np.arange(10)*2 - 20, marker='v', linestyle='--')
plt.plot(np.arange(10), np.arange(10)*2 - 30, marker='+', linestyle='-.')
plt.plot(np.arange(10), np.arange(10)*2 - 40, marker='*', linestyle=':')

# 타이틀 & font 설정
plt.title('다양한 선의 종류 예제', fontsize=20)

# X축 & Y축 Label 설정
plt.xlabel('X축', fontsize=20)
plt.ylabel('Y축', fontsize=20)
```


    Text(0, 0.5, 'Y축')




![png](/images/S-Python-Matplotlib1/output_78_1.png)

<br />


**(3) color의 종류**

* 'b'	blue
* 'g'	green
* 'r'	red
* 'c'	cyan
* 'm'	magenta
* 'y'	yellow
* 'k'	black
* 'w'	white
* more choices: [matplotlib.colors](https://matplotlib.org/api/colors_api.html#module-matplotlib.colors)   *(e.g. "purple", "#008000")*


```python
# color 설정
plt.plot(np.arange(10), np.arange(10)*2, marker='o', linestyle='-', color='b')
plt.plot(np.arange(10), np.arange(10)*2 - 10, marker='v', linestyle='--', color='c')
plt.plot(np.arange(10), np.arange(10)*2 - 20, marker='+', linestyle='-.', color='y')
plt.plot(np.arange(10), np.arange(10)*2 - 30, marker='*', linestyle=':', color='r')

# 타이틀 & font 설정
plt.title('색상 설정 예제', fontsize=20)

# X축 & Y축 Label 설정
plt.xlabel('X축', fontsize=20)
plt.ylabel('Y축', fontsize=20)
```


    Text(0, 0.5, 'Y축')




![png](/images/S-Python-Matplotlib1/output_81_1.png)

<br />

**(4) Format: '[marker][line][color]'**

example:  

* 'b'    # blue markers with default shape
* 'or'   # red circles
* '-g'   # green solid line
* '--'   # dashed line with default color
* '^k:'  # black triangle_up markers connected by a dotted line

Each of them is optional. If not provided, the value from the style cycle is used. Exception: If line is given, but no marker, the data will be a line without markers.

<br />  


```python
# "marker + line + color" format 설정
plt.plot(np.arange(10), np.arange(10)*2, "o-r")
plt.plot(np.arange(10), np.arange(10)*2 - 10, 'v--b')
plt.plot(np.arange(10), np.arange(10)*2 - 20, '+y')
plt.plot(np.arange(10), np.arange(10)*2 - 30, ':k')

# 타이틀 & font 설정
plt.title('marker/line + color 설정 예제', fontsize=20)

# X축 & Y축 Label 설정
plt.xlabel('X축', fontsize=20)
plt.ylabel('Y축', fontsize=20)
```


    Text(0, 0.5, 'Y축')




![png](/images/S-Python-Matplotlib1/output_87_1.png)

<br />

**(5) 색상 투명도 설정**  

* alpha = .. (0.0 ~ 1.0)


```python
# color 투명도 설정
plt.plot(np.arange(10), np.arange(10)*2, color='b', alpha=0.1)
plt.plot(np.arange(10), np.arange(10)*2 - 10, color='b', alpha=0.3)
plt.plot(np.arange(10), np.arange(10)*2 - 20, color='b', alpha=0.6)
plt.plot(np.arange(10), np.arange(10)*2 - 30, color='b', alpha=1.0)

# 타이틀 & font 설정
plt.title('투명도 (alpha) 설정 예제', fontsize=20)

# X축 & Y축 Label 설정
plt.xlabel('X축', fontsize=20)
plt.ylabel('Y축', fontsize=20)
```


    Text(0, 0.5, 'Y축')




![png](/images/S-Python-Matplotlib1/output_90_1.png)

<br />


### 2-7. 그리드 (grid) 설정

> **그리드 (grid) 추가:** plt.grid()

```python
plt.plot(np.arange(10), np.arange(10)*2, marker='o', linestyle='-', color='b')
plt.plot(np.arange(10), np.arange(10)*2 - 10, marker='v', linestyle='--', color='c')
plt.plot(np.arange(10), np.arange(10)*2 - 20, marker='+', linestyle='-.', color='y')
plt.plot(np.arange(10), np.arange(10)*2 - 30, marker='*', linestyle=':', color='r')

# 타이틀 & font 설정
plt.title('그리드 설정 예제', fontsize=20)

# X축 & Y축 Label 설정
plt.xlabel('X축', fontsize=20)
plt.ylabel('Y축', fontsize=20)

# grid 옵션 추가
plt.grid()

```


![png](/images/S-Python-Matplotlib1/output_94_0.png)

<br />

<br />
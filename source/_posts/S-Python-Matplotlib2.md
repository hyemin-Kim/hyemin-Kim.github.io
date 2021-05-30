---
title: Python >> Matplotlib - (2) 다양한 그래프 그리기
tags:
  - Python
  - Matplotlib
  - 시각화
categories: 
  - [【STUDY - Python】, Python - 3. Matplotlib]
  - [【STUDY - Python】, Python - 시각화]
cover: 'https://s1.ax1x.com/2020/06/28/NgUVOS.png'
typora-root-url: ..
description: scatterplot, barplot, line plot, areaplot, histogram, pie chart, box plot, 3D plot, imshow
abbrlink: 53476
date: 2020-06-28 14:12:32
---

# matplotlib을 활용한 다양한 그래프 그리기

@[toc]

<br />


```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
```


```python
plt.rcParams["figure.figsize"] = (9, 6)  # figure size 설정
plt.rcParams["font.size"] = 14  # fontsize 설정
```

 <br />

## **1. Scatterplot**

> ***reference:*** [<plt.scatter> Document](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.scatter.html)



> **plt.scatter**( *x, y, s=None, c=None, cmap=None, alpha=None* )
>
> * **s:** marker size
> * **c:** color
> * **cmap:** colormap
> * **alpha:** between 0 and 1

  <br />

**Data 생성**


```python
# 0~1 사이의 random value 50 개 생성
np.random.rand(50)
```


    array([0.65532609, 0.19008877, 0.72343673, 0.63981883, 0.07531076,
           0.67080518, 0.93282479, 0.04750706, 0.81240348, 0.40032198,
           0.59662026, 0.25797641, 0.37315105, 0.6266855 , 0.50732916,
           0.55803591, 0.63610033, 0.88673444, 0.99751021, 0.03723629,
           0.07695327, 0.44247   , 0.5245731 , 0.41263818, 0.8009583 ,
           0.57238283, 0.58647938, 0.9882001 , 0.88993497, 0.5396632 ,
           0.24683042, 0.0838774 , 0.0826096 , 0.89701004, 0.78305308,
           0.21027637, 0.93441558, 0.05756907, 0.6299839 , 0.05833447,
           0.24247082, 0.9057054 , 0.1585265 , 0.45569918, 0.85597115,
           0.43875418, 0.96962923, 0.17476189, 0.68713067, 0.832518  ])

<br />


```python
# 0 부터 50 개의 value 생성
np.arange(50)
```


    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
           17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33,
           34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49])



 <br /> 

### 1-1. x, y, colors, area 설정하기 
> **plt.scatter** ( *x, y, s = , c =* )
>
> * **s**: 점의 넓이. area 값이 커지면 넓이도 커진다
> * **c**: 임의 값을 color 값으로 변환

<br />

```python
x = np.random.rand(50)
y = np.random.rand(50)
colors = np.arange(50)
area = x * y * 1000

plt.scatter(x, y, s = area, c = colors)
plt.show()
```


![png](/images/S-Python-Matplotlib2/output_16_0.png)

<br />

### 1-2. cmap과 alpha

> * cmap에 컬러를 지정하면, 컬러 값을 모두 같게 가져갈 수도 있다
> * alpha값은 투명도를 나타내며 0~1 사이의 값을 지정해 둘 수 있으며, 0에 가까울 수록 투명한 값을 가진다

```python
plt.figure(figsize=(12 ,6))

plt.subplot(131)
plt.scatter(x, y, s = area, cmap = 'blue', alpha = 0.1)
plt.title('alpha = 0.1')
  
plt.subplot(132)
plt.scatter(x, y, s = area, cmap = 'blue', alpha = 0.5)
plt.title('alpha = 0.5')
    
plt.subplot(133)
plt.scatter(x, y, s = area, cmap = 'blue', alpha = 1.0)
plt.title('alpha = 1.0')

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_20_0.png)

<br />

<br />


## **2. Barplot, Barhplot**

> ***reference:*** [<plt.bar>  Document](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.bar.html)

> **plt.bar**(*x, height, width = 0.8, align = 'center', alpha = .., color = ..* )
>
> * **x:** The x coordinates of the bars
> * **height:** The height(s) of the bars
> * **width:** The width(s) of the bars (default: 0.8)
> * **align:** Alignment of the bars to the x coordinates:
>   {'center', 'edge'}

<br />

### 2-1. 기본 barplot 그리기


```python
x = ['Math', 'Programming', 'Data Science', 'Art', 'English', 'Physics']
y = [90, 60, 80, 50, 70, 40]

# figure size
plt.figure(figsize = (7,4))

# 수직 barplot
plt.bar(x, y, alpha = 0.7, color = 'red')

# title
plt.title('Subjects')

# y label
plt.ylabel('Grades')

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_28_0.png)

<br />


문자열이 겹히는 현상 발생했다. 이를 해결하는 방법은 2가지다:  

1. 문자열 화전:  plt.xtick(rotation = ..)  

2. barh(수평바 그래프) 사용

  <br /> 


```python
x = ['Math', 'Programming', 'Data Science', 'Art', 'English', 'Physics']
y = [90, 60, 80, 50, 70, 40]

# figure size
plt.figure(figsize = (7,4))

# 수직 barplot
plt.bar(x, y, alpha = 0.7, color = 'red')

# title
plt.title('Subjects')

# x ticks
plt.xticks(rotation = 20)

# y label
plt.ylabel('Grades')

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_32_0.png)

<br />


### 2-2. 기본 Barhplot 그리기

barh 함수에서는 **xticks / ylabel 로 설정**했던 부분을 **yticks / xlabel 로 변경함**

<br />


```python
x = ['Math', 'Programming', 'Data Science', 'Art', 'English', 'Physics']
y = [90, 60, 80, 50, 70, 40]

# figure size
plt.figure(figsize = (7,4))

# 수직 barplot
plt.barh(x, y, alpha = 0.7, color = 'green')

# title
plt.title('Subjects')

# y ticks
# plt.yticks(x)

# x label
plt.xlabel('Grades')

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_36_0.png)

<br />


### 2-3. Barplot에서 비교 그래프 그리기

> ***reference:*** [Grouped bar chart with labels](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/barchart.html#sphx-glr-gallery-lines-bars-and-markers-barchart-py)

**(1) barplot**


```python
x_label = ['Math', 'Programming', 'Data Science', 'Art', 'English', 'Physics']
x = np.arange(len(x_label))  # x = [0, 1, 2, 3, 4, 5]
y_1 = [90, 60, 80, 50, 70, 40]
y_2 = [80, 40, 90, 60, 50, 70]


# 넓이 지정
width = 0.35

# subplots 생성
fig, axes = plt.subplots()

# 넓이 설정
axes.bar(x - width/2, y_1, width, alpha = 0.5)
axes.bar(x + width/2, y_2, width, alpha = 0.8)

# ticks & label 설정
plt.xticks(x)
axes.set_xticklabels(x_label)
plt.ylabel('Grades')

# title
plt.title('Subjects')

# legend
plt.legend(['John', 'Peter'])

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_41_0.png)

<br />


**(2) barhplot**


```python
x_label = ['Math', 'Programming', 'Data Science', 'Art', 'English', 'Physics']
x = np.arange(len(x_label))  # x = [0, 1, 2, 3, 4, 5]
y_1 = [90, 60, 80, 50, 70, 40]
y_2 = [80, 40, 90, 60, 50, 70]

# 넓이 지정
width = 0.35

# subplots 생성
fig, axes = plt.subplots()

# 넓이 설정
axes.barh(x - width/2, y_1, width, alpha = 0.5, color = "green")
axes.barh(x + width/2, y_2, width, alpha = 0.5, color = "blue")

# ticks & label 설정
plt.yticks(x)
axes.set_yticklabels(x_label)
plt.xlabel('Grades')

# title
plt.title('Subjects')

# legend
plt.legend(['John', 'Peter'])

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_44_0.png)

<br />

<br />


## **3. Line Plot**

> **plt.plot** ( *x, y, label=.., color=.., alpha=.., marker=.., linestyle=..*)

### 3-1. 기본 lineplot 그리기


```python
x = np.arange(0, 10, 0.1)
y = 1 + np.sin(x)

plt.plot(x, y)

plt.xlabel('x value')
plt.ylabel('y value')
plt.title('sin graph', fontsize = 16)

plt.grid()

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_50_0.png)

<br />


### 3-2. 2개 이상의 그래프 그리기

* label: line 이름 (legend에 나타남)
* color: 컬러 옵션
* alpha: 투명도 옵션


```python
x = np.arange(0, 10, 0.1)
y_1 = 1 + np.sin(x)
y_2 = 1 + np.cos(x)

plt.plot(x, y_1,label='1+sin', color='blue', alpha = 0.3)  # label 설정값을 legend에 나타날 수 있음
plt.plot(x, y_2, label='1+cos', color='red', alpha = 0.7)

plt.xlabel("x value")
plt.ylabel("y value")

plt.title("sin and cos graph", fontsize = 18)
plt.grid()
plt.legend()

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_54_0.png)

<br />


### 3-3. 마커 스타일링

* marker: 마커 옵션


```python
x = np.arange(0, 10, 0.1)
y_1 = 1 + np.sin(x)
y_2 = 1+ np.cos(x)

plt.plot(x, y_1, label='1+sin', color='blue', alpha=0.3, marker='o')
plt.plot(x, y_2, label='1+cos', color='red', alpha=0.7, marker='+')

plt.xlabel('x value')
plt.ylabel('y value')

plt.title('sin and cos graph', fontsize = 18)
plt.grid()
plt.legend()

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_58_0.png)

<br />


### 3-4. 라인 스타일링

* linestyle: 라인 스타일 변경 옵션


```python
x = np.arange(0, 10, 0.1)
y_1 = 1 + np.sin(x)
y_2 = 1+ np.cos(x)

plt.plot(x, y_1, label='1+sin', color='blue', linestyle=':')
plt.plot(x, y_2, label='1+cos', color='red', linestyle='-.')

plt.xlabel('x value')
plt.ylabel('y value')

plt.title('sin and cos graph', fontsize = 18)
plt.grid()
plt.legend()

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_62_0.png)

<br />

<br />


## **4. Areaplot (Filled Area)**

> ***reference:*** [<plt.fill_between> Document](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.fill_between.html)

> **plt.fill_between** (*x, y, color=.., alpha=..*)

  

### 4-1. 기본 areaplot 그리기


```python
y = np.random.randint(low=5, high=10, size=20)
y
```


    array([8, 8, 7, 6, 5, 8, 6, 9, 8, 8, 5, 5, 6, 6, 5, 5, 6, 8, 9, 5])

<br />

  


```python
x = np.arange(1,21)
y = np.random.randint(low=5, high=10, size=20)

# fill_between으로 색칠하기
plt.fill_between(x, y, color = "green", alpha = 0.6)

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_72_0.png)

<br />


### 4-2. 경계선을 굵게 그리고 area는 옅게 그리는 효과 적용


```python
plt.fill_between(x, y, color='green', alpha=0.3)
plt.plot(x, y, color='green', alpha=0.7)

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_75_0.png)

<br />


### 4-3. 여러 그래프를 겹쳐서 표현


```python
x = np.arange(0, 10, 0.05)
y_1 = np.cos(x) + 1
y_2 = np.sin(x) + 1
y_3 = y_1 * y_2 / np.pi

plt.fill_between(x, y_1, label='1+cos', color='green', alpha=0.1)
plt.fill_between(x, y_2, label='1+sin', color='blue', alpha=0.2)
plt.fill_between(x, y_3, label='sin*cos/pi', color='red', alpha=0.3)

plt.legend()

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_78_0.png)


많이 겹치는 부분이 어디인지 확인하고 싶을 때 많이 활용됨

 <br /> <br />

  

## **5. Histogram**

> ***reference:*** [<plt.hist> Document](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.hist.html)

> **plt.hist** (x, bins = ..)  

### 5-1. 기본 Histogram 그리기


```python
N = 100000
bins = 30

x = np.random.randn(N)

plt.hist(x, bins = bins)

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_87_0.png)

<br />

### 5-2. 다중 Histogram 그리기

> **fig, axs = plt.subplots** (*row, column, sharey = True, tight_layout = True*)  
> **axes[i].hist** ( *x, bins = ..*)
>
> * **sharey:** 다중 그래프가 같은 y축을 share
> * **tight_layout:** graph의 패딩을 자동으로 조절해주어 fit한 graph를 생성

<br />

```python
N = 100000
bins = 30

x = np.random.randn(N)

fig, axes = plt.subplots(1, 3, 
                        sharey = True,
                        tight_layout = True)

fig.set_size_inches(12, 5)

axes[0].hist(x, bins = bins)
axes[1].hist(x, bins = bins*2)
axes[2].hist(x, bins = bins*4)

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_91_0.png)

<br />


### 5-3. Y축에 Density 표기

* **pdf(확률 밀도 함수):** density = True
* **cdf(누적 확률 함수):** density = True, cumulatice = True


```python
N = 100000
bins = 30

x = np.random.randn(N)

fig, axes = plt.subplots(1, 2, tight_layout = True)

fig.set_size_inches(12, 4)

# density=True 값을 통하여 Y축에 density를 표기할 수 있다
axes[0].hist(x, bins = bins, density = True, cumulative = True)  #cdf: 누적확률함수
axes[1].hist(x, bins = bins, density = True)  # pdf: 확률밀도함수

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_95_0.png)

<br />

<br />


## **6. Pie Chart**

> ***reference:*** [<plt.pie> Document](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.pie.html)

> **plt.pie**( *x, explode=None, labels=None, colors=None, autopct=None, shadow=False, startangle=None,...*) 

**pie chart 옵션**

* explode: 파이에서 툭 튀어져 나온 비율
* autopct: 퍼센트 자동으로 표기
* shadow: 그림자 표시
* startangle: 파이를 그리기 시작할 각도

**리턴을 받는 인자**

* texts: label에 대한 텍스트 효과

* autotexts: 파이 위에 그려지는 텍스트 효과

  <br />


```python
labels = ['Samsung', 'Huawei', 'Apple', 'Xiaomi', 'Oppo', 'Etc']
sizes = [20.4, 15.8, 10.5, 9, 7.6, 36.7]
explode = (0.3, 0, 0, 0, 0, 0)

# text, autotext 인자를 활용하여 텍스트 스타일링을 적용한다
patches, texts, autotexts = plt.pie(sizes,
                                    explode = explode,
                                    labels = labels,
                                    autopct = "%1.1f%%",
                                    shadow = True,
                                    startangle=90)

plt.title('Smartphone Pie', fontsize=15)

# label 텍스트에 대한 스타일 적용
for t in texts:
    t.set_fontsize(12)
    t.set_color('gray')
    
# pie 위의 텍스트에 대한 스타일 적용
for t in autotexts:
    t.set_fontsize(18)
    t.set_color('white')
    
plt.show()
    
```


![png](/images/S-Python-Matplotlib2/output_103_0.png)

<br />

<br />


## **7. Box Plot**

<img src="/images/S-Python-Matplotlib2/R800x0" alt="box plot 해석" style="zoom:80%;" />

> ***reference:*** [<plt.boxplot> Document](https://matplotlib.org/3.2.1/api/_as_gen/matplotlib.pyplot.boxplot.html)

> **plt.boxplot** (*data, vert=True, flierprops = ..*)
>
> * **vert:** boxplot 축 바꾸기 (If True: 수직 boxplot; If not: 수평 boxplot)
> * **flierprops:** oulier marker 설정 (Symbol & Color)

  <br />

**샘플 데이터 생성**


```python
# Data Generation Process (DGP)
spread = np.random.rand(50) * 100
center = np.ones(25) * 50
flier_high = np.random.rand(10) * 100 + 100
flier_low = np.random.rand(10) * -100
data = np.concatenate((spread, center, flier_high, flier_low))
```

  <br />

### 7-1. 기본 박스플롯 생성


```python
plt.boxplot(data)
plt.tight_layout
plt.show()
```


![png](/images/S-Python-Matplotlib2/output_115_0.png)

<br />


### 7-2. 다중 박스플롯 생성

> * 다중 그래프 생성을 위해서는 data 자체가 **2차원으로 구성**되어 있어야 한다
> * row와 column으로 구성된 DataFrame에서 Column은 x축에 Row는 Y축에 구성되어 있음


```python
# DGP
spread1 = np.random.rand(50) * 100
center1 = np.ones(25) * 50
flier_high1 = np.random.rand(10) * 100 + 100
flier_low1 = np.random.rand(10) * -100
data1 = np.concatenate((spread1, center1, flier_high1, flier_low1))

spread2 = np.random.rand(50) * 100
center2 = np.ones(25) * 40
flier_high2 = np.random.rand(10) * 100 + 100
flier_low2 = np.random.rand(10) * -100
data2 = np.concatenate((spread2, center2, flier_high2, flier_low2))

data1.shape = (-1, 1)
data2.shape = (-1, 1)

data = [data1, data2, data2[::2, 0]]
```


```python
plt.boxplot(data)
plt.show()
```


![png](/images/S-Python-Matplotlib2/output_120_0.png)

<br />


### 7-3. Box Plot 축 바꾸기

* **vert = False** 옵션을 사용


```python
plt.boxplot(data, vert = False)
plt.title('Horizontal Box Plot', fontsize = 16)

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_124_0.png)

<br />


### 7-4. Outlier 마커 심볼과 컬러 변경

* **flierprops = ..** 옵션 사용


```python
outlier_marker = dict(markerfacecolor = 'r', marker = 'D')  # red diamond

plt.boxplot(data, flierprops = outlier_marker)
plt.title('Change Outlier Symbols', fontsize = 16)

plt.show()
```


![png](/images/S-Python-Matplotlib2/output_128_0.png)

<br />

<br />


## **8. 3D 그래프 그리기**

> ***reference:*** [mplot3d tutorial](https://matplotlib.org/mpl_toolkits/mplot3d/tutorial.html#contour-plots)

3D 로 그래프를 그리기 위해서는 ```mplot3d```를 추가로 import 해야 함


```python
from mpl_toolkits import mplot3d
```

  <br />

### 8-1. 밑그림 그리기 (canvas)


```python
fig = plt.figure()
ax = plt.axes(projection = '3d')
```


![png](/images/S-Python-Matplotlib2/output_137_0.png)

<br />

### 8-2. 3D plot 그리기

> *Axes* = plt.axes(projection = '3d')
>
> * _Axes_ **.plot** (*x, y, z, color=.., alpha=.., marker=..*)
> * _Axes_ **.plot3D** (*x, y, z, color=.., alpha=.., marker=..*)

  <br />


```python
# projection = 3d로 설정
ax = plt.axes(projection = '3d')

# x, y, z 데이터 생성
z = np.linspace(0, 15, 1000)
x = np.sin(z)
y = np.cos(z)

ax.plot(x, y, z, 'gray')
plt.show()
```


![png](/images/S-Python-Matplotlib2/output_142_0.png)

<br />



```python
# projection = 3d로 설정
ax = plt.axes(projection = '3d')

# x, y, z 데이터 생성
sample_size = 100
x = np.cumsum(np.random.normal(0, 1, sample_size)) # cumsum: 누적 합
y = np.cumsum(np.random.normal(0, 1, sample_size))
z = np.cumsum(np.random.normal(0, 1, sample_size))

ax.plot3D(x, y, z, alpha=0.6, marker='o')

plt.title('ax.plot')
plt.show()
```


![png](/images/S-Python-Matplotlib2/output_144_0.png)

<br />

### 8-3. 3d-scatter 그리기

> ***reference:*** [<Axes.scatter> Document](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.scatter.html)

> *Axes* = fig.add_subplot(111, projection='3d') <font color='blue'># Axe3D object</font>
>
> *Axes* **.scatter**( *x, y, z, s=None, c=None, marker=None, cmap=None, alpha=None, ..*)
>
> * **s:** marker size
> * **c:** marker color

<br />

```python
fig = plt.figure(figsize=(10, 5))
ax = fig.add_subplot(111, projection='3d') # Axe3D object

sample_size = 500

x = np.cumsum(np.random.normal(0, 5, sample_size))
y = np.cumsum(np.random.normal(0, 5, sample_size))
z = np.cumsum(np.random.normal(0, 5, sample_size))

ax.scatter(x, y, z, c=z, s=20, alpha=0.5, cmap='Greens')

plt.title('ax.scatter')
plt.show()
```


![png](/images/S-Python-Matplotlib2/output_148_0.png)


컬러가 찐한 부분에 데이터가 더 많이 몰려있음

  <br />

### 8-4. contour3D 그리기 (등고선)

> *Axes* = plt.axes(projection='3d')  
> *Axes* **.contour3D** (*x, y, z* )


```python
x = np.linspace(-6, 6, 30)
y = np.linspace(-6, 6, 30)
x, y = np.meshgrid(x, y)

z = np.sin(np.sqrt(x**2 + y**2))

fig = plt.figure(figsize=(12, 6))
ax = plt.axes(projection='3d')

ax.contour3D(x, y, z, 20, cmap='Reds')

plt.title("ax.contour3D")
plt.show()
```


![png](/images/S-Python-Matplotlib2/output_153_0.png)

<br />

<br />


## **9. imshow**

이미지 데이터가 numpy array에서는 숫자형식으로 표현됨  
명령어```imshow```는 이 컬러숫자들을 이미지로 변환하여 보여줌

  <br />

예제: ```sklearn.datasets```안의 ```load_digits```데이터

* ```load_digits``` 는 0~16 값을 가지는 array로 이루어져 있다

* 1개의 array는 8 X 8 배열 안에 표현되어 있다

* 숫자는 0~9까지 이루어져있다

  <br />


```python
from sklearn.datasets import load_digits

digits = load_digits()
X = digits.images[:10]  # 앞에 10개 image를 뽑아서 저장함
X[0]  # 첫번째 image의 컬러숫자를 살펴보자
```


    array([[ 0.,  0.,  5., 13.,  9.,  1.,  0.,  0.],
           [ 0.,  0., 13., 15., 10., 15.,  5.,  0.],
           [ 0.,  3., 15.,  2.,  0., 11.,  8.,  0.],
           [ 0.,  4., 12.,  0.,  0.,  8.,  8.,  0.],
           [ 0.,  5.,  8.,  0.,  0.,  9.,  8.,  0.],
           [ 0.,  4., 11.,  0.,  1., 12.,  7.,  0.],
           [ 0.,  2., 14.,  5., 10., 12.,  0.,  0.],
           [ 0.,  0.,  6., 13., 10.,  0.,  0.,  0.]])

<br />

지금 한 위치에 숫자 하나밖에 없어서 컬러는 흑백으로 나옴.  
숫자가 클수록 black에 가깝고, 작을수록 white에 가까움

  <br />


```python
fig, axes = plt.subplots(nrows=2, ncols=5, sharex=True, figsize=(12, 6), sharey=True)

for i in range(10):
    axes[i//5][i%5].imshow(X[i], cmap='Blues')
    axes[i//5][i%5].set_title(str(i), fontsize=20)
    
plt.tight_layout()
plt.show()
```


![png](/images/S-Python-Matplotlib2/output_164_0.png)

<br />

<br />
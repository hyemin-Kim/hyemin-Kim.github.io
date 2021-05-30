---
title: Python >> Seaborn - (1) Seaborn을 활용한 다양한 그래프 그리기
tags:
  - Python
  - Seaborn
  - 시각화
categories: 
  - [【STUDY - Python】, Python - 4. Seaborn]
  - [【STUDY - Python】, Python - 시각화]
cover: 'https://s1.ax1x.com/2020/07/03/NjPQXV.png'
description: >-
  matplotlib 차트들을 seaborn에서 구현하기 (scatterplot, barplot, lineplot, histogram,
  boxplot)
typora-root-url: ..
abbrlink: 57429
date: 2020-07-03 19:14:58
---

# Seaborn을 활용한 다양한 그래프 그리기

  @[toc]

<br />

> ***reference:***
>
> * [pyplot 공식 도튜먼트 살펴보기](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot)
> * [seaborn 공식 도큐먼트 살펴보기](https://seaborn.pydata.org/)

<br />

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from IPython.display import Image

# seaborn
import seaborn as sns
```


```python
plt.rcParams["figure.figsize"] = (9, 6)  # figure size 설정
plt.rcParams["font.size"] = 14  # fontsize 설정
```

  <br />

## **0. Seaborn 개요**

seaborn은 matplotlib을 더 사용하게 쉽게 해주는 라이브러리다.  
matplotlib으로 대부분의 시각화는 가능하지만, 다음과 같은 이유로 많은 사람들이 ```seaborn```을 선호한다.

> **비교:** [matplotlib을 활용한 다양한 그래프 그리기](https://hyemin-kim.github.io/2020/06/28/S-Python-Matplotlib2/)

 <br /> 

### 0-1. seaborn 에서만 제공되는 통계 기반 plot


```python
tips = sns.load_dataset("tips")
```

  <br />

**(1) violinplot**


```python
sns.violinplot(x="day", y="total_bill", data=tips)
plt.title('violin plot')
plt.show()
```


![png](/images/S-Python-Seaborn1/output_14_0.png)

<br />


**(2) countplot** 


```python
sns.countplot(tips['day'])
plt.title('countplot')
plt.show()
```


![png](/images/S-Python-Seaborn1/output_17_0.png)

<br />


**(3) relplot**


```python
sns.relplot(x='tip', y='total_bill', data=tips)
plt.title('relplot')
plt.show()
```


![png](/images/S-Python-Seaborn1/output_20_0.png)

<br />


**(4) lmplot**


```python
sns.lmplot(x='tip', y='total_bill', data=tips)
plt.title('lmplot')
plt.show()
```


![png](/images/S-Python-Seaborn1/output_23_0.png)

<br />


**(5) heatmap**


```python
plt.title('heatmap')
sns.heatmap(tips.corr(), annot=True, linewidths=1)
plt.show()
```


![png](/images/S-Python-Seaborn1/output_26_0.png)

<br />


### 0-2. 아름다운 스타일링

**(1) default color의 예쁜 조합**

seaborn의 최대 장점 중의 하나가 아름다운 컬러팔레트다.  
스타일링에 크게 신경 쓰지 않아도 default 컬러가 예쁘게 조합해준다.

<br />

**matplotlib VS seaborn** 


```python
plt.bar(tips['day'], tips['total_bill'])
plt.show()
```


![png](/images/S-Python-Seaborn1/output_32_0.png)



```python
sns.barplot(x="day", y="total_bill", data=tips, palette="colorblind")
plt.show()
```


![png](/images/S-Python-Seaborn1/output_33_0.png)

<br />


**(2) 그래프 배경 설정**

그래프의 배경 (grid 스타일)을 설정할 수 있음.

> **sns.set_style('...')**  
>
> * whitegrid: white background + grid
> * darkgrid: dark background + grid
> * white: white background (without grid)
> * dark: dark background (without grid)

<br />

```python
sns.set_style('darkgrid')
sns.barplot(x="day", y="total_bill", data=tips, palette="colorblind")
plt.show()
```


![png](/images/S-Python-Seaborn1/output_38_0.png)

<br />

```python
sns.set_style('white')
sns.barplot(x="day", y="total_bill", data=tips, palette="colorblind")
plt.show()
```


![png](/images/S-Python-Seaborn1/output_39_0.png)

<br />


### 0-3. 컬러 팔레트

자세한 컬러팔레트는 [공식 도큐먼트](https://chrisalbon.com/python/data_visualization/seaborn_color_palettes/)를 참고


```python
sns.palplot(sns.light_palette((210, 90, 60), input="husl"))
sns.palplot(sns.dark_palette("muted purple", input="xkcd"))
sns.palplot(sns.color_palette("BrBG", 10))
sns.palplot(sns.color_palette("BrBG_r", 10))
sns.palplot(sns.color_palette("coolwarm", 10))
sns.palplot(sns.diverging_palette(255, 133, l=60, n=10, center="dark"))
```


![png](/images/S-Python-Seaborn1/output_43_0.png)



![png](/images/S-Python-Seaborn1/output_43_1.png)



![png](/images/S-Python-Seaborn1/output_43_2.png)



![png](/images/S-Python-Seaborn1/output_43_3.png)



![png](/images/S-Python-Seaborn1/output_43_4.png)



![png](/images/S-Python-Seaborn1/output_43_5.png)

<br />

```python
sns.barplot(x="tip", y="total_bill", data=tips, palette='coolwarm')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1ba5bf62888>




![png](/images/S-Python-Seaborn1/output_44_1.png)

<br />

```python
sns.barplot(x="tip", y="total_bill", data=tips, palette='Reds')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1ba59e40988>




![png](/images/S-Python-Seaborn1/output_45_1.png)

<br />


### 0-4. pandas 데이터프레임과 높은 호환성


```python
tips
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>16.99</td>
      <td>1.01</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10.34</td>
      <td>1.66</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21.01</td>
      <td>3.50</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>23.68</td>
      <td>3.31</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24.59</td>
      <td>3.61</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>239</th>
      <td>29.03</td>
      <td>5.92</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>240</th>
      <td>27.18</td>
      <td>2.00</td>
      <td>Female</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>241</th>
      <td>22.67</td>
      <td>2.00</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>242</th>
      <td>17.82</td>
      <td>1.75</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>243</th>
      <td>18.78</td>
      <td>3.00</td>
      <td>Female</td>
      <td>No</td>
      <td>Thur</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>244 rows × 7 columns</p>

</div>



  <br />


```python
sns.catplot(x="sex", y="total_bill",
            data=tips, 
            kind="bar")
plt.show()
```


![png](/images/S-Python-Seaborn1/output_50_0.png)

<br />


* ```hue```옵션: bar를 새로운 기준으로 분할


```python
sns.catplot(x="sex", y="total_bill",
            hue="smoker", 
            data=tips, 
            kind="bar")
plt.show()
```


![png](/images/S-Python-Seaborn1/output_53_0.png)

<br />


* ```col``` / ```row``` 옵션: 그래프 자체를 새로운 기준으로 분할


```python
sns.catplot(x="sex", y="total_bill",
            hue="smoker", 
            col="time",
            data=tips, 
            kind="bar")
plt.show()
```


![png](/images/S-Python-Seaborn1/output_56_0.png)

<br />


* xtick, ytick, xlabel, ylabel을 알아서 생성해 줌

* legend까지 자동으로 생성해 줌

* 뿐만 아니라, 신뢰 구간도 알아서 계산하여 생성함

  <br />

## **1. Scatterplot**

> ***reference:*** [<sns.scatterplot> Document](https://seaborn.pydata.org/generated/seaborn.scatterplot.html)

> **sns.scatterplot** ( *x, y, size=None, sizes=None, hue=None, palette=None, color='auto', alpha='auto'...* )
>
> * ```sizes``` 옵션: size의 선택범위를 설정. (사아즈의 min, max를 설정)
> * ```hue``` 옵션: 컬러의 구별 기준이 되는 grouping variable 설정
> * ```color``` 옵션: cmap에 컬러를 지정하면, 컬러 값을 모두 같게 가겨갈 수 있음
> * ```alpha``` 옵션: 투명도 (0~1)

<br />

```python
sns.set_style('darkgrid')
```

  <br />

### 1-1. x, y, color, area 설정하기


```python
# 데이터 생성
x = np.random.rand(50)
y = np.random.rand(50)
colors = np.arange(50)
area = x * y * 1000
```

  <br />

**(1) matplotlib**


```python
plt.scatter(x, y, s=area, c=colors)
plt.show()
```


![png](/images/S-Python-Seaborn1/output_69_0.png)

<br />

**(2) seaborn**


```python
sns.scatterplot(x, y, size=area, sizes=(area.min(), area.max()), hue=area, palette='coolwarm')
plt.show()
```


![png](/images/S-Python-Seaborn1/output_72_0.png)

<br />


**[Tip]** Palette 이름이 생각안나면: palette 값을 임의로 주고 실행하여 오류 경고창에 정확한 palette 이름을 보여줌


```python
sns.scatterplot(x, y, size=area, sizes=(area.min(), area.max()), hue=area, palette='coolwarm111')
plt.show()
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    D:\Anaconda\lib\site-packages\seaborn\relational.py in numeric_to_palette(self, data, order, palette, norm)
        248             try:
    --> 249                 cmap = mpl.cm.get_cmap(palette)
        250             except (ValueError, TypeError):


    D:\Anaconda\lib\site-packages\matplotlib\cm.py in get_cmap(name, lut)
        182             "Colormap %s is not recognized. Possible values are: %s"
    --> 183             % (name, ', '.join(sorted(cmap_d))))
        184 


    ValueError: Colormap coolwarm111 is not recognized. Possible values are: Accent, Accent_r, Blues, Blues_r, BrBG, BrBG_r, BuGn, BuGn_r, BuPu, BuPu_r, CMRmap, CMRmap_r, Dark2, Dark2_r, GnBu, GnBu_r, Greens, Greens_r, Greys, Greys_r, OrRd, OrRd_r, Oranges, Oranges_r, PRGn, PRGn_r, Paired, Paired_r, Pastel1, Pastel1_r, Pastel2, Pastel2_r, PiYG, PiYG_r, PuBu, PuBuGn, PuBuGn_r, PuBu_r, PuOr, PuOr_r, PuRd, PuRd_r, Purples, Purples_r, RdBu, RdBu_r, RdGy, RdGy_r, RdPu, RdPu_r, RdYlBu, RdYlBu_r, RdYlGn, RdYlGn_r, Reds, Reds_r, Set1, Set1_r, Set2, Set2_r, Set3, Set3_r, Spectral, Spectral_r, Wistia, Wistia_r, YlGn, YlGnBu, YlGnBu_r, YlGn_r, YlOrBr, YlOrBr_r, YlOrRd, YlOrRd_r, afmhot, afmhot_r, autumn, autumn_r, binary, binary_r, bone, bone_r, brg, brg_r, bwr, bwr_r, cividis, cividis_r, cool, cool_r, coolwarm, coolwarm_r, copper, copper_r, cubehelix, cubehelix_r, flag, flag_r, gist_earth, gist_earth_r, gist_gray, gist_gray_r, gist_heat, gist_heat_r, gist_ncar, gist_ncar_r, gist_rainbow, gist_rainbow_r, gist_stern, gist_stern_r, gist_yarg, gist_yarg_r, gnuplot, gnuplot2, gnuplot2_r, gnuplot_r, gray, gray_r, hot, hot_r, hsv, hsv_r, icefire, icefire_r, inferno, inferno_r, jet, jet_r, magma, magma_r, mako, mako_r, nipy_spectral, nipy_spectral_r, ocean, ocean_r, pink, pink_r, plasma, plasma_r, prism, prism_r, rainbow, rainbow_r, rocket, rocket_r, seismic, seismic_r, spring, spring_r, summer, summer_r, tab10, tab10_r, tab20, tab20_r, tab20b, tab20b_r, tab20c, tab20c_r, terrain, terrain_r, twilight, twilight_r, twilight_shifted, twilight_shifted_r, viridis, viridis_r, vlag, vlag_r, winter, winter_r


  <br />

### 1-2. cmap과 alpha

**(1) matplotlib**


```python
plt.figure(figsize=(12, 6))

plt.subplot(131)
plt.scatter(x, y, s=area, c='blue', alpha=0.1)
plt.title('alpha=0.1')
plt.subplot(132)
plt.title('alpha=0.5')
plt.scatter(x, y, s=area, c='red', alpha=0.5)
plt.subplot(133)
plt.title('alpha=1.0')
plt.scatter(x, y, s=area, c='green', alpha=1.0)

plt.show()
```


![png](/images/S-Python-Seaborn1/output_79_0.png)

<br />


**(2) seaborn**


```python
plt.figure(figsize=(12, 6))

plt.subplot(131)
sns.scatterplot(x, y, size=area, sizes=(area.min(), area.max()), color='blue', alpha=0.1)
plt.title('alpha=0.1')

plt.subplot(132)
plt.title('alpha=0.5')
sns.scatterplot(x, y, size=area, sizes=(area.min(), area.max()), color='red', alpha=0.5)

plt.subplot(133)
plt.title('alpha=1.0')
sns.scatterplot(x, y, size=area, sizes=(area.min(), area.max()), color='green', alpha=0.9)

plt.show()
```


![png](/images/S-Python-Seaborn1/output_82_0.png)

<br />

<br />


## **2. Barplot, Barhplot**

> ***reference:*** [<sns.barplot> Document](https://seaborn.pydata.org/generated/seaborn.barplot.html)

> **sns.boxplot** ( *x, y, hue=None, data=None, alpha='auto', palette=None / color=None* )

<br /> 

### 2-1. 기본 Barplot 그리기

**(1) matplotlib**


```python
x = ['Math', 'Programming', 'Data Science', 'Art', 'English', 'Physics']
y = [90, 60, 80, 50, 70, 40]

plt.figure(figsize = (7,4))

plt.bar(x, y, alpha = 0.7, color = 'red')

plt.title('Subjects')

plt.xticks(rotation=20)
plt.ylabel('Grades')

plt.show()
```


![png](/images/S-Python-Seaborn1/output_91_0.png)

<br />


**(2) seaborn**


```python
x = ['Math', 'Programming', 'Data Science', 'Art', 'English', 'Physics']
y = [90, 60, 80, 50, 70, 40]

plt.figure(figsize = (7,4))

sns.barplot(x, y, alpha=0.8, palette='YlGnBu')

plt.title('Subjects')

plt.xticks(rotation=20)
plt.ylabel('Grades')

plt.show()
```


![png](/images/S-Python-Seaborn1/output_94_0.png)

<br />


### 2-2. 기본 Barhplot 그리기

**(1) matplotlib**

> * **plt.barh** 함수 사용 
> * bar 함수에서 **xticks / ylabel 로 설정**했던 부분이 barh 함수에서 **yticks / xlabel 로 변경함** 


```python
x = ['Math', 'Programming', 'Data Science', 'Art', 'English', 'Physics']
y = [90, 60, 80, 50, 70, 40]

plt.figure(figsize = (7,5))

plt.barh(x, y, alpha = 0.7, color = 'red')

plt.title('Subjects')

plt.yticks(x)
plt.xlabel('Grades')

plt.show()
```

![png](/images/S-Python-Seaborn1/output_99_0.png)

<br />

**(2) seaborn**

> * sns.barplot 함수를 그대로 사용
> * barplot함수 안에 x와 y의 위치를 교환
>   xticks설정이 변경 불필요;  
>    하지만 ylabel설정은 xlable로 변경 필요

<br />

```python
x = ['Math', 'Programming', 'Data Science', 'Art', 'English', 'Physics']
y = [90, 60, 80, 50, 70, 40]

plt.figure(figsize = (7,5))

sns.barplot(y, x, alpha=0.9, palette="YlOrRd")

plt.xlabel('Grades')
plt.title('Subjects')

plt.show()
```


![png](/images/S-Python-Seaborn1/output_102_0.png)

<br />


### 2-3. Barplot에서 비교 그래프 그리기

**(1) matplotlib**


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


![png](/images/S-Python-Seaborn1/output_106_0.png)

<br />

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


![png](/images/S-Python-Seaborn1/output_107_0.png)

<br />


**(2) seaborn**

Seaborn에서는 위의 ```matplotlib```과 조금 다른 방식을 취한다.  
seaborn에서 ```hue```옵션으로 매우 쉽게 비교 **barplot**을 그릴 수 있음.  

> **sns.barplot** ( *x, y, hue=.., data=.., palette=..* )

<br />

**실전 tip.**

* 그래프를 임의로 그려야 하는 경우 -> ```matplotlib```

* DataFrame을 가지고 그리는 경우 -> ```seaborn```

  <br />


```python
titanic = sns.load_dataset('titanic')
titanic.head()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<div style='overflow:auto'>
<table style='width = 100%;'>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>class</th>
      <th>who</th>
      <th>adult_male</th>
      <th>deck</th>
      <th>embark_town</th>
      <th>alive</th>
      <th>alone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Cherbourg</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>Third</td>
      <td>woman</td>
      <td>False</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>

</div>



<br />


```python
sns.barplot(x='sex', y='survived', hue='pclass', data=titanic, palette='muted')
plt.show()
```


![png](/images/S-Python-Seaborn1/output_115_0.png)

<br />

<br />


## **3. Line Plot**

> ***reference:*** [<sns.lineplot> Document](https://seaborn.pydata.org/generated/seaborn.lineplot.html)

<br />

> **sns.lineplot** ( *x, y, label=.., color=None, alpha='auto', marker=None, linestyle=None* )
>
> * 기본 옵션은 matplotlib의 ```plt.plot```과 비슷
> * 함수만 ```plt.plot```에서 ```sns.lineplot```로 바꾸면 됨
> * plt.legend() 명령어 따로 쓸 필요없음
> * 배경이 whitegrid / darkgrid 로 설정되어 있을 시 plt.grid() 명령어 불필요

<br />  

### 3-1. 기본 lineplot 그리기

**(1) matplotlib**


```python
x = np.arange(0, 10, 0.1)
y = 1 + np.sin(x)

plt.plot(x, y)

plt.xlabel('x value')
plt.ylabel('y value')
plt.title('sin graph', fontsize=16)

plt.show()
```


![png](/images/S-Python-Seaborn1/output_124_0.png)

<br />


**(2) seaborn**


```python
sns.lineplot(x, y)  # 함수만 변경하면 됨 (plt.plot -> sns.lineplot)

plt.xlabel('x value')
plt.ylabel('y value')
plt.title('sin graph', fontsize=16)

plt.show()
```


![png](/images/S-Python-Seaborn1/output_127_0.png)

<br />


### 3-2. 2개 이상의 그래프 그리기


```python
x = np.arange(0, 10, 0.1)
y_1 = 1 + np.sin(x)
y_2 = 1 + np.cos(x)

sns.lineplot(x, y_1,label='1+sin', color='blue', alpha = 0.3)  # label 설정값을 legend에 나타날 수 있음
sns.lineplot(x, y_2, label='1+cos', color='red', alpha = 0.7)

plt.xlabel("x value")
plt.ylabel("y value")

plt.title("sin and cos graph", fontsize = 18)

plt.show()
```


![png](/images/S-Python-Seaborn1/output_130_0.png)

<br />


### 3-3. 마커 스타일링

* marker: 마커 옵션


```python
x = np.arange(0, 10, 0.1)
y_1 = 1 + np.sin(x)
y_2 = 1+ np.cos(x)

sns.lineplot(x, y_1, label='1+sin', color='blue', alpha=0.3, marker='o')
sns.lineplot(x, y_2, label='1+cos', color='red', alpha=0.7, marker='+')

plt.xlabel('x value')
plt.ylabel('y value')

plt.title('sin and cos graph', fontsize = 18)

plt.show()
```


![png](/images/S-Python-Seaborn1/output_134_0.png)

<br />


### 3-4. 라인 스타일 변경하기

* linestyle: 라인 스타일 변경하기


```python
x = np.arange(0, 10, 0.1)
y_1 = 1 + np.sin(x)
y_2 = 1+ np.cos(x)

sns.lineplot(x, y_1, label='1+sin', color='blue', linestyle=':')
sns.lineplot(x, y_2, label='1+cos', color='red', linestyle='-.')

plt.xlabel('x value')
plt.ylabel('y value')

plt.title('sin and cos graph', fontsize = 18)

plt.show()
```


![png](/images/S-Python-Seaborn1/output_138_0.png)

<br />

<br />


## **4. Areaplot (Filled Area)**

> Seaborn에서는 **areaplot을 지원하지 않음**  
> matplotlib을 활용하여 구현해야 함

<br />  

## **5.Histogram**

> ***reference:*** [<sns.distplot> Document](https://seaborn.pydata.org/generated/seaborn.distplot.html)

<br />

> **sns.distplot** ( *x, bins=None, hist=True, kde=True, vertical=False* )
>
> * **bins:** hist bins 갯수 설정
> * **hist:** Whether to plot a (normed) histogram
> * **kde:** Whether to plot a gaussian kernel density estimate
> * **vertical:** If True, observed values are on y-axis

  <br />

### 5-1. 기본 Histogram 그리기

**(1) matplotlib**


```python
N = 100000
bins = 30

x = np.random.randn(N)

plt.hist(x, bins=bins)

plt.show()
```


![png](/images/S-Python-Seaborn1/output_150_0.png)

<br />


**(2) seaborn**

**Histogram + Density Function** <font color='blue'>(*default*)</font>


```python
N = 100000
bins = 30

x = np.random.randn(N)

sns.distplot(x, bins=bins)
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1ba5cc800c8>




![png](/images/S-Python-Seaborn1/output_154_1.png)

<br />


**Histogram Only**


```python
sns.distplot(x, bins=bins, hist=True, kde=False, color='g')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1ba5cd09788>




![png](/images/S-Python-Seaborn1/output_157_1.png)

<br />

**Density Function Only**


```python
sns.distplot(x, bins=bins, hist=False, kde=True, color='g')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1ba5c7cc208>




![png](/images/S-Python-Seaborn1/output_160_1.png)

<br />


**수평 그래프**


```python
sns.distplot(x, bins=bins, vertical=True, color='r')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1ba5c250108>




![png](/images/S-Python-Seaborn1/output_163_1.png)

<br />


### 5-2. 다중 Histogram 그리기

matplotlib 에서의 방법을 사용


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


![png](/images/S-Python-Seaborn1/output_167_0.png)

<br />

<br />


## **6. Pie Chart**

> Seaborn에서는 **pie plot을 지원하지 않음**  
> matplotlib을 활용하여 구현해야 함

  <br />

## **7. Box Plot**

> ***reference:*** [<sns.boxplot> Document](https://seaborn.pydata.org/generated/seaborn.boxplot.html)

<br />

> **sns.baxplot** ( *x=None, y=None, hue=None, data=None, orient=None, width=0.8* )
>
> * **hue:** 비교 그래프를 그릴 때 나눔 기준이 되는 Variable 설정
> * **orient:** "v" / "h".  Orientation of the plot (vertical or horizontal)
> * **width:** box의 넓이

<br />  

### 7-1. 기본 박스플롯 생성

**샘플 데이터 생성**


```python
# DGP
spread = np.random.rand(50) * 100
center = np.ones(25) * 50
flier_high = np.random.rand(10) * 100 + 100
flier_low = np.random.rand(10) * -100
data = np.concatenate((spread, center, flier_high, flier_low))
```

  <br />

**(1) matplotlib**


```python
plt.boxplot(data)
plt.show()
```


![png](/images/S-Python-Seaborn1/output_182_0.png)

<br />


**(2) seaborn**


```python
sns.boxplot(data, orient='v', width=0.2)
plt.show()
```


![png](/images/S-Python-Seaborn1/output_185_0.png)

<br />


### 7-2. 다중 박스플롯 생성

seaborn에서는  ```hue```옵션으로 매우 쉽게 **비교 boxplot**을 그릴 수 있으며 주로 DataFrame을 가지고 그릴 때 활용한다.  

barplot과 마찬가지로, 용도에 따라 적절한 library를 사용한다

<br />

**실전 Tip.**

* 그래프를 임의로 그려야 하는 경우 -> ```matplotlit```

* DataFrame을 가지고 그리는 경우 -> ```seaborn``` 

  <br />

**(1) matplotlib**


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

  <br />


```python
plt.boxplot(data)
plt.show()
```


![png](/images/S-Python-Seaborn1/output_194_0.png)

<br />


**(2) seaborn**


```python
titanic = sns.load_dataset('titanic')
titanic.head()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<div style='overflow:auto'>
<table style='width = 100%;'>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>class</th>
      <th>who</th>
      <th>adult_male</th>
      <th>deck</th>
      <th>embark_town</th>
      <th>alive</th>
      <th>alone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Cherbourg</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>Third</td>
      <td>woman</td>
      <td>False</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>

</div>



 <br /> 


```python
sns.boxplot(x='pclass', y='age', hue='survived', data=titanic)
plt.show()
```


![png](/images/S-Python-Seaborn1/output_199_0.png)

<br />


### 7-3. Box Plot 축 바꾸기

**(1) 단일 boxplot**

* orient옵션: orient = "h"로 설정


```python
# DGP
spread = np.random.rand(50) * 100
center = np.ones(25) * 50
flier_high = np.random.rand(10) * 100 + 100
flier_low = np.random.rand(10) * -100
data = np.concatenate((spread, center, flier_high, flier_low))
```


```python
sns.boxplot(data, orient='h', width=0.3)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ba5e866188>




![png](/images/S-Python-Seaborn1/output_205_1.png)

<br />


**(2) 다중 boxplot**

1. x, y 변수 교환
2. orient = "h"


```python
sns.boxplot(y='pclass', x='age', hue='survived', data=titanic, orient='h')
plt.show()
```


![png](/images/S-Python-Seaborn1/output_209_0.png)

<br />


### 7-4. Outlier 마커 심볼과 컬러 변경

* **flierprops = ...** 옵션 사용  <font color='blue'>(matplotlib과 동일)</font>


```python
outlier_marker = dict(markerfacecolor='r', marker='D')

plt.title('Changed Outlier Symbols', fontsize=15)
sns.boxplot(data, orient='v', width=0.2, flierprops=outlier_marker)

plt.show()
```


![png](/images/S-Python-Seaborn1/output_213_0.png)

<br />

<br />
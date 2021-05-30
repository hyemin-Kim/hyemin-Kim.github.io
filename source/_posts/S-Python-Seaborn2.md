---
title: Python >> Seaborn - (2) 통계 기반의 시각화
tags:
  - Python
  - Seaborn
  - 시각화
categories: 
  - [【STUDY - Python】, Python - 4. Seaborn]
  - [【STUDY - Python】, Python - 시각화]
cover: 'https://s1.ax1x.com/2020/07/03/NjPQXV.png'
description: 'countplot, distplot, heatmap, pairplot, violinplot, lmplot, relplot, jointplot'
typora-root-url: ..
abbrlink: 49809
date: 2020-07-03 19:18:20
---

# 통계 기반의 시각화

@[toc]

<br />


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
plt.rcParams["figure.figsize"] = (9, 6)  # figure size 설정
plt.rcParams["font.size"] = 14  # fontsize 설정
```

 <br /> 

## **0. 통계 기반의 시각화를 제공해주는 Seaborn**

> ***reference:*** [Seaborn 공식 도큐먼트](https://seaborn.pydata.org/api.html)

seaborn 라이브러리가  매력적인 이유는 바로 **통계 차트**다.  

이번 실습에서는 seaborn의 다양한 통계 차트 중 대표적인 차트 몇 개를 뽑아서 다뤄볼 예정이다.

그럼 먼저 실습에 사용되는 Dataset을 한번 살펴볼게요.

 <br /> 

**Dataset --- "Titanic"**


```python
titanic = sns.load_dataset('titanic')
titanic
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
<table>
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
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>0</td>
      <td>2</td>
      <td>male</td>
      <td>27.0</td>
      <td>0</td>
      <td>0</td>
      <td>13.0000</td>
      <td>S</td>
      <td>Second</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>True</td>
    </tr>
    <tr>
      <th>887</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>19.0</td>
      <td>0</td>
      <td>0</td>
      <td>30.0000</td>
      <td>S</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>B</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>888</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>NaN</td>
      <td>1</td>
      <td>2</td>
      <td>23.4500</td>
      <td>S</td>
      <td>Third</td>
      <td>woman</td>
      <td>False</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>False</td>
    </tr>
    <tr>
      <th>889</th>
      <td>1</td>
      <td>1</td>
      <td>male</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>30.0000</td>
      <td>C</td>
      <td>First</td>
      <td>man</td>
      <td>True</td>
      <td>C</td>
      <td>Cherbourg</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>890</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>32.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.7500</td>
      <td>Q</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Queenstown</td>
      <td>no</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>
<p>891 rows × 15 columns</p>

</div>

<br />

  

* survived: 생존여부

* pclass: 좌석등급 (숫자)

* sex: 성별

* age: 나이

* sibsp: 형제자매 + 배우자 숫자

* parch: 부모 + 자식 숫자

* fare: 요금

* embarked: 탑승 항구

* class: 좌석등급 (영문)

* who: 사람 구분

* deck: 데크

* embark_town: 탑승 항구 (영문)

* alive: 생존여부 (영문)

* alone: 혼자인지 여부

  <br />

**Dataset --- "tips"**


```python
tips = sns.load_dataset('tips')
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

<table  >
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

  

* total_bill: 총 합계 요금표

* tip: 팁

* sex: 성별

* smoker: 흡연자 여부

* day: 요일

* time: 식사 시간

* size: 식사 인원

  <br />


```python
# 배경 설정
sns.set(style='darkgrid')
```

<br />  

## **1. countplot**

항목별 갯수를 세어주는 ```countplot```  

* 해당 column을 구성하고 있는 value들을 자동으로 구분하여 보여준다

> ***reference:*** [<sns.countplot> Document](https://seaborn.pydata.org/generated/seaborn.countplot.html)

> **sns.countplot** ( *x=None, y=None, hue=None, data=None, color=None, palette=None* )

 <br /> 

### 1-1. 세로로 그리기


```python
sns.countplot(x='class', hue='who', data=titanic)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_26_0.png)

<br />


### 1-2. 가로로 그리기


```python
sns.countplot(y='class', hue='who', data=titanic)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_29_0.png)

<br />


### 1-3. 색상 팔레트 설정


```python
sns.countplot(x='class', hue='who', palette='copper', data= titanic)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_32_0.png)

<br />

<br />


## **2. distplot**

matplotlib의 ```hist```그래프와 ```kdeplot```을 통합한 그래프다.  
**분포**와 **밀도**를 확인할 수 있음

<br />

> ***reference:*** [<sns.distplot> Document](https://seaborn.pydata.org/generated/seaborn.distplot.html?highlight=distplot#seaborn.distplot)

> **sns.displot** ( *a, hist=True, kde=True, rug=False, vertical=False, color=None* )
>
> * hist: histogram
> * kde: kernel density estimate
> * rug: rugplot
> * vertical: If True, observed values are on y-axis

  <br />


```python
# 샘플 데이터 생성
x = np.random.randn(100)
x
```


    array([-3.39765920e-01, -1.48664049e+00, -5.57926444e-01,  3.25206560e-01,
           -7.46665762e-01, -3.10926812e-01, -2.14536012e+00,  1.25905620e+00,
           -2.07806423e-01,  5.56377038e-01, -2.20574498e+00, -1.15138577e-01,
           -3.32417471e-01,  1.13927613e-01, -7.29559442e-01, -1.31243715e+00,
           -8.27477111e-01, -1.24455099e+00, -5.44035731e-02, -1.85399773e+00,
           -1.62571613e+00,  3.89312791e-01,  1.26815698e+00, -7.43355761e-01,
           -1.34113997e+00,  2.67291801e-02, -4.74142344e-01, -1.07662894e+00,
           -2.35607451e+00,  1.90337236e-01, -1.18577255e+00, -1.23238300e+00,
            9.39298755e-01, -2.69078751e-01, -3.50418097e-01,  1.92109121e+00,
           -1.46520490e-01,  3.90810577e-01, -6.60511307e-01, -1.46288431e+00,
            1.26314685e+00,  2.38384651e-01,  8.03730080e-01,  2.83340226e-01,
           -1.24219159e+00, -1.50458389e+00, -1.60213592e-01,  3.97086657e-01,
            1.27321390e-01, -1.13722876e+00, -1.48448425e+00,  1.36136226e+00,
           -2.34669327e-01, -1.32679409e+00,  1.59032718e+00,  7.53779845e-01,
           -7.48815568e-01,  7.34822673e-03,  5.57358372e-01,  1.78429993e+00,
           -1.50510591e+00, -3.87983571e-01, -7.57372493e-01,  6.25354827e-01,
            1.44857563e-01,  7.78608476e-01, -6.61441801e-02, -1.24836018e+00,
            1.77522984e+00,  1.60497019e-01, -1.18893624e+00,  1.93951152e+00,
           -9.34504796e-01,  1.82000588e+00, -1.91594654e+00, -1.13118210e+00,
           -4.13371342e-01, -5.07021131e-01,  1.57792370e+00, -2.52509848e+00,
            1.86695906e-01, -1.18412859e+00,  1.49572473e-01, -3.53669860e-01,
            1.38877682e+00,  2.53212949e-02,  7.79387552e-01, -7.41508306e-01,
            4.10007279e-01,  1.96517288e-02, -5.69215198e-01,  1.45113980e+00,
           -8.80722624e-01,  1.35468793e+00, -1.67677998e-03, -1.14952039e+00,
            8.90718244e-01, -4.10411520e-01,  6.17620908e-01,  2.96993057e-01])

<br />

  

### 2-1. 기본 displot


```python
sns.distplot(x)  # x: numpy array
plt.show()
```


![png](/images/S-Python-Seaborn2/output_43_0.png)

<br />


### 2-2. 데이터가 Series일 경우


```python
x = pd.Series(x, name='x variable')
x
```


    0    -0.339766
    1    -1.486640
    2    -0.557926
    3     0.325207
    4    -0.746666
            ...   
    95   -1.149520
    96    0.890718
    97   -0.410412
    98    0.617621
    99    0.296993
    Name: x variable, Length: 100, dtype: float64

<br />


```python
sns.distplot(x)  # x: Series
plt.show()
```


![png](/images/S-Python-Seaborn2/output_47_0.png)


x가 Seires일 때는:  그래프에서 x label이 자동으로 Series 이름(column name) 으로 나타남

<br />  

### 2-3. rugplot

데이터 위치를 x축 위에 **작은 선분(rug)으로 나타내어** 데이터들의 위치 및 분포를 보여준다


```python
sns.distplot(x, rug=True, hist=False, kde=True)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_52_0.png)

<br />


### 2-4. kde (kernel density)

kde 는 histogram보다 **부드러운 형태의 분포 곡선**을 보여주는 방법


```python
sns.distplot(x, rug=False, hist=False, kde=True)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_56_0.png)

<br />


### 2-5. 가로로 표현하기


```python
sns.distplot(x, vertical=True)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_59_0.png)

<br />


### 2-6. 컬러 바꾸기


```python
sns.distplot(x, color='r')
plt.show()
```


![png](/images/S-Python-Seaborn2/output_62_0.png)

<br />

<br />


## **3. heatmap**

색상으로 표현할 수 있는 다양한 정보를 **일정한 이미지위에 열분포 형태의 비쥬얼한 그래픽**으로 출력하는 것이 특정이다

**주로 활용되는 경우:**

1. pivot table의 데이터를 시각화할 때
2. 데이터의 상관관계를 살펴볼 때

<br />

> ***reference:*** [ <sns.heatmap> Document](https://seaborn.pydata.org/generated/seaborn.heatmap.html?highlight=heatmap#seaborn.heatmap)

> **sns.heatmap** ( *data, annot=None, cmap=None* )
>
> * annot: If True, write the data value in each cell

  <br />

### 3-1. 기본 heatmap


```python
uniform_data = np.random.rand(10, 12)
sns.heatmap(uniform_data, annot=True)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_72_0.png)


컬러가 진할수록 숫자가 0에 가깝고, 연할수록 1에 가깝다

  <br />

### 3-2. pivot table을 활용하여 그리기  


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

<table  >
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
pivot = tips.pivot_table(index='day', columns='size', values='tip')
pivot
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

<table  >
  <thead>
    <tr style="text-align: right;">
      <th>size</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
    </tr>
    <tr>
      <th>day</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Thur</th>
      <td>1.83</td>
      <td>2.442500</td>
      <td>2.692500</td>
      <td>4.218000</td>
      <td>5.000000</td>
      <td>5.3</td>
    </tr>
    <tr>
      <th>Fri</th>
      <td>1.92</td>
      <td>2.644375</td>
      <td>3.000000</td>
      <td>4.730000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Sat</th>
      <td>1.00</td>
      <td>2.517547</td>
      <td>3.797778</td>
      <td>4.123846</td>
      <td>3.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Sun</th>
      <td>NaN</td>
      <td>2.816923</td>
      <td>3.120667</td>
      <td>4.087778</td>
      <td>4.046667</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
sns.heatmap(pivot, cmap='Blues', annot=True)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_78_0.png)

<br />


### 3-3. correlation(상관관계)를 시각화

**corr()** 함수는 데이터의 상관관계를 보여줌


```python
titanic.corr()
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

<table  >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>survived</th>
      <th>pclass</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>adult_male</th>
      <th>alone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>survived</th>
      <td>1.000000</td>
      <td>-0.338481</td>
      <td>-0.077221</td>
      <td>-0.035322</td>
      <td>0.081629</td>
      <td>0.257307</td>
      <td>-0.557080</td>
      <td>-0.203367</td>
    </tr>
    <tr>
      <th>pclass</th>
      <td>-0.338481</td>
      <td>1.000000</td>
      <td>-0.369226</td>
      <td>0.083081</td>
      <td>0.018443</td>
      <td>-0.549500</td>
      <td>0.094035</td>
      <td>0.135207</td>
    </tr>
    <tr>
      <th>age</th>
      <td>-0.077221</td>
      <td>-0.369226</td>
      <td>1.000000</td>
      <td>-0.308247</td>
      <td>-0.189119</td>
      <td>0.096067</td>
      <td>0.280328</td>
      <td>0.198270</td>
    </tr>
    <tr>
      <th>sibsp</th>
      <td>-0.035322</td>
      <td>0.083081</td>
      <td>-0.308247</td>
      <td>1.000000</td>
      <td>0.414838</td>
      <td>0.159651</td>
      <td>-0.253586</td>
      <td>-0.584471</td>
    </tr>
    <tr>
      <th>parch</th>
      <td>0.081629</td>
      <td>0.018443</td>
      <td>-0.189119</td>
      <td>0.414838</td>
      <td>1.000000</td>
      <td>0.216225</td>
      <td>-0.349943</td>
      <td>-0.583398</td>
    </tr>
    <tr>
      <th>fare</th>
      <td>0.257307</td>
      <td>-0.549500</td>
      <td>0.096067</td>
      <td>0.159651</td>
      <td>0.216225</td>
      <td>1.000000</td>
      <td>-0.182024</td>
      <td>-0.271832</td>
    </tr>
    <tr>
      <th>adult_male</th>
      <td>-0.557080</td>
      <td>0.094035</td>
      <td>0.280328</td>
      <td>-0.253586</td>
      <td>-0.349943</td>
      <td>-0.182024</td>
      <td>1.000000</td>
      <td>0.404744</td>
    </tr>
    <tr>
      <th>alone</th>
      <td>-0.203367</td>
      <td>0.135207</td>
      <td>0.198270</td>
      <td>-0.584471</td>
      <td>-0.583398</td>
      <td>-0.271832</td>
      <td>0.404744</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
sns.heatmap(titanic.corr(), annot=True, cmap='YlGnBu')
plt.show()
```


![png](/images/S-Python-Seaborn2/output_83_0.png)



<br />

<br />


## **4. pairplot**

pairplot은 grid 형태로 각 **집합의 조합에 대해 히스토그램과 분포도**를 그린다.  
(숫자형 column에 대해서만 그려줌)

> ***reference:*** [<sns.pairplot> Document](https://seaborn.pydata.org/generated/seaborn.pairplot.html?highlight=pairplot#seaborn.pairplot)

> **sns.pairplot** ( *data, hue=None, palette=None, height=2.5* )

  <br />


```python
tips.head()
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

<table  >
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
  </tbody>
</table>

</div>

<br />

  

### 4-1. 기본 pairplot 그리기


```python
sns.pairplot(tips)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_94_0.png)

<br />


### 4-2. hue 옵션으로 특성 구분


```python
sns.pairplot(tips, hue='size')
plt.show()
```


![png](/images/S-Python-Seaborn2/output_97_0.png)

<br />


### 4-3. 컬러 팔레트 적용


```python
sns.pairplot(tips, hue='size', palette='rainbow')
plt.show()
```


![png](/images/S-Python-Seaborn2/output_100_0.png)

<br />


### 4-4. 사이즈 적용


```python
sns.pairplot(tips, hue='size', palette='rainbow', height=4)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_103_0.png)

<br />

<br />


## **5. violinplot**

마이올린처럼 생긴 violinplot다.  

column에 대한 **데이터의 비교 분포도**를 확인할 수 있다.

* 곡선형 부분 (뚱뚱한 부분)은 데이터의 분포를 나타냄
* 양쪽 끝 뾰족한 부분은 데이터의 최소값과 최대값을 나타냄

<br />

> ***reference:*** [<sns.violinplot> Document](https://seaborn.pydata.org/generated/seaborn.violinplot.html)

> **sns.violinplot** ( *x=None. y=None, hue=None, data=None, split=False* )
>
> * **split:** When using hue nesting with a variable that takes two levels, setting split to True will draw half of a violin for each level. This can make it easier to directly compare the distributions.

 <br /> 


```python
tips.head()
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

<table  >
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
  </tbody>
</table>

</div>

<br />

### 5-1. 기본 violinplot 그리기


```python
sns.violinplot(x=tips['total_bill'])
plt.show()
```


![png](/images/S-Python-Seaborn2/output_113_0.png)

<br />


### 5-2. 비교 분포 확인

x, y축을 지정해줌으로써 바이올린을 분할하여 **비교 분포**를 볼 수 있다


```python
sns.violinplot(x='day', y='total_bill', data=tips)
plt.show()
```

![png](/images/S-Python-Seaborn2/output_117_0.png)

<br />


### 5-3. 가로로 뉘인 violinplot

* x축, y축 변경


```python
sns.violinplot(y='day', x='total_bill', data=tips)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_120_0.png)

<br />


### 5-4. hue 옵션으로 분포 비교

사실 hue옵션을 사용하지 않으면 바이올린이 대칭이기 때문에 분포의 큰 의미는 없다.  
하지만, hue옵션을 주면, **단일 column에 대한 바이올린 모양의 비교**를 할 수 있다.


```python
sns.violinplot(x='day', y='total_bill', hue='smoker', data=tips, palette='muted')
plt.show()
```


![png](/images/S-Python-Seaborn2/output_124_0.png)

<br />


**split 옵션으로 바이올린을 합쳐서 볼 수 있다**


```python
sns.violinplot(x='day', y='total_bill', hue='smoker', data=tips, palette='muted', split=True)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_127_0.png)


violinplot은 이런 경우에 많이 활용된다

 <br /> <br />

  

## **6. lmplot**

lmport (*initial: 소문자 L*) 은 column간의 **선형관계를 확인하기에 용이한 차트**임.  
또한, **outlier**도 같이 짐작해 볼 수 있다.

> ***reference:*** [<sns.lmplot> Document](https://seaborn.pydata.org/generated/seaborn.lmplot.html)

> **sns.lmplot** ( *x, y, data, hue=None, col=None, col_wrap=None, row=None, height=5* )

  <br />


```python
tips.head()
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

<table  >
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
  </tbody>
</table>

</div>

<br />

### 6-1. 기본 lmplot


```python
sns.lmplot(x='total_bill', y='tip', data=tips, height=6)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_138_0.png)

<br />


### 6-2. hue 옵션으로 다중 선형관계 그리기

아래의 그래프를 통하여 비흡연자가, 흡연자 대비 좀 더 **가파른 선형관계**를 가지는 것을 볼 수 있다


```python
sns.lmplot(x='total_bill', y='tip', hue='smoker', data=tips, height=6)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_142_0.png)

<br />


### 6-3. col 옵션을 추가하여 그래프를 별도로 그려볼 수 있다

또한, ```col_wrap```으로 한 줄에 표기할 column의 갯수를 명시할 수 있다


```python
sns.lmplot(x='total_bill', y='tip', hue='smoker', col='day', col_wrap=2, data=tips, height=6)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_146_0.png)

<br />

<br />


## **7. relplot**

두 column간 상관관계를 보지만 ```lmport```처럼 선형관계를 따로 그려주지 않다

> ***reference:*** [<sns.replot> Document](https://seaborn.pydata.org/generated/seaborn.relplot.html?highlight=relplot#seaborn.relplot)

> **sns.relplot** ( *x, y, data, hue=None, col=None, row=None, height=5, palette=None* )

  <br />


```python
tips.head()
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

<table  >
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
  </tbody>
</table>

</div>



<br />  

### 7-1. 기본 relplot


```python
sns.relplot(x='total_bill', y='tip', hue='day', data=tips)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_157_0.png)

<br />


### 7-2. col 옵션으로 그래프 분할


```python
sns.relplot(x='total_bill', y='tip', hue='day', col='time', data=tips)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_160_0.png)

<br />


### 7-3. row와 column에 표기할 데이터 column 선택


```python
sns.relplot(x='total_bill', y='tip',hue='day', col='time', row='sex', data=tips)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_163_0.png)

<br />


### 7-4. 컬러 팔레트 적용


```python
sns.relplot(x='total_bill', y='tip', hue='day', col='time', row='sex', data=tips, palette='CMRmap_r')
plt.show()
```


![png](/images/S-Python-Seaborn2/output_166_0.png)

<br />

<br />


## **8. jointplot**

jointplot은 scatter(산점도)와 histogram(분포)을 동시에 그려줌.(숫자형 데이터만)

> ***reference:*** [<sns.jointplot> Document](https://seaborn.pydata.org/generated/seaborn.jointplot.html?highlight=jointplot#seaborn.jointplot)

> **sns.jointplot** ( *x, y, data=None, kind='scatter', height=6* )
>
> * **kind**: kind of plot to draw. {'scatter', 'reg', 'resid', 'kde', 'hex'}

  <br />


```python
tips.head()
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

<table  >
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
  </tbody>
</table>

</div>



<br />  

### 8-1. 기본 jointplot 그리기

**default 로 "scatter plot"을 그린다  (kind='scatter')**


```python
sns.jointplot(x='total_bill', y='tip', data=tips)
plt.show()
```


![png](/images/S-Python-Seaborn2/output_178_0.png)

<br />


### 8-2. 선형관계를 표현하는 regression 라인 그리기

**옵션: kind='reg'**


```python
sns.jointplot('total_bill', 'tip', data=tips, kind='reg')
plt.show()
```


![png](/images/S-Python-Seaborn2/output_182_0.png)

<br />


### 8-3. hex 밀도 보기

**옵션: kind='hex'**


```python
sns.jointplot('total_bill', 'tip', data=tips, kind='hex')
plt.show()
```


![png](/images/S-Python-Seaborn2/output_186_0.png)

<br />


### 8-4. 등고선 모양으로 밀집도 확인하기

**kind='kde'** 옵션으로 데이터의 밀집도를 보다 부드러운 선으로 확인할 수 있다


```python
iris = sns.load_dataset('iris')
iris
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

<table  >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>145</th>
      <td>6.7</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.3</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>146</th>
      <td>6.3</td>
      <td>2.5</td>
      <td>5.0</td>
      <td>1.9</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>147</th>
      <td>6.5</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.0</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>148</th>
      <td>6.2</td>
      <td>3.4</td>
      <td>5.4</td>
      <td>2.3</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>149</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
      <td>virginica</td>
    </tr>
  </tbody>
</table>
<p>150 rows × 5 columns</p>

</div>

<br />

  


```python
sns.jointplot('sepal_width', 'petal_length', data=iris, kind='kde', color='g')
plt.show()
```


![png](/images/S-Python-Seaborn2/output_192_0.png)

<br />

<br />
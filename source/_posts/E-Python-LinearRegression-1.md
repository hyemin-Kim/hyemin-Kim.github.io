---
title: 【실습】 Python >> EDA & Linear Regression -- 부동산 가격 예측
tags:
  - Python
  - sklearn
  - Machine Learning
  - 회귀
categories:
  - 【EXERCISE】
  - Python
cover: https://s1.ax1x.com/2020/08/25/dciYCV.png
description: Linear Regression -- 부동산 가격 예측 
typora-root-url: ..
abbrlink: 6537
date: 2020-08-11 00:42:27
---

# 【EDA & Regression 실습】 -- 부동산 데이터

@[toc]  

<br />

## **0. 개요**

미국 매사추세츠주의 주택 가격 데이터(Boston Housing 1970)를 활용해 지역의 평균 주택 가격을 예측하는 선형 회귀 모델을 만들었고, 이를 기초하여 주택 가격의 영향 요소 파악 및 주택 가격 예측을 진행하였습니다.  

전체 분석 절차는 다음과 같습니다:

1. 데이터 파악 (EDA: 탐색적 데이터 분석)

   * 데이터셋 기본 정보 파악
   * 변수 특징 탐색
   * 변수간 관계 탐색

2. 데이터 전처리

3. 모델링

4. 주택 가격 영향 요소 파악

5. 주택 가격 예측 및 모델 예측 성능 평가

   <br />  

## **1. Library & Data Import**

**>> 사용할 Library**


```python
%matplotlib inline

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

import warnings
warnings.filterwarnings('ignore')
```

<br />  

**>> 사용할 데이터셋 -- Boston Housing Dataset**

분석에 사용될 데이터셋은 [Boston Housing 1970](http://lib.stat.cmu.edu/datasets/boston_corrected.txt)데이터의 일부 변수를 추출한 데이터입니다.  
여기에 미국 매사추세츠주 92개 도시(TOWN)의 506개 지역의 주택 가격 및 기타 지역 특성 데이터가 포함되어 있습니다. [(Dataset Introduction)](https://geodacenter.github.io/data-and-lab/boston-housing/)  

데이터셋을 불러와서 첫 다섯 줄을 출력하여 데이터의 구성을 한 번 살펴볼게요.


```python
df = pd.read_csv("https://raw.githubusercontent.com/yoonkt200/FastCampusDataset/master/BostonHousing2.csv")
```


```python
df.head()
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
<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TOWN</th>
      <th>LON</th>
      <th>LAT</th>
      <th>CMEDV</th>
      <th>CRIM</th>
      <th>ZN</th>
      <th>INDUS</th>
      <th>CHAS</th>
      <th>NOX</th>
      <th>RM</th>
      <th>AGE</th>
      <th>DIS</th>
      <th>RAD</th>
      <th>TAX</th>
      <th>PTRATIO</th>
      <th>B</th>
      <th>LSTAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Nahant</td>
      <td>-70.955</td>
      <td>42.2550</td>
      <td>24.0</td>
      <td>0.00632</td>
      <td>18.0</td>
      <td>2.31</td>
      <td>0</td>
      <td>0.538</td>
      <td>6.575</td>
      <td>65.2</td>
      <td>4.0900</td>
      <td>1</td>
      <td>296</td>
      <td>15.3</td>
      <td>396.90</td>
      <td>4.98</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Swampscott</td>
      <td>-70.950</td>
      <td>42.2875</td>
      <td>21.6</td>
      <td>0.02731</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0</td>
      <td>0.469</td>
      <td>6.421</td>
      <td>78.9</td>
      <td>4.9671</td>
      <td>2</td>
      <td>242</td>
      <td>17.8</td>
      <td>396.90</td>
      <td>9.14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Swampscott</td>
      <td>-70.936</td>
      <td>42.2830</td>
      <td>34.7</td>
      <td>0.02729</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0</td>
      <td>0.469</td>
      <td>7.185</td>
      <td>61.1</td>
      <td>4.9671</td>
      <td>2</td>
      <td>242</td>
      <td>17.8</td>
      <td>392.83</td>
      <td>4.03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Marblehead</td>
      <td>-70.928</td>
      <td>42.2930</td>
      <td>33.4</td>
      <td>0.03237</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0</td>
      <td>0.458</td>
      <td>6.998</td>
      <td>45.8</td>
      <td>6.0622</td>
      <td>3</td>
      <td>222</td>
      <td>18.7</td>
      <td>394.63</td>
      <td>2.94</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Marblehead</td>
      <td>-70.922</td>
      <td>42.2980</td>
      <td>36.2</td>
      <td>0.06905</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0</td>
      <td>0.458</td>
      <td>7.147</td>
      <td>54.2</td>
      <td>6.0622</td>
      <td>3</td>
      <td>222</td>
      <td>18.7</td>
      <td>396.90</td>
      <td>5.33</td>
    </tr>
  </tbody>
</table>
</div>
</div>



<br />

**>> Feature Description**  

각 변수의 의미는 다음과 같습니다:

* TOWN: 소속 도시 이름

* LON, LAT: 해당 지역의 경도(Longitudes) 위도(Latitudes) 정보

* **CMEDV: 해당 지역의 주택 가격 (중앙값)** (corrected median values of housing in USD 1000)

* CRIM: 지역 범죄율 (per capita crime)

* ZN: 소속 도시에 25,000 제곱 피트(sq.ft) 이상의 주택지 비율

* INDUS: 소속 도시에 상업적 비즈니스에 활용되지 않는 농지 면적

* CHAS: 해당 지역이 Charles 강과 접하고 있는지 여부 (dummy variable)

* NOX: 소속 도시의 산화질소 농도

* RM: 해당 지역의 자택당 평균 방 갯수

* AGE: 해당 지역에 1940년 이전에 건설된 주택의 비율

* DIS: 5개의 보스턴 고용 센터와의 거리에 따른 가중치 부여

* RAD: 소속 도시가 Radial 고속도로와의 접근성 지수

* TAX: 소속 도시의 10000달러당 재산세

* PTRATIO: 소속 도시의 학생-교사 비율

* B: 해당 지역의 흑인 지수 (1000(Bk - 0.63)^2), Bk는 흑인의 비율

* LSTAT: 해당 지역의 빈곤층 비율

  <br />

  <br />

  

## **2. 데이터 파악 (EDA: 탐색적 데이터 분석)**

이제 데이터셋의 기본 정보 및 각 변수의 특성을 파악해 보겠습니다.


```python
# 그래프 배경 설정
sns.set_style('darkgrid')
```

  <br />

### 2-1. 데이터셋 기본 정보 파악

먼저 데이터셋의 기본 정보부터 알아볼게요.


```python
# shape (dimension)
df.shape
```


    (506, 17)

<br />


```python
# 결측치
df.isnull().sum()
```


    TOWN       0
    LON        0
    LAT        0
    CMEDV      0
    CRIM       0
    ZN         0
    INDUS      0
    CHAS       0
    NOX        0
    RM         0
    AGE        0
    DIS        0
    RAD        0
    TAX        0
    PTRATIO    0
    B          0
    LSTAT      0
    dtype: int64

<br />

데이터셋은 총 506개의 관측치(observations)과 17개의 변수(variables)로 구성되어 있고 결측치는 존재하지 않습니다.  

각 **변수의 타입** 및 **기초 통계량 (범주형 변수는 범주 구성)** 을 확인 해보면 다음과 같습니다.


```python
# data type
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 506 entries, 0 to 505
    Data columns (total 17 columns):
     #   Column   Non-Null Count  Dtype  
    ---  ------   --------------  -----  
     0   TOWN     506 non-null    object 
     1   LON      506 non-null    float64
     2   LAT      506 non-null    float64
     3   CMEDV    506 non-null    float64
     4   CRIM     506 non-null    float64
     5   ZN       506 non-null    float64
     6   INDUS    506 non-null    float64
     7   CHAS     506 non-null    int64  
     8   NOX      506 non-null    float64
     9   RM       506 non-null    float64
     10  AGE      506 non-null    float64
     11  DIS      506 non-null    float64
     12  RAD      506 non-null    int64  
     13  TAX      506 non-null    int64  
     14  PTRATIO  506 non-null    float64
     15  B        506 non-null    float64
     16  LSTAT    506 non-null    float64
    dtypes: float64(13), int64(3), object(1)
    memory usage: 67.3+ KB

이중 TOWN(소속 도시 이름)만 문자형 변수이고, 이를 제외한 모든 변수가 숫자형 변수입니다. 

<br />


```python
# numerical variable
df.describe() 
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
<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>LON</th>
      <th>LAT</th>
      <th>CMEDV</th>
      <th>CRIM</th>
      <th>ZN</th>
      <th>INDUS</th>
      <th>CHAS</th>
      <th>NOX</th>
      <th>RM</th>
      <th>AGE</th>
      <th>DIS</th>
      <th>RAD</th>
      <th>TAX</th>
      <th>PTRATIO</th>
      <th>B</th>
      <th>LSTAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
      <td>506.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-71.056389</td>
      <td>42.216440</td>
      <td>22.528854</td>
      <td>3.613524</td>
      <td>11.363636</td>
      <td>11.136779</td>
      <td>0.069170</td>
      <td>0.554695</td>
      <td>6.284634</td>
      <td>68.574901</td>
      <td>3.795043</td>
      <td>9.549407</td>
      <td>408.237154</td>
      <td>18.455534</td>
      <td>356.674032</td>
      <td>12.653063</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.075405</td>
      <td>0.061777</td>
      <td>9.182176</td>
      <td>8.601545</td>
      <td>23.322453</td>
      <td>6.860353</td>
      <td>0.253994</td>
      <td>0.115878</td>
      <td>0.702617</td>
      <td>28.148861</td>
      <td>2.105710</td>
      <td>8.707259</td>
      <td>168.537116</td>
      <td>2.164946</td>
      <td>91.294864</td>
      <td>7.141062</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-71.289500</td>
      <td>42.030000</td>
      <td>5.000000</td>
      <td>0.006320</td>
      <td>0.000000</td>
      <td>0.460000</td>
      <td>0.000000</td>
      <td>0.385000</td>
      <td>3.561000</td>
      <td>2.900000</td>
      <td>1.129600</td>
      <td>1.000000</td>
      <td>187.000000</td>
      <td>12.600000</td>
      <td>0.320000</td>
      <td>1.730000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-71.093225</td>
      <td>42.180775</td>
      <td>17.025000</td>
      <td>0.082045</td>
      <td>0.000000</td>
      <td>5.190000</td>
      <td>0.000000</td>
      <td>0.449000</td>
      <td>5.885500</td>
      <td>45.025000</td>
      <td>2.100175</td>
      <td>4.000000</td>
      <td>279.000000</td>
      <td>17.400000</td>
      <td>375.377500</td>
      <td>6.950000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-71.052900</td>
      <td>42.218100</td>
      <td>21.200000</td>
      <td>0.256510</td>
      <td>0.000000</td>
      <td>9.690000</td>
      <td>0.000000</td>
      <td>0.538000</td>
      <td>6.208500</td>
      <td>77.500000</td>
      <td>3.207450</td>
      <td>5.000000</td>
      <td>330.000000</td>
      <td>19.050000</td>
      <td>391.440000</td>
      <td>11.360000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>-71.019625</td>
      <td>42.252250</td>
      <td>25.000000</td>
      <td>3.677082</td>
      <td>12.500000</td>
      <td>18.100000</td>
      <td>0.000000</td>
      <td>0.624000</td>
      <td>6.623500</td>
      <td>94.075000</td>
      <td>5.188425</td>
      <td>24.000000</td>
      <td>666.000000</td>
      <td>20.200000</td>
      <td>396.225000</td>
      <td>16.955000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>-70.810000</td>
      <td>42.381000</td>
      <td>50.000000</td>
      <td>88.976200</td>
      <td>100.000000</td>
      <td>27.740000</td>
      <td>1.000000</td>
      <td>0.871000</td>
      <td>8.780000</td>
      <td>100.000000</td>
      <td>12.126500</td>
      <td>24.000000</td>
      <td>711.000000</td>
      <td>22.000000</td>
      <td>396.900000</td>
      <td>37.970000</td>
    </tr>
  </tbody>
</table>
</div>

</div>

<br />


```python
# categorical variable
num_town = df['TOWN'].unique()
print(len(num_town))
num_town
```

    92



    array(['Nahant', 'Swampscott', 'Marblehead', 'Salem', 'Lynn', 'Sargus',
           'Lynnfield', 'Peabody', 'Danvers', 'Middleton', 'Topsfield',
           'Hamilton', 'Wenham', 'Beverly', 'Manchester', 'North Reading',
           'Wilmington', 'Burlington', 'Woburn', 'Reading', 'Wakefield',
           'Melrose', 'Stoneham', 'Winchester', 'Medford', 'Malden',
           'Everett', 'Somerville', 'Cambridge', 'Arlington', 'Belmont',
           'Lexington', 'Bedford', 'Lincoln', 'Concord', 'Sudbury', 'Wayland',
           'Weston', 'Waltham', 'Watertown', 'Newton', 'Natick', 'Framingham',
           'Ashland', 'Sherborn', 'Brookline', 'Dedham', 'Needham',
           'Wellesley', 'Dover', 'Medfield', 'Millis', 'Norfolk', 'Walpole',
           'Westwood', 'Norwood', 'Sharon', 'Canton', 'Milton', 'Quincy',
           'Braintree', 'Randolph', 'Holbrook', 'Weymouth', 'Cohasset',
           'Hull', 'Hingham', 'Rockland', 'Hanover', 'Norwell', 'Scituate',
           'Marshfield', 'Duxbury', 'Pembroke', 'Boston Allston-Brighton',
           'Boston Back Bay', 'Boston Beacon Hill', 'Boston North End',
           'Boston Charlestown', 'Boston East Boston', 'Boston South Boston',
           'Boston Downtown', 'Boston Roxbury', 'Boston Savin Hill',
           'Boston Dorchester', 'Boston Mattapan', 'Boston Forest Hills',
           'Boston West Roxbury', 'Boston Hyde Park', 'Chelsea', 'Revere',
           'Winthrop'], dtype=object)

<br />

  

### 2-2. 종속 변수(목표 변수) 탐색

**>> Target Variable: 'CMEDV'(주택 가격) 탐색**

이제 각 변수의 특성을 시각화 도구를 통해 파악해보겠습니다.  
먼저 우리가 예측하고자 하는 대상, 즉 회귀 모델의 종속 변수인 "주택 가격"('CMECV') 부터 살펴볼게요.


```python
# 기초 통계량
df['CMEDV'].describe()
```


    count    506.000000
    mean      22.528854
    std        9.182176
    min        5.000000
    25%       17.025000
    50%       21.200000
    75%       25.000000
    max       50.000000
    Name: CMEDV, dtype: float64

<br />


```python
# 분포
df['CMEDV'].hist(bins=50)
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1ca69ebcf48>




![png](/images/E-Python-LinearRegression-1/output_36_1.png)


**boxplot:**

1. Pandas Function ([pandas.DataFrame.boxplot](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.boxplot.html?highlight=boxplot#pandas.DataFrame.boxplot))
2. Matplotlib Function ([matplotlib.pyplot.boxplot](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.boxplot.html#matplotlib.pyplot.boxplot))


```python
# boxplot - Pandas
df.boxplot(column=['CMEDV'])
plt.show()
```


![png](/images/E-Python-LinearRegression-1/output_38_0.png)

<br />

```python
# boxplot - matplotlib
plt.boxplot(df['CMEDV'])
plt.show()
```


![png](/images/E-Python-LinearRegression-1/output_39_0.png)


분포를 살펴보면, 주택 가격이 대부분 ```$17,000``` ~ ```$25,000``` 사이에 분포되어 있으며, 소수의 ```$40,000``` 이상인 고가 주택도 존재합니다.

<br />  

### 2-3. 설명 변수 탐색

**>> 설명 변수의 분포 탐색**


```python
# numerical features (except "LON" & "LAT")
numerical_columns = ['CRIM', 'ZN', 'INDUS', 'CHAS', 'NOX', 'RM', 'AGE', 'DIS', 'RAD', 'TAX', 'PTRATIO', 'B', 'LSTAT']

fig = plt.figure(figsize = (16, 20))
ax = fig.gca()  # Axes 생성

df[numerical_columns].hist(ax=ax)
plt.show()
```


![png](/images/E-Python-LinearRegression-1/output_44_0.png)

<br />


### 2-4. 설명변수와 종속변수 간의 관계 탐색

**>> 변수간의 상관계수 파악**

먼저 변수간의 상관계수를 추출해보겠습니다. 


```python
# Person 상관계수
cols = ['CMEDV', 'CRIM', 'ZN', 'INDUS', 'CHAS', 'NOX', 'RM', 'AGE', 'DIS', 'RAD', 'TAX', 'PTRATIO', 'B', 'LSTAT']

corr = df[cols].corr(method = 'pearson')
corr
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
<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CMEDV</th>
      <th>CRIM</th>
      <th>ZN</th>
      <th>INDUS</th>
      <th>CHAS</th>
      <th>NOX</th>
      <th>RM</th>
      <th>AGE</th>
      <th>DIS</th>
      <th>RAD</th>
      <th>TAX</th>
      <th>PTRATIO</th>
      <th>B</th>
      <th>LSTAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CMEDV</th>
      <td>1.000000</td>
      <td>-0.389582</td>
      <td>0.360386</td>
      <td>-0.484754</td>
      <td>0.175663</td>
      <td>-0.429300</td>
      <td>0.696304</td>
      <td>-0.377999</td>
      <td>0.249315</td>
      <td>-0.384766</td>
      <td>-0.471979</td>
      <td>-0.505655</td>
      <td>0.334861</td>
      <td>-0.740836</td>
    </tr>
    <tr>
      <th>CRIM</th>
      <td>-0.389582</td>
      <td>1.000000</td>
      <td>-0.200469</td>
      <td>0.406583</td>
      <td>-0.055892</td>
      <td>0.420972</td>
      <td>-0.219247</td>
      <td>0.352734</td>
      <td>-0.379670</td>
      <td>0.625505</td>
      <td>0.582764</td>
      <td>0.289946</td>
      <td>-0.385064</td>
      <td>0.455621</td>
    </tr>
    <tr>
      <th>ZN</th>
      <td>0.360386</td>
      <td>-0.200469</td>
      <td>1.000000</td>
      <td>-0.533828</td>
      <td>-0.042697</td>
      <td>-0.516604</td>
      <td>0.311991</td>
      <td>-0.569537</td>
      <td>0.664408</td>
      <td>-0.311948</td>
      <td>-0.314563</td>
      <td>-0.391679</td>
      <td>0.175520</td>
      <td>-0.412995</td>
    </tr>
    <tr>
      <th>INDUS</th>
      <td>-0.484754</td>
      <td>0.406583</td>
      <td>-0.533828</td>
      <td>1.000000</td>
      <td>0.062938</td>
      <td>0.763651</td>
      <td>-0.391676</td>
      <td>0.644779</td>
      <td>-0.708027</td>
      <td>0.595129</td>
      <td>0.720760</td>
      <td>0.383248</td>
      <td>-0.356977</td>
      <td>0.603800</td>
    </tr>
    <tr>
      <th>CHAS</th>
      <td>0.175663</td>
      <td>-0.055892</td>
      <td>-0.042697</td>
      <td>0.062938</td>
      <td>1.000000</td>
      <td>0.091203</td>
      <td>0.091251</td>
      <td>0.086518</td>
      <td>-0.099176</td>
      <td>-0.007368</td>
      <td>-0.035587</td>
      <td>-0.121515</td>
      <td>0.048788</td>
      <td>-0.053929</td>
    </tr>
    <tr>
      <th>NOX</th>
      <td>-0.429300</td>
      <td>0.420972</td>
      <td>-0.516604</td>
      <td>0.763651</td>
      <td>0.091203</td>
      <td>1.000000</td>
      <td>-0.302188</td>
      <td>0.731470</td>
      <td>-0.769230</td>
      <td>0.611441</td>
      <td>0.668023</td>
      <td>0.188933</td>
      <td>-0.380051</td>
      <td>0.590879</td>
    </tr>
    <tr>
      <th>RM</th>
      <td>0.696304</td>
      <td>-0.219247</td>
      <td>0.311991</td>
      <td>-0.391676</td>
      <td>0.091251</td>
      <td>-0.302188</td>
      <td>1.000000</td>
      <td>-0.240265</td>
      <td>0.205246</td>
      <td>-0.209847</td>
      <td>-0.292048</td>
      <td>-0.355501</td>
      <td>0.128069</td>
      <td>-0.613808</td>
    </tr>
    <tr>
      <th>AGE</th>
      <td>-0.377999</td>
      <td>0.352734</td>
      <td>-0.569537</td>
      <td>0.644779</td>
      <td>0.086518</td>
      <td>0.731470</td>
      <td>-0.240265</td>
      <td>1.000000</td>
      <td>-0.747881</td>
      <td>0.456022</td>
      <td>0.506456</td>
      <td>0.261515</td>
      <td>-0.273534</td>
      <td>0.602339</td>
    </tr>
    <tr>
      <th>DIS</th>
      <td>0.249315</td>
      <td>-0.379670</td>
      <td>0.664408</td>
      <td>-0.708027</td>
      <td>-0.099176</td>
      <td>-0.769230</td>
      <td>0.205246</td>
      <td>-0.747881</td>
      <td>1.000000</td>
      <td>-0.494588</td>
      <td>-0.534432</td>
      <td>-0.232471</td>
      <td>0.291512</td>
      <td>-0.496996</td>
    </tr>
    <tr>
      <th>RAD</th>
      <td>-0.384766</td>
      <td>0.625505</td>
      <td>-0.311948</td>
      <td>0.595129</td>
      <td>-0.007368</td>
      <td>0.611441</td>
      <td>-0.209847</td>
      <td>0.456022</td>
      <td>-0.494588</td>
      <td>1.000000</td>
      <td>0.910228</td>
      <td>0.464741</td>
      <td>-0.444413</td>
      <td>0.488676</td>
    </tr>
    <tr>
      <th>TAX</th>
      <td>-0.471979</td>
      <td>0.582764</td>
      <td>-0.314563</td>
      <td>0.720760</td>
      <td>-0.035587</td>
      <td>0.668023</td>
      <td>-0.292048</td>
      <td>0.506456</td>
      <td>-0.534432</td>
      <td>0.910228</td>
      <td>1.000000</td>
      <td>0.460853</td>
      <td>-0.441808</td>
      <td>0.543993</td>
    </tr>
    <tr>
      <th>PTRATIO</th>
      <td>-0.505655</td>
      <td>0.289946</td>
      <td>-0.391679</td>
      <td>0.383248</td>
      <td>-0.121515</td>
      <td>0.188933</td>
      <td>-0.355501</td>
      <td>0.261515</td>
      <td>-0.232471</td>
      <td>0.464741</td>
      <td>0.460853</td>
      <td>1.000000</td>
      <td>-0.177383</td>
      <td>0.374044</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.334861</td>
      <td>-0.385064</td>
      <td>0.175520</td>
      <td>-0.356977</td>
      <td>0.048788</td>
      <td>-0.380051</td>
      <td>0.128069</td>
      <td>-0.273534</td>
      <td>0.291512</td>
      <td>-0.444413</td>
      <td>-0.441808</td>
      <td>-0.177383</td>
      <td>1.000000</td>
      <td>-0.366087</td>
    </tr>
    <tr>
      <th>LSTAT</th>
      <td>-0.740836</td>
      <td>0.455621</td>
      <td>-0.412995</td>
      <td>0.603800</td>
      <td>-0.053929</td>
      <td>0.590879</td>
      <td>-0.613808</td>
      <td>0.602339</td>
      <td>-0.496996</td>
      <td>0.488676</td>
      <td>0.543993</td>
      <td>0.374044</td>
      <td>-0.366087</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>

</div>

<br />

상관계수를 좀 더 직관적인 Heatmap으로 표현해볼게요.


```python
# heatmap (seaborn)
fig = plt.figure(figsize = (16, 12))
ax = fig.gca()

sns.set(font_scale = 1.5)  # heatmap 안의 font-size 설정
heatmap = sns.heatmap(corr.values, annot = True, fmt='.2f', annot_kws={'size':15},
                      yticklabels = cols, xticklabels = cols, ax=ax, cmap = "RdYlBu")
plt.tight_layout()
plt.show()
```


![png](/images/E-Python-LinearRegression-1/output_52_0.png)


우리의 관심사인 target variable **"CMEDV - 주택 가격"**과 다른 변수간의 상관관계를 살펴보면, **"CMEDV - 주택 가격"**은 **"RM - 자택당 평균 방 갯수"(0.7)** 및 **"LSTAT - 빈곤층의 비율"(-0.74)**과 **강한 상관관계**를 보이고 있다는 것을 알 수 있습니다.  

이 두 변수와의 관계를 좀 더 자세히 살펴볼게요.

 <br /> 

**>> 종속 변수와 설명 변수간의 관계 탐색**

* 주택 가격 ( "CMEDV" )  ~  방 갯수 ( "RM" )


```python
# scatter plot
sns.scatterplot(data=df, x='RM', y='CMEDV', markers='o', color='blue', alpha=0.6)
plt.title('Scatter Plot')
plt.show()
```


![png](/images/E-Python-LinearRegression-1/output_57_0.png)


주택 가격이 방 갯수와 양의 상관관계(positive correlation)를 갖고 있습니다. 즉, 방 갯수가 많은 주택들이 상대적으로 더 높은 가격을 갖고 있습니다.

 <br /> 

* 주택 가격("CMEDV") ~ 빈곤층의 비율("LSTAT")


```python
# scatter plot
sns.scatterplot(data=df, x='LSTAT', y='CMEDV', markers='o', color='blue', alpha=0.6)
plt.title('Scatter Plot')
plt.show()
```


![png](/images/E-Python-LinearRegression-1/output_61_0.png)


주택 가격이 빈곤층의 비율과 음의 상관관계(negative correlation)를 갖고 있습니다. 즉, 빈곤층의 비율이 높은 지역의 주택 가격이 상대적으로 낮은 경향이 있습니다. 

 <br /> 

**>> 도시별 차이 탐색**

데이터를 살펴보면 여러 지역이 같은 도시에 속한 경우가 있습니다. 변수 중에서도 도시 단위로 측정되는 변수가 많고요. 따라서 우리는 자연스럽게 도시 간의 차이를 궁금하게 됩니다.

먼저 각 도시의 데이터 갯수부터 살펴볼게요.


```python
# 도시별 데이터 갯수
df['TOWN'].value_counts()
```


    Cambridge            30
    Boston Savin Hill    23
    Lynn                 22
    Boston Roxbury       19
    Newton               18
                         ..
    Hanover               1
    Hull                  1
    Sherborn              1
    Hamilton              1
    Dover                 1
    Name: TOWN, Length: 92, dtype: int64

<br />


```python
# 도시별 데이터 갯수 (bar plot)
df['TOWN'].value_counts().hist(bins=50)
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1ca6c233a48>




![png](/images/E-Python-LinearRegression-1/output_68_1.png)

<br />


이제 각 도시의 주택 가격 분포를 box plot을 통해 표현 해보겠습니다.


```python
# 도시별 주택 가격 특징 (boxplot 이용)
fig = plt.figure(figsize = (12, 20))
sns.boxplot(x='CMEDV', y='TOWN', data=df)
```


    <matplotlib.axes._subplots.AxesSubplot at 0x23cf3ff9ec8>




![png](/images/E-Python-LinearRegression-1/output_71_1.png)


그림을 보면, Boston 지역(Boston으로 시작하는 도시)의 주택 가격이 전반적으로 다른 지역보다 낮다는 것을 알 수 있습니다.

도시별 범죄율을 한 번 확인 해보면,


```python
# 도시별 범죄율 특징
fig = plt.figure(figsize = (12, 20))
sns.boxplot(x='CRIM', y='TOWN', data=df)
```


    <matplotlib.axes._subplots.AxesSubplot at 0x23cf407fec8>




![png](/images/E-Python-LinearRegression-1/output_73_1.png)


Boston 지역의 범죄율이 유독 높다는 것을 확인할 수 있고, 따라서 범죄율이 높은 지역의 주택 가격이 상대적으로 낮다는 것을 추측해볼 수 있겠습니다.

<br />  <br />

  

## **3. 주택 가격 예측 모델링: 회귀 분석**

이제 변수들을 활용하여 매사추세츠주 각 지역의 주택 가격을 예측하는 회귀 모델을 만들어 보겠습니다. 

### 3-1. 데이터 전처리

**>>  Feature 표준화**

먼저 Feature 들의 scale 차이를 없애기 위해 수치형 Feature에 대해서 표준화를 진행해야 합니다.


```python
df.head()
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
<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TOWN</th>
      <th>LON</th>
      <th>LAT</th>
      <th>CMEDV</th>
      <th>CRIM</th>
      <th>ZN</th>
      <th>INDUS</th>
      <th>CHAS</th>
      <th>NOX</th>
      <th>RM</th>
      <th>AGE</th>
      <th>DIS</th>
      <th>RAD</th>
      <th>TAX</th>
      <th>PTRATIO</th>
      <th>B</th>
      <th>LSTAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Nahant</td>
      <td>-70.955</td>
      <td>42.2550</td>
      <td>24.0</td>
      <td>0.00632</td>
      <td>18.0</td>
      <td>2.31</td>
      <td>0</td>
      <td>0.538</td>
      <td>6.575</td>
      <td>65.2</td>
      <td>4.0900</td>
      <td>1</td>
      <td>296</td>
      <td>15.3</td>
      <td>396.90</td>
      <td>4.98</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Swampscott</td>
      <td>-70.950</td>
      <td>42.2875</td>
      <td>21.6</td>
      <td>0.02731</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0</td>
      <td>0.469</td>
      <td>6.421</td>
      <td>78.9</td>
      <td>4.9671</td>
      <td>2</td>
      <td>242</td>
      <td>17.8</td>
      <td>396.90</td>
      <td>9.14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Swampscott</td>
      <td>-70.936</td>
      <td>42.2830</td>
      <td>34.7</td>
      <td>0.02729</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0</td>
      <td>0.469</td>
      <td>7.185</td>
      <td>61.1</td>
      <td>4.9671</td>
      <td>2</td>
      <td>242</td>
      <td>17.8</td>
      <td>392.83</td>
      <td>4.03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Marblehead</td>
      <td>-70.928</td>
      <td>42.2930</td>
      <td>33.4</td>
      <td>0.03237</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0</td>
      <td>0.458</td>
      <td>6.998</td>
      <td>45.8</td>
      <td>6.0622</td>
      <td>3</td>
      <td>222</td>
      <td>18.7</td>
      <td>394.63</td>
      <td>2.94</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Marblehead</td>
      <td>-70.922</td>
      <td>42.2980</td>
      <td>36.2</td>
      <td>0.06905</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0</td>
      <td>0.458</td>
      <td>7.147</td>
      <td>54.2</td>
      <td>6.0622</td>
      <td>3</td>
      <td>222</td>
      <td>18.7</td>
      <td>396.90</td>
      <td>5.33</td>
    </tr>
  </tbody>
</table>
</div>

</div>

<br />


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 506 entries, 0 to 505
    Data columns (total 17 columns):
     #   Column   Non-Null Count  Dtype  
    ---  ------   --------------  -----  
     0   TOWN     506 non-null    object 
     1   LON      506 non-null    float64
     2   LAT      506 non-null    float64
     3   CMEDV    506 non-null    float64
     4   CRIM     506 non-null    float64
     5   ZN       506 non-null    float64
     6   INDUS    506 non-null    float64
     7   CHAS     506 non-null    int64  
     8   NOX      506 non-null    float64
     9   RM       506 non-null    float64
     10  AGE      506 non-null    float64
     11  DIS      506 non-null    float64
     12  RAD      506 non-null    int64  
     13  TAX      506 non-null    int64  
     14  PTRATIO  506 non-null    float64
     15  B        506 non-null    float64
     16  LSTAT    506 non-null    float64
    dtypes: float64(13), int64(3), object(1)
    memory usage: 67.3+ KB

<br />문자형 변수인 "TOWN"와 범주형 변수인 "CHAS" (Dummy variable)를 제외하여 모든 수치형 변수에 대해서 표준화를 진행합니다. 


```python
from sklearn.preprocessing import StandardScaler

# feature standardization  (numerical_columns except dummy var.-"CHAS")
scaler = StandardScaler()  # 평균 0, 표준편차 1
scale_columns = ['CRIM', 'ZN', 'INDUS', 'NOX', 'RM', 'AGE', 'DIS', 'RAD', 'TAX', 'PTRATIO', 'B', 'LSTAT']
df[scale_columns] = scaler.fit_transform(df[scale_columns])
```


```python
df.head()
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
<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TOWN</th>
      <th>LON</th>
      <th>LAT</th>
      <th>CMEDV</th>
      <th>CRIM</th>
      <th>ZN</th>
      <th>INDUS</th>
      <th>CHAS</th>
      <th>NOX</th>
      <th>RM</th>
      <th>AGE</th>
      <th>DIS</th>
      <th>RAD</th>
      <th>TAX</th>
      <th>PTRATIO</th>
      <th>B</th>
      <th>LSTAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Nahant</td>
      <td>-70.955</td>
      <td>42.2550</td>
      <td>24.0</td>
      <td>-0.419782</td>
      <td>0.284830</td>
      <td>-1.287909</td>
      <td>0</td>
      <td>-0.144217</td>
      <td>0.413672</td>
      <td>-0.120013</td>
      <td>0.140214</td>
      <td>-0.982843</td>
      <td>-0.666608</td>
      <td>-1.459000</td>
      <td>0.441052</td>
      <td>-1.075562</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Swampscott</td>
      <td>-70.950</td>
      <td>42.2875</td>
      <td>21.6</td>
      <td>-0.417339</td>
      <td>-0.487722</td>
      <td>-0.593381</td>
      <td>0</td>
      <td>-0.740262</td>
      <td>0.194274</td>
      <td>0.367166</td>
      <td>0.557160</td>
      <td>-0.867883</td>
      <td>-0.987329</td>
      <td>-0.303094</td>
      <td>0.441052</td>
      <td>-0.492439</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Swampscott</td>
      <td>-70.936</td>
      <td>42.2830</td>
      <td>34.7</td>
      <td>-0.417342</td>
      <td>-0.487722</td>
      <td>-0.593381</td>
      <td>0</td>
      <td>-0.740262</td>
      <td>1.282714</td>
      <td>-0.265812</td>
      <td>0.557160</td>
      <td>-0.867883</td>
      <td>-0.987329</td>
      <td>-0.303094</td>
      <td>0.396427</td>
      <td>-1.208727</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Marblehead</td>
      <td>-70.928</td>
      <td>42.2930</td>
      <td>33.4</td>
      <td>-0.416750</td>
      <td>-0.487722</td>
      <td>-1.306878</td>
      <td>0</td>
      <td>-0.835284</td>
      <td>1.016303</td>
      <td>-0.809889</td>
      <td>1.077737</td>
      <td>-0.752922</td>
      <td>-1.106115</td>
      <td>0.113032</td>
      <td>0.416163</td>
      <td>-1.361517</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Marblehead</td>
      <td>-70.922</td>
      <td>42.2980</td>
      <td>36.2</td>
      <td>-0.412482</td>
      <td>-0.487722</td>
      <td>-1.306878</td>
      <td>0</td>
      <td>-0.835284</td>
      <td>1.228577</td>
      <td>-0.511180</td>
      <td>1.077737</td>
      <td>-0.752922</td>
      <td>-1.106115</td>
      <td>0.113032</td>
      <td>0.441052</td>
      <td>-1.026501</td>
    </tr>
  </tbody>
</table>
</div>

</div>



 <br /> 

**>> Training set / Test set 나누기**

나중에 도출될 예측 모델의 예측 성능을 평가하기 위해, 먼저 전체 데이터셋을 "Training set"과 "Test set"으로 나누겠습니다. Training set에서 모델을 학습하고 Test set에서 모델의 예측 성능을 검증할 겁니다.


```python
# features for linear regression model
df[numerical_columns].head()
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
<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CRIM</th>
      <th>ZN</th>
      <th>INDUS</th>
      <th>CHAS</th>
      <th>NOX</th>
      <th>RM</th>
      <th>AGE</th>
      <th>DIS</th>
      <th>RAD</th>
      <th>TAX</th>
      <th>PTRATIO</th>
      <th>B</th>
      <th>LSTAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.419782</td>
      <td>0.284830</td>
      <td>-1.287909</td>
      <td>0</td>
      <td>-0.144217</td>
      <td>0.413672</td>
      <td>-0.120013</td>
      <td>0.140214</td>
      <td>-0.982843</td>
      <td>-0.666608</td>
      <td>-1.459000</td>
      <td>0.441052</td>
      <td>-1.075562</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.417339</td>
      <td>-0.487722</td>
      <td>-0.593381</td>
      <td>0</td>
      <td>-0.740262</td>
      <td>0.194274</td>
      <td>0.367166</td>
      <td>0.557160</td>
      <td>-0.867883</td>
      <td>-0.987329</td>
      <td>-0.303094</td>
      <td>0.441052</td>
      <td>-0.492439</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.417342</td>
      <td>-0.487722</td>
      <td>-0.593381</td>
      <td>0</td>
      <td>-0.740262</td>
      <td>1.282714</td>
      <td>-0.265812</td>
      <td>0.557160</td>
      <td>-0.867883</td>
      <td>-0.987329</td>
      <td>-0.303094</td>
      <td>0.396427</td>
      <td>-1.208727</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.416750</td>
      <td>-0.487722</td>
      <td>-1.306878</td>
      <td>0</td>
      <td>-0.835284</td>
      <td>1.016303</td>
      <td>-0.809889</td>
      <td>1.077737</td>
      <td>-0.752922</td>
      <td>-1.106115</td>
      <td>0.113032</td>
      <td>0.416163</td>
      <td>-1.361517</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.412482</td>
      <td>-0.487722</td>
      <td>-1.306878</td>
      <td>0</td>
      <td>-0.835284</td>
      <td>1.228577</td>
      <td>-0.511180</td>
      <td>1.077737</td>
      <td>-0.752922</td>
      <td>-1.106115</td>
      <td>0.113032</td>
      <td>0.441052</td>
      <td>-1.026501</td>
    </tr>
  </tbody>
</table>
</div>

</div>

<br />


```python
from sklearn.model_selection import train_test_split

# split dataset into training & test
X = df[numerical_columns]
y = df['CMEDV']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1)
```


```python
X_train.shape, y_train.shape
```


    ((404, 13), (404,))

<br />


```python
X_test.shape, y_test.shape
```


    ((102, 13), (102,))



  <br />

**>> 다중공선성**

회귀 분석에서 하나의 feature(예측 변수)가 다른 feature와의 상관 관계가 높으면(즉, 다중공선성이 존재하면), 회귀 분석 시 부정적인 영향을 미칠 수 있기 때문에, 모델링 하기 전에 먼저 다중공선성의 존재 여부를 확인해야합니다. 

보통 다중공선성을 판단할 때 VIF값을 확인합니다. 일반적으로, VIF > 10인 feature들은 다른 변수와의 상관관계가 높아, 다중공선성이 존재하는 것으로 판단합니다.


```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

vif = pd.DataFrame()
vif['features'] = X_train.columns
vif["VIF Factor"] = [variance_inflation_factor(X_train.values, i) for i in range(X_train.shape[1])]
vif.round(1)
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
      <th>features</th>
      <th>VIF Factor</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CRIM</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ZN</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>INDUS</td>
      <td>3.8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CHAS</td>
      <td>1.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NOX</td>
      <td>4.4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>RM</td>
      <td>1.9</td>
    </tr>
    <tr>
      <th>6</th>
      <td>AGE</td>
      <td>3.2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>DIS</td>
      <td>4.2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>RAD</td>
      <td>8.1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TAX</td>
      <td>9.8</td>
    </tr>
    <tr>
      <th>10</th>
      <td>PTRATIO</td>
      <td>1.9</td>
    </tr>
    <tr>
      <th>11</th>
      <td>B</td>
      <td>1.4</td>
    </tr>
    <tr>
      <th>12</th>
      <td>LSTAT</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>

</div>

<br />

VIF값을 확인해보면, 모든 변수의 VIF값이 다 10 이하입니다. 따라서 다중공선성 문제가 존재하지 않아 모든 feature을 활용하여 회귀 모델링을 진행하면 됩니다. 

 <br /> 

### 3-2. 회귀 모델링

먼저 Training set에서 선형 회귀 예측 모델을 학습합니다.  
그 다음 도출된 모델을 Test set에 적용해 주택 가격("CMEDV")을 예측합니다. 이 결과는 다중에 실제 "CMEDV" 값과 비교하여 모델의 예측 성능을 평가하는 데 활용하게 됩니다. 


```python
from sklearn import linear_model

# fit regression model in training set
lr = linear_model.LinearRegression()
model = lr.fit(X_train, y_train)

# predict in test set
pred_test = lr.predict(X_test)
```

<br />  

### 3-3. 모델 해석

**>> coefficients 확인하기**

먼저 각 feature의 회귀 계수를 확인해보겠습니다. 


```python
# print coef
print(lr.coef_)
```

    [-0.9479409   1.39796831  0.14786968  2.13469673 -2.25995614  2.15879342
      0.12103297 -3.23121173  2.63662665 -1.95959865 -2.05639351  0.65670428
     -3.93702535]

<br />

```python
# "feature - coefficients" DataFrame 만들기
coefs = pd.DataFrame(zip(df[numerical_columns].columns, lr.coef_), columns = ['feature', 'coefficients'])
coefs
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
      <th>feature</th>
      <th>coefficients</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CRIM</td>
      <td>-0.947941</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ZN</td>
      <td>1.397968</td>
    </tr>
    <tr>
      <th>2</th>
      <td>INDUS</td>
      <td>0.147870</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CHAS</td>
      <td>2.134697</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NOX</td>
      <td>-2.259956</td>
    </tr>
    <tr>
      <th>5</th>
      <td>RM</td>
      <td>2.158793</td>
    </tr>
    <tr>
      <th>6</th>
      <td>AGE</td>
      <td>0.121033</td>
    </tr>
    <tr>
      <th>7</th>
      <td>DIS</td>
      <td>-3.231212</td>
    </tr>
    <tr>
      <th>8</th>
      <td>RAD</td>
      <td>2.636627</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TAX</td>
      <td>-1.959599</td>
    </tr>
    <tr>
      <th>10</th>
      <td>PTRATIO</td>
      <td>-2.056394</td>
    </tr>
    <tr>
      <th>11</th>
      <td>B</td>
      <td>0.656704</td>
    </tr>
    <tr>
      <th>12</th>
      <td>LSTAT</td>
      <td>-3.937025</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
# 크기 순서로 나열
coefs_new = coefs.reindex(coefs.coefficients.abs().sort_values(ascending=False).index)
coefs_new
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
      <th>feature</th>
      <th>coefficients</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>12</th>
      <td>LSTAT</td>
      <td>-3.937025</td>
    </tr>
    <tr>
      <th>7</th>
      <td>DIS</td>
      <td>-3.231212</td>
    </tr>
    <tr>
      <th>8</th>
      <td>RAD</td>
      <td>2.636627</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NOX</td>
      <td>-2.259956</td>
    </tr>
    <tr>
      <th>5</th>
      <td>RM</td>
      <td>2.158793</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CHAS</td>
      <td>2.134697</td>
    </tr>
    <tr>
      <th>10</th>
      <td>PTRATIO</td>
      <td>-2.056394</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TAX</td>
      <td>-1.959599</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ZN</td>
      <td>1.397968</td>
    </tr>
    <tr>
      <th>0</th>
      <td>CRIM</td>
      <td>-0.947941</td>
    </tr>
    <tr>
      <th>11</th>
      <td>B</td>
      <td>0.656704</td>
    </tr>
    <tr>
      <th>2</th>
      <td>INDUS</td>
      <td>0.147870</td>
    </tr>
    <tr>
      <th>6</th>
      <td>AGE</td>
      <td>0.121033</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
## coefficients 시각화

# figure size
plt.figure(figsize = (8, 8))

# bar plot
plt.barh(coefs_new['feature'], coefs_new['coefficients'])
plt.title('"feature - coefficient" Graph')
plt.xlabel('coefficients')
plt.ylabel('features')
plt.show()
```


![png](/images/E-Python-LinearRegression-1/output_112_0.png)

<br />


**>> feature 유의성 검정**


```python
import statsmodels.api as sm

X_train2 = sm.add_constant(X_train)
model2 = sm.OLS(y_train, X_train2).fit()
model2.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>          <td>CMEDV</td>      <th>  R-squared:         </th> <td>   0.734</td> 
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.725</td> 
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   82.86</td> 
</tr>
<tr>
  <th>Date:</th>             <td>Tue, 11 Aug 2020</td> <th>  Prob (F-statistic):</th> <td>1.72e-103</td>
</tr>
<tr>
  <th>Time:</th>                 <td>00:22:07</td>     <th>  Log-Likelihood:    </th> <td> -1191.9</td> 
</tr>
<tr>
  <th>No. Observations:</th>      <td>   404</td>      <th>  AIC:               </th> <td>   2412.</td> 
</tr>
<tr>
  <th>Df Residuals:</th>          <td>   390</td>      <th>  BIC:               </th> <td>   2468.</td> 
</tr>
<tr>
  <th>Df Model:</th>              <td>    13</td>      <th>                     </th>     <td> </td>    
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>    
</tr>
</table>
<table class="simpletable">
<tr>
     <td></td>        <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>const</th>   <td>   22.4313</td> <td>    0.245</td> <td>   91.399</td> <td> 0.000</td> <td>   21.949</td> <td>   22.914</td>
</tr>
<tr>
  <th>CRIM</th>    <td>   -0.9479</td> <td>    0.290</td> <td>   -3.263</td> <td> 0.001</td> <td>   -1.519</td> <td>   -0.377</td>
</tr>
<tr>
  <th>ZN</th>      <td>    1.3980</td> <td>    0.372</td> <td>    3.758</td> <td> 0.000</td> <td>    0.667</td> <td>    2.129</td>
</tr>
<tr>
  <th>INDUS</th>   <td>    0.1479</td> <td>    0.458</td> <td>    0.323</td> <td> 0.747</td> <td>   -0.753</td> <td>    1.049</td>
</tr>
<tr>
  <th>CHAS</th>    <td>    2.1347</td> <td>    0.899</td> <td>    2.375</td> <td> 0.018</td> <td>    0.367</td> <td>    3.902</td>
</tr>
<tr>
  <th>NOX</th>     <td>   -2.2600</td> <td>    0.490</td> <td>   -4.617</td> <td> 0.000</td> <td>   -3.222</td> <td>   -1.298</td>
</tr>
<tr>
  <th>RM</th>      <td>    2.1588</td> <td>    0.332</td> <td>    6.495</td> <td> 0.000</td> <td>    1.505</td> <td>    2.812</td>
</tr>
<tr>
  <th>AGE</th>     <td>    0.1210</td> <td>    0.415</td> <td>    0.292</td> <td> 0.771</td> <td>   -0.695</td> <td>    0.937</td>
</tr>
<tr>
  <th>DIS</th>     <td>   -3.2312</td> <td>    0.477</td> <td>   -6.774</td> <td> 0.000</td> <td>   -4.169</td> <td>   -2.293</td>
</tr>
<tr>
  <th>RAD</th>     <td>    2.6366</td> <td>    0.671</td> <td>    3.931</td> <td> 0.000</td> <td>    1.318</td> <td>    3.955</td>
</tr>
<tr>
  <th>TAX</th>     <td>   -1.9596</td> <td>    0.731</td> <td>   -2.679</td> <td> 0.008</td> <td>   -3.398</td> <td>   -0.522</td>
</tr>
<tr>
  <th>PTRATIO</th> <td>   -2.0564</td> <td>    0.319</td> <td>   -6.446</td> <td> 0.000</td> <td>   -2.684</td> <td>   -1.429</td>
</tr>
<tr>
  <th>B</th>       <td>    0.6567</td> <td>    0.272</td> <td>    2.414</td> <td> 0.016</td> <td>    0.122</td> <td>    1.191</td>
</tr>
<tr>
  <th>LSTAT</th>   <td>   -3.9370</td> <td>    0.405</td> <td>   -9.723</td> <td> 0.000</td> <td>   -4.733</td> <td>   -3.141</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>169.952</td> <th>  Durbin-Watson:     </th> <td>   1.935</td> 
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td>  <th>  Jarque-Bera (JB):  </th> <td> 859.012</td> 
</tr>
<tr>
  <th>Skew:</th>          <td> 1.762</td>  <th>  Prob(JB):          </th> <td>2.94e-187</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 9.213</td>  <th>  Cond. No.          </th> <td>    10.7</td> 
</tr>
</table><br/><br/>Warnings:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
 <br />

<br />


**>> 주택 가격 영향 요소**

위 결과를 종합해 보면, 주택 가격의 영향 요소에 관하여 다음과 같은 결론들을 도출할 수 있습니다:

1. **"INDUS"**(상업적 비즈니스에 활용되지 않는 농지 면적)과 **"AGE"**(1940년 이전에 건설된 비율)은 유의하지 않습니다. (p value > 0.05)

2. **"ZN"**(25,000 제곱 피트(sq.ft) 이상의 주택지 비율),  
   **"CHAS"**(Charles 강과 접하고 있는지 여부),  
   **"RM"**(자택당 평균 방 갯수),  
   **"RAD"**(소속 도시가 Radial 고속도로와의 접근성 지수),  
   **"B"**(흑인 지수)는  
   주택 가격에 Positive한 영향을 미칩니다.  
   즉, 다른 변수의 값이 고정했을 때, 해당 변수의 값이 클수록 주택의 가격이 높을 것입니다. 

3. **"CRIM"**(지역 범죄율),   
   **"NOX"**(산화질소 농도),  
   **"DIS"**(보스턴 고용 센터와의 거리),  
   **"TAX"**(재산세),  
   **"PTRATIO"**(학생-교사 비율),  
   **"LSTAT"**(빈곤층 비율)은  
   주택 가격에 Negative한 영향을 미칩니다.  
   즉, 다른 변수의 값이 고정했을 때, 해당 변수의 값이 작을수록 주택의 가격이 높을 것입니다.

   <br />

### 3-4. 모델 예측 결과 및 성능 평가

**>> 예측 결과 시각화**

학습한 모델을 Test set에 적용하여 y값("CMEDV")을 예측합니다.  
예측 결과를 확인하기 위해 실제값과 예측값을 한 plot에 출력해 시각화해보겠습니다.


```python
# 예측 결과 시각화 (test set)
df = pd.DataFrame({'actual': y_test, 'prediction': pred_test})
df = df.sort_values(by='actual').reset_index(drop=True)

plt.figure(figsize=(12, 9))
plt.scatter(df.index, df['prediction'], marker='x', color='r')
plt.scatter(df.index, df['actual'], alpha=0.7, marker='o', color='black')
plt.title("Prediction Result in Test Set", fontsize=20)
plt.legend(['prediction', 'actual'], fontsize=12)
plt.show()
```


![png](/images/E-Python-LinearRegression-1/output_123_0.png)

<br />


**>> 모델 성능 평가**

모델의 예측 성능을 평가하기 위해 모델의 R square과 RMSE를 계산해볼게요.

* R square


```python
# R square
print(model.score(X_train, y_train))  # training set
print(model.score(X_test, y_test))  # test set
```

    0.7341832055169144
    0.7639579157366423

<br />


* RMSE


```python
# RMSE
from sklearn.metrics import mean_squared_error
from math import sqrt

# training set
pred_train = lr.predict(X_train)
print(sqrt(mean_squared_error(y_train, pred_train)))

# test set
print(sqrt(mean_squared_error(y_test, pred_test)))
```

    4.624051760840334
    4.829847098176557


Test set에서 해당 예측 모델의 R square가 0.76이고, RMSE가 4.83입니다.

<br />

<br />
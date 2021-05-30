---
title: 【실습】 Python >> Classification -- 포켓몬 분류 분석
tags:
  - Python
  - sklearn
  - Machine Learning
  - 분류
categories:
  - 【EXERCISE】
  - Python
cover: https://s1.ax1x.com/2020/08/25/dcPqB9.png
description: >-
  지도학습(Logistic Regression) -- "전설의 포켓몬" 여부 예측;  비지도학습(K-Means Clustering) --
  포켓몬 군집 분석
typora-root-url: ..
abbrlink: 3694
date: 2020-08-13 23:00:08
---

# 【Classification 실습】 -- 포켓몬 데이터셋

@[toc]

<br />

## **0. 개요**

포켓몬 데이터셋을 이용해 분류 분석을 진행합니다.

  * **지도 학습 (Logistic Regression):** "전설의 포켓몬" 여부 예측 -- "Legendary" = 0/1
  * **비지도 학습 (K-Means Clustering):** 포켓몬 군집 분석

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
warnings.filterwarnings("ignore")
```


```python
plt.rcParams['font.family'] = 'Malgun Gothic'  # 한글 깨짐 방지
```


```python
plt.rcParams['figure.figsize'] = (10, 8)  # figsize 설정
```

<br />  

**>> 사용할 데이터셋 - Pokemon Dataset**


```python
df = pd.read_csv("https://raw.githubusercontent.com/yoonkt200/FastCampusDataset/master/Pokemon.csv")
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

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>

</div>

<br />

  

**>> Feature Description**

  * Name: 포켓몬 이름
  * Type 1: 포켓몬 타입 1
  * Type 2: 포켓몬 타입 2
  * Total: 포켓몬 총 능력치 (Sum of 'HP', 'Attack', 'Defense', 'Sp.Atk', 'Sp.Def' and 'Speed')
  * HP: 포켓몬 HP 능력치
  * Attack: 포켓몬 Attack 능력치
  * Defense: 포켓몬 Defense 능력치
  * Sp.Atk: 포켓몬 Sp.Atk 능력치
  * Sp.Def: 포켓몬 Sp.Def 능력치
  * Speed: 포켓몬 Speed 능력치
  * Generation: 포켓몬 세대
  * Legendary: 전설의 포켓몬 여부

<br />  <br />

  

## **2. EDA (Exploratoty Data Analysis: 탐색적 데이터 분석)**


```python
# 그래프 배경 설정
sns.set_style('darkgrid')
```

### 2-1. 데이터셋 기본 정보 탐색

**>> 전체 데이터셋**


```python
# demension
df.shape
```


    (800, 13)

  <br />


```python
# information (data type)
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 800 entries, 0 to 799
    Data columns (total 13 columns):
     #   Column      Non-Null Count  Dtype 
    ---  ------      --------------  ----- 
     0   #           800 non-null    int64 
     1   Name        800 non-null    object
     2   Type 1      800 non-null    object
     3   Type 2      414 non-null    object
     4   Total       800 non-null    int64 
     5   HP          800 non-null    int64 
     6   Attack      800 non-null    int64 
     7   Defense     800 non-null    int64 
     8   Sp. Atk     800 non-null    int64 
     9   Sp. Def     800 non-null    int64 
     10  Speed       800 non-null    int64 
     11  Generation  800 non-null    int64 
     12  Legendary   800 non-null    bool  
    dtypes: bool(1), int64(9), object(3)
    memory usage: 75.9+ KB



<br />

```python
# 결측치
df.isnull().sum()
```


    #               0
    Name            0
    Type 1          0
    Type 2        386
    Total           0
    HP              0
    Attack          0
    Defense         0
    Sp. Atk         0
    Sp. Def         0
    Speed           0
    Generation      0
    Legendary       0
    dtype: int64



  <br />

**>> 개별 Feature 탐색**

* **분류할 목표 Feature**: "Legendary" (전설의 포켓몬 여부)


```python
# class 별 데이터 수 확인
df['Legendary'].value_counts()
```


    False    735
    True      65
    Name: Legendary, dtype: int64



 <br /> 

* "Generation" (포켓몬 세대)


```python
# 세대별 데이터 수 확인
df['Generation'].value_counts()
```


    1    166
    5    165
    3    160
    4    121
    2    106
    6     82
    Name: Generation, dtype: int64

<br />


```python
# 세대 순서로 데이터 갯수 시각화
fig = plt.figure(figsize=(8, 6))
df['Generation'].value_counts().sort_index().plot()
plt.title("'Generation 별 데이터 갯수'")
plt.show()
```


![output_34_0](/images/E-Python-Classification-1/output_34_0.png)

<br />


* "Type 1" & "Type 2" (포켓몬 타입)


```python
# unique value of "Type 1"
df['Type 1'].unique()
```


    array(['Grass', 'Fire', 'Water', 'Bug', 'Normal', 'Poison', 'Electric',
           'Ground', 'Fairy', 'Fighting', 'Psychic', 'Rock', 'Ghost', 'Ice',
           'Dragon', 'Dark', 'Steel', 'Flying'], dtype=object)

<br />


```python
# No. of unique value for "Type 1"
len(df['Type 1'].unique())
```


    18

<br />


```python
# unique value of "Type 2"  (exclude "NaN")
df[df['Type 2'].notnull()]['Type 2'].unique()
```


    array(['Poison', 'Flying', 'Dragon', 'Ground', 'Fairy', 'Grass',
           'Fighting', 'Psychic', 'Steel', 'Ice', 'Rock', 'Dark', 'Water',
           'Electric', 'Fire', 'Ghost', 'Bug', 'Normal'], dtype=object)

<br />


```python
# No. of unique value for "Type 2"
len(df[df['Type 2'].notnull()]['Type 2'].unique())
```


    18



  <br />

### 2-2. 변수(Feature) 특징 탐색

각 변수(Feature)의 분포를 관찰함으로써, 변수들의 특징을 알아보도록 하겠습니다.  

특히, 저희가 분류할 목표 Feature가 "Legendary"이므로, 각 변수의 분포를 탐색 시:  

  1. 각 항목(feature)에서 **전체 데이터의 분포** 뿐만 아닌
  2. **"Legendary"변수 class 별의 데이터 분포**도 함께 살펴볼게요.

   <br /> 

**GUIDE**  

【전체 데이터 탐색】  **&**  【"Legendary" class별 탐색】

  1. 각 능력치 분포
  2. 총 능력치 (Toal) 분포
  3. 포켓몬 타입 (Type 1 & Type 2) 분포
  4. 포켓몬 세대 (Generation) 분포

 <br /> 

#### (1) 각 능력치 분포


```python
# 전체 포켓몬의 각 능력치 분포

stats = ['HP', 'Attack', 'Defense', 'Sp. Atk', 'Sp. Def', 'Speed'] # 능력치 변수 집합
sns.boxplot(data = df[stats])
plt.title('각 능력치 분포')
plt.show()
```


![output_48_0](/images/E-Python-Classification-1/output_48_0.png)



<br />

```python
# "전설의 포켓몬" 여부에 따른 능력치 분포

fig = plt.figure(figsize=(16, 8))

plt.subplot(1,2,1)
sns.boxplot(data = df[df['Legendary']==1][stats])
plt.title('Legendary = True')

plt.subplot(1,2,2)
sns.boxplot(data = df[df['Legendary']==0][stats])
plt.title('Legendary = False')

plt.show()
```


![output_50_0](/images/E-Python-Classification-1/output_50_0.png)

 <br />

"전설의 포켓몬"은 전체적으로 더 높은 능력치를 보유하고 있으며, Attack와 Sp.Atk가 특히 높은 것으로 보입니다. 

 <br /> 

#### (2) 총 능력치 (Total) 분포


```python
# 전체 포켓몬의 총 능력치 분포

df['Total'].hist(bins=50)
plt.title('총 능력치 (Total) 분포')
plt.show()
```


![output_54_0](/images/E-Python-Classification-1/output_54_0.png)



<br />

```python
# 세대별 총 능력치 분포
sns.boxplot(data = df, x = "Generation", y="Total")
plt.title("세대별 총 능력치 분포")
plt.show()
```


![output_56_0](/images/E-Python-Classification-1/output_56_0.png)

<br />

```python
# 각 세대 "전설의 포켓몬" 여부에 따른 총 능력치 분포
sns.boxplot(data = df, x = "Generation", y="Total", hue="Legendary")
plt.title("각 세대 '전설의 포켓몬' 여부에 따른 총 능력치 분포")
plt.show()
```


![output_57_0](/images/E-Python-Classification-1/output_57_0.png)



<br />

```python
# 타입(Type 1)별 총 능력치 분포
sns.boxplot(data = df, x = 'Type 1', y = 'Total')
plt.title("타입(Type 1)별 총 능력치 분포")
plt.show()
```


![output_59_0](/images/E-Python-Classification-1/output_59_0.png)

<br />


#### (3) 포켓몬 타입 (Type 1 & Type 2) 분포


```python
# 전체 포켓몬 -- Type 1 분포

df['Type 1'].value_counts(sort=False).sort_index().plot.barh()
```


    <matplotlib.axes._subplots.AxesSubplot at 0x2e92fab51c8>




![output_62_1](/images/E-Python-Classification-1/output_62_1.png)



<br />

```python
# "전설의 포켓몬" 여부에 따른 Type 1 분포

T1_Total = pd.DataFrame(df['Type 1'].value_counts().sort_index())
T1_NotLeg = pd.DataFrame(df[df['Legendary']==0].groupby('Type 1').size())
T1_count = pd.concat([T1_Total, T1_NotLeg], axis = 1)
T1_count.columns = ['Total', 'Not Legend']
T1_count['Legend'] = T1_count['Total'] - T1_count['Not Legend']
T1_count
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
      <th>Total</th>
      <th>Not Legend</th>
      <th>Legend</th>
    </tr>
    <tr>
      <th>Type 1</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bug</th>
      <td>69</td>
      <td>69</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Dark</th>
      <td>31</td>
      <td>29</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Dragon</th>
      <td>32</td>
      <td>20</td>
      <td>12</td>
    </tr>
    <tr>
      <th>Electric</th>
      <td>44</td>
      <td>40</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Fairy</th>
      <td>17</td>
      <td>16</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Fighting</th>
      <td>27</td>
      <td>27</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Fire</th>
      <td>52</td>
      <td>47</td>
      <td>5</td>
    </tr>
    <tr>
      <th>Flying</th>
      <td>4</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Ghost</th>
      <td>32</td>
      <td>30</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Grass</th>
      <td>70</td>
      <td>67</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Ground</th>
      <td>32</td>
      <td>28</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Ice</th>
      <td>24</td>
      <td>22</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Normal</th>
      <td>98</td>
      <td>96</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Poison</th>
      <td>28</td>
      <td>28</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Psychic</th>
      <td>57</td>
      <td>43</td>
      <td>14</td>
    </tr>
    <tr>
      <th>Rock</th>
      <td>44</td>
      <td>40</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Steel</th>
      <td>27</td>
      <td>23</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Water</th>
      <td>112</td>
      <td>108</td>
      <td>4</td>
    </tr>
  </tbody>
</table>

</div>




```python
T1_count[['Not Legend', 'Legend']].plot.barh(width=0.7)
```


    <matplotlib.axes._subplots.AxesSubplot at 0x2e92ff18b88>




![output_65_1](/images/E-Python-Classification-1/output_65_1.png)



<br />

```python
# 전체 포켓몬 -- Type 2 분포

df['Type 2'].value_counts(sort=False).sort_index().plot.barh()

plt.title('"전설의 포켓몬" 여부에 따른 Type 1 분포')
plt.show()
```


![output_67_0](/images/E-Python-Classification-1/output_67_0.png)



<br />

```python
# "전설의 포켓몬" 여부에 따른 Type 2 분포

T2_Total = pd.DataFrame(df['Type 2'].value_counts().sort_index())
T2_NotLeg = pd.DataFrame(df[df['Legendary']==0].groupby('Type 2').size())
T2_count = pd.concat([T2_Total, T2_NotLeg], axis = 1)
T2_count.columns = ['Total', 'Not Legend']
T2_count['Legend'] = T2_count['Total'] - T2_count['Not Legend']
T2_count
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
      <th>Total</th>
      <th>Not Legend</th>
      <th>Legend</th>
    </tr>
    <tr>
      <th>Type 2</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bug</th>
      <td>3</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Dark</th>
      <td>20</td>
      <td>19</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Dragon</th>
      <td>18</td>
      <td>14</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Electric</th>
      <td>6</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Fairy</th>
      <td>23</td>
      <td>21</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Fighting</th>
      <td>26</td>
      <td>22</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Fire</th>
      <td>12</td>
      <td>9</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Flying</th>
      <td>97</td>
      <td>84</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Ghost</th>
      <td>14</td>
      <td>13</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Grass</th>
      <td>25</td>
      <td>25</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Ground</th>
      <td>35</td>
      <td>34</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Ice</th>
      <td>14</td>
      <td>11</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Normal</th>
      <td>4</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Poison</th>
      <td>34</td>
      <td>34</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Psychic</th>
      <td>33</td>
      <td>28</td>
      <td>5</td>
    </tr>
    <tr>
      <th>Rock</th>
      <td>14</td>
      <td>14</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Steel</th>
      <td>22</td>
      <td>21</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Water</th>
      <td>14</td>
      <td>13</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
T2_count[['Not Legend', 'Legend']].plot.barh(width=0.7)

plt.title('"전설의 포켓몬" 여부에 따른 Type 2 분포')
plt.show()
```


![output_70_0](/images/E-Python-Classification-1/output_70_0.png)

<br />


#### (4) 포켓몬 세대(Generation) 분포


```python
# 전체 포켓몬 -- 세대 분포

df['Generation'].value_counts().sort_index().plot.bar()
```


    <matplotlib.axes._subplots.AxesSubplot at 0x2e930887d08>




![output_73_1](/images/E-Python-Classification-1/output_73_1.png)

<br />



```python
# "전설의 포켓몬" 여부에 따른 세대 분포

gene_Leg = pd.DataFrame(df[df['Legendary']==1].groupby('Generation').size())
gene_NotLeg = pd.DataFrame(df[df['Legendary']==0].groupby('Generation').size())
gene_count = pd.concat([gene_Leg, gene_NotLeg], axis=1)
gene_count.columns = ['Legend', 'Not Legend']
gene_count
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
      <th>Legend</th>
      <th>Not Legend</th>
    </tr>
    <tr>
      <th>Generation</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>160</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>101</td>
    </tr>
    <tr>
      <th>3</th>
      <td>18</td>
      <td>142</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13</td>
      <td>108</td>
    </tr>
    <tr>
      <th>5</th>
      <td>15</td>
      <td>150</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>74</td>
    </tr>
  </tbody>
</table>

</div>




```python
gene_count.plot.bar()
plt.title('"전설의 포켓몬" 여부에 따른 세대 분포')
plt.show()
```


![output_76_0](/images/E-Python-Classification-1/output_76_0.png)

<br />

<br />


## **3. 지도 학습 기반 분류 분석 -- Logistic Regression**

### 3-1. 데이터 전처리

#### (1) 데이터 타입 변경


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

<table >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 800 entries, 0 to 799
    Data columns (total 13 columns):
     #   Column      Non-Null Count  Dtype 
    ---  ------      --------------  ----- 
     0   #           800 non-null    int64 
     1   Name        800 non-null    object
     2   Type 1      800 non-null    object
     3   Type 2      414 non-null    object
     4   Total       800 non-null    int64 
     5   HP          800 non-null    int64 
     6   Attack      800 non-null    int64 
     7   Defense     800 non-null    int64 
     8   Sp. Atk     800 non-null    int64 
     9   Sp. Def     800 non-null    int64 
     10  Speed       800 non-null    int64 
     11  Generation  800 non-null    int64 
     12  Legendary   800 non-null    bool  
    dtypes: bool(1), int64(9), object(3)
    memory usage: 75.9+ KB

<br />


* 분류예측 목표 Feature인 "Lengendary"의 값은 현재 "True"/"False"로 구성되어있습니다. 예측 모델에 적용하기 위해 "1"/"0"으로 바꾸겠습니다.

* 포켓몬의 세대를 나타나는 Feature인 "Generation"의 타입은 지금 "int"로 되어있지만, Feature의 의미상 해당 숫자는 분류 역할을 하고 있으므로 "str"타입으로 변환시키겠습니다.

* 분류 예측 시 이름 데이터가 예측에 도움이 없으므로 "Name"을 빼고 데이터셋을 제구성하겠습니다.

  <br />


```python
df['Legendary'] = df['Legendary'].astype(int)
df['Generation'] = df['Generation'].astype(str)
preprocessed_df = df[['Type 1', 'Type 2', 'Total', 'HP', 'Attack', 'Defense', 
                      'Sp. Atk', 'Sp. Def', 'Speed', 'Generation', 'Legendary']]
preprocessed_df.head()
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
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

#### (2) One-Hot Encoding

Categorical Variable에 대해서 dummy화 작업을 진행하겠습니다.  

* 1 data one-label: One-hot Encoding

* 1 data multi-label: Multi-label Encoding

  <br />

**>> 타입 (Type) -- Multi-label Encoding**

* 먼저 Type 1과 Type 2를 하나의 변수(Type)로 묶는다.
* 그 다음 1~2개의 label를 가진 Type변수에 대해서 Multi-label Encoding을 진행한다.


```python
# pokemon type list 생성
def make_list(x1, x2):
    type_list = []
    type_list.append(x1)
    if x2 is not np.nan:
        type_list.append(x2)
    return type_list

preprocessed_df['Type'] = preprocessed_df.apply(lambda x: make_list(x['Type 1'], x['Type 2']), axis=1)
preprocessed_df.head()                                    
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
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>0</td>
      <td>[Grass, Poison]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>0</td>
      <td>[Grass, Poison]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>0</td>
      <td>[Grass, Poison]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>0</td>
      <td>[Grass, Poison]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>0</td>
      <td>[Fire]</td>
    </tr>
  </tbody>
</table>

</div>




```python
del preprocessed_df['Type 1']
del preprocessed_df['Type 2']
preprocessed_df.head()
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
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>0</td>
      <td>[Grass, Poison]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>0</td>
      <td>[Grass, Poison]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>0</td>
      <td>[Grass, Poison]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>0</td>
      <td>[Grass, Poison]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>0</td>
      <td>[Fire]</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
# multi-lacel encoding
from sklearn.preprocessing import MultiLabelBinarizer

ml = MultiLabelBinarizer()
preprocessed_df = preprocessed_df.join(pd.DataFrame(ml.fit_transform(preprocessed_df.pop('Type')),
                                                    columns = ml.classes_))
```

> * [[pandas.DataFrame.join]](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.join.html): Join columns of another DataFrame
> * [[pandas.DataFrame.pop (*item*) ]](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.pop.html): Return item and drop from frame


```python
preprocessed_df.head()
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
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Bug</th>
      <th>...</th>
      <th>Ghost</th>
      <th>Grass</th>
      <th>Ground</th>
      <th>Ice</th>
      <th>Normal</th>
      <th>Poison</th>
      <th>Psychic</th>
      <th>Rock</th>
      <th>Steel</th>
      <th>Water</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 27 columns</p>
</div>

</div>



 <br /> 

**>> 세대 (Generation) -- One-hot Encoding**


```python
# apply one-hot encoding to 'Generation'
preprocessed_df = pd.get_dummies(preprocessed_df)  # df name입력하면 str var를 자동 식별하여 encoding 진행함
# preprocessed_ddf = pd.get_dummies(preprocessed_df['Generation'])  # 작업할 var 지정
preprocessed_df.head()
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
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Legendary</th>
      <th>Bug</th>
      <th>Dark</th>
      <th>...</th>
      <th>Psychic</th>
      <th>Rock</th>
      <th>Steel</th>
      <th>Water</th>
      <th>Generation_1</th>
      <th>Generation_2</th>
      <th>Generation_3</th>
      <th>Generation_4</th>
      <th>Generation_5</th>
      <th>Generation_6</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 32 columns</p>
</div>

</div>



<br />  

#### (3) Feature 포준화

Numerical Feature간의 Scale차이를 없애기 위해 feature 표준화를 진행합니다.


```python
preprocessed_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 800 entries, 0 to 799
    Data columns (total 32 columns):
     #   Column        Non-Null Count  Dtype
    ---  ------        --------------  -----
     0   Total         800 non-null    int64
     1   HP            800 non-null    int64
     2   Attack        800 non-null    int64
     3   Defense       800 non-null    int64
     4   Sp. Atk       800 non-null    int64
     5   Sp. Def       800 non-null    int64
     6   Speed         800 non-null    int64
     7   Legendary     800 non-null    int32
     8   Bug           800 non-null    int32
     9   Dark          800 non-null    int32
     10  Dragon        800 non-null    int32
     11  Electric      800 non-null    int32
     12  Fairy         800 non-null    int32
     13  Fighting      800 non-null    int32
     14  Fire          800 non-null    int32
     15  Flying        800 non-null    int32
     16  Ghost         800 non-null    int32
     17  Grass         800 non-null    int32
     18  Ground        800 non-null    int32
     19  Ice           800 non-null    int32
     20  Normal        800 non-null    int32
     21  Poison        800 non-null    int32
     22  Psychic       800 non-null    int32
     23  Rock          800 non-null    int32
     24  Steel         800 non-null    int32
     25  Water         800 non-null    int32
     26  Generation_1  800 non-null    uint8
     27  Generation_2  800 non-null    uint8
     28  Generation_3  800 non-null    uint8
     29  Generation_4  800 non-null    uint8
     30  Generation_5  800 non-null    uint8
     31  Generation_6  800 non-null    uint8
    dtypes: int32(19), int64(7), uint8(6)
    memory usage: 107.9 KB



```python
from sklearn.preprocessing import StandardScaler

# feature standardization
scaler = StandardScaler()
scale_columns = ['Total', 'HP', 'Attack', 'Defense', 'Sp. Atk', 'Sp. Def', 'Speed']
preprocessed_df[scale_columns] = scaler.fit_transform(preprocessed_df[scale_columns])
preprocessed_df.head()
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
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Legendary</th>
      <th>Bug</th>
      <th>Dark</th>
      <th>...</th>
      <th>Psychic</th>
      <th>Rock</th>
      <th>Steel</th>
      <th>Water</th>
      <th>Generation_1</th>
      <th>Generation_2</th>
      <th>Generation_3</th>
      <th>Generation_4</th>
      <th>Generation_5</th>
      <th>Generation_6</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.976765</td>
      <td>-0.950626</td>
      <td>-0.924906</td>
      <td>-0.797154</td>
      <td>-0.239130</td>
      <td>-0.248189</td>
      <td>-0.801503</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.251088</td>
      <td>-0.362822</td>
      <td>-0.524130</td>
      <td>-0.347917</td>
      <td>0.219560</td>
      <td>0.291156</td>
      <td>-0.285015</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.749845</td>
      <td>0.420917</td>
      <td>0.092448</td>
      <td>0.293849</td>
      <td>0.831146</td>
      <td>1.010283</td>
      <td>0.403635</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.583957</td>
      <td>0.420917</td>
      <td>0.647369</td>
      <td>1.577381</td>
      <td>1.503891</td>
      <td>1.729409</td>
      <td>0.403635</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.051836</td>
      <td>-1.185748</td>
      <td>-0.832419</td>
      <td>-0.989683</td>
      <td>-0.392027</td>
      <td>-0.787533</td>
      <td>-0.112853</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 32 columns</p>
</div>

</div>



 <br /> 

#### (4) Training set / Test set 나누기


```python
from sklearn.model_selection import train_test_split

X = preprocessed_df.loc[:, preprocessed_df.columns != 'Legendary']
y = preprocessed_df['Legendary']
x_train, x_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=1)
```


```python
x_train.shape, y_train.shape
```


    ((600, 31), (600,))




```python
x_test.shape, y_test.shape
```


    ((200, 31), (200,))



  

 <br /> 

### 3-2. Logistic Regression 모델 학습

#### (1) 모델 학습


```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

# Fit in Training set
logit = LogisticRegression(random_state=0)
logit.fit(x_train, y_train)

# Predict in Test set
y_pred = logit.predict(x_test)
```

  <br />

#### (2) 모델 평가


```python
# classification result for test set

print("accuracy: %.2f" % accuracy_score(y_test, y_pred))
print("Precision: %.3f" % precision_score(y_test, y_pred))
print("Recall: %.3f" % recall_score(y_test, y_pred))
print("F1: %.3f" % f1_score(y_test, y_pred))
```

    accuracy: 0.93
    Precision: 0.615
    Recall: 0.471
    F1: 0.533

<br />


위 모델 평가 결과를 확인해보면, 해당 모델은 **정확도(accuracy) 만** 높고, 정밀도(Precision), 재현율(Recall), F1 score 등 모두 낮습니다. 이는 학습 데이터의 **클래스 불균형으로 인한 정확도 함정** 문제일 가능성이 높습니다. (참고: [[Python >> sklearn - (2) 분류] 4-2. !!정확도 함정!!](https://hyemin-kim.github.io/2020/07/26/S-Python-sklearn2/#4-2-%EC%A0%95%ED%99%95%EB%8F%84-accuracy))  

추가 확인을 위해 Confusion Matrix를 출력해 봅니다.

  <br />


```python
np.set_printoptions(suppress=True)
```


```python
from sklearn.metrics import confusion_matrix

# print confusion matrix
confu = confusion_matrix(y_true = y_test, y_pred = y_pred)

plt.figure(figsize=(4, 3))
sns.heatmap(confu, annot=True, annot_kws={'size':15}, cmap='OrRd', fmt='.10g')
plt.title('Confusion Matrix')
plt.show()
```


![output_122_0](/images/E-Python-Classification-1/output_122_0.png)


Positive Condition ( _"Legendary" = True/1_ ) <17> 대비 Negative Condition ( _"Legendary" = False/0_ ) <183>인 케이스가 훨씬 많다는 것을 볼 수 있습니다. 따라서, 클래스 불균형으로 인한 정확도 함정 문제가 맞으며, **클래스 불균형을 조정**한 후 다시 학습 시키도록 하겠습니다.

<br />  

### 3-3. 클래스 불균형 조정


```python
preprocessed_df['Legendary'].value_counts()
```


    0    735
    1     65
    Name: Legendary, dtype: int64



<br />  

**>> 1:1 샘플링**

Positive Condition 케이스와 Negative Condition 케이스를 1:1비율로 샘플링 합니다.


```python
positive_random_idx = preprocessed_df[preprocessed_df['Legendary']==1].sample(65, random_state=12).index.tolist()
negative_random_idx = preprocessed_df[preprocessed_df['Legendary']==0].sample(65, random_state=12).index.tolist()
```

  <br />

**>> Training set / Test set 나누기**


```python
random_idx = positive_random_idx + negative_random_idx
X = preprocessed_df.loc[random_idx, preprocessed_df.columns != 'Legendary']
y = preprocessed_df['Legendary'][random_idx]
x_train, x_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=1)
```


```python
x_train.shape, y_train.shape
```


    ((97, 31), (97,))




```python
x_test.shape, y_test.shape
```


    ((33, 31), (33,))



<br />  

**>> 모델 재학습**


```python
# Fit in Training set
logit2 = LogisticRegression(random_state=0)
logit2.fit(x_train, y_train)

# Predict in Test set
y_pred2 = logit2.predict(x_test)
```

  <br />

**>> 모델 재평가**


```python
# clssification result for test set

print("accuracy: %.2f" % accuracy_score(y_test, y_pred2))
print("Precision: %.3f" % precision_score(y_test, y_pred2))
print("Recall: %.3f" % recall_score(y_test, y_pred2))
print("F1: %.3f" % f1_score(y_test, y_pred2))
```

    accuracy: 1.00
    Precision: 1.000
    Recall: 1.000
    F1: 1.000



<br />

```python
# confusion matrix

confu2 = confusion_matrix(y_true=y_test, y_pred = y_pred2)

plt.figure(figsize=(4, 3))
sns.heatmap(confu2, annot=True, annot_kws={'size':15}, cmap='OrRd', fmt='.10g')
plt.title('Confusion Matrix')
plt.show()
```


![output_143_0](/images/E-Python-Classification-1/output_143_0.png)




클래스 불균형을 조정한 후, 새롭게 학습된 모델의 performance가 많이 좋아졌습니다.

<br />  <br />

  

## **4. 비지도 학습 기반 군집 분석 -- K-Means Clustering**

### 4-1. K-Means 군집 분석

#### (1) 2차원 군집 분석 


```python
from sklearn.cluster import KMeans

# K-means train & Elbow method
X = preprocessed_df[['Attack', 'Defense']]

k_list = []
cost_list = []
for k in range (1, 8):
    kmeans = KMeans(n_clusters=k).fit(X)
    interia = kmeans.inertia_  # inertia: Sum of squared distances of samples to their closest cluster center.
    print("k:", k, "| cost:", interia)
    k_list.append(k)
    cost_list.append(interia)

plt.figure(figsize=(8, 6))
plt.plot(k_list, cost_list)
```

    k: 1 | cost: 1600.0
    k: 2 | cost: 853.3477298974242
    k: 3 | cost: 642.3911470107209
    k: 4 | cost: 480.49450250321513
    k: 5 | cost: 403.97191765107124
    k: 6 | cost: 343.98696660525184
    k: 7 | cost: 295.56093457429847



    [<matplotlib.lines.Line2D at 0x2e930467c48>]




![output_151_2](/images/E-Python-Classification-1/output_151_2.png)

<br />

추세를 봤을 때, 4 clusters가 제일 적당한 것으로 보입니다.  

따라서, cluster를 4로 지정한 후 다시 학습시킨 뒤, 각 데이터가 분류된 cluster 결과를 원 데이터셋에 추가합니다.

<br />


```python
# k-means fitting and predict
kmeans = KMeans(n_clusters=4).fit(X)
cluster_num = pd.Series(kmeans.predict(X))
preprocessed_df['cluster_num'] = cluster_num.values
preprocessed_df.head()
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
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Legendary</th>
      <th>Bug</th>
      <th>Dark</th>
      <th>...</th>
      <th>Rock</th>
      <th>Steel</th>
      <th>Water</th>
      <th>Generation_1</th>
      <th>Generation_2</th>
      <th>Generation_3</th>
      <th>Generation_4</th>
      <th>Generation_5</th>
      <th>Generation_6</th>
      <th>cluster_num</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.976765</td>
      <td>-0.950626</td>
      <td>-0.924906</td>
      <td>-0.797154</td>
      <td>-0.239130</td>
      <td>-0.248189</td>
      <td>-0.801503</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.251088</td>
      <td>-0.362822</td>
      <td>-0.524130</td>
      <td>-0.347917</td>
      <td>0.219560</td>
      <td>0.291156</td>
      <td>-0.285015</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.749845</td>
      <td>0.420917</td>
      <td>0.092448</td>
      <td>0.293849</td>
      <td>0.831146</td>
      <td>1.010283</td>
      <td>0.403635</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.583957</td>
      <td>0.420917</td>
      <td>0.647369</td>
      <td>1.577381</td>
      <td>1.503891</td>
      <td>1.729409</td>
      <td>0.403635</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.051836</td>
      <td>-1.185748</td>
      <td>-0.832419</td>
      <td>-0.989683</td>
      <td>-0.392027</td>
      <td>-0.787533</td>
      <td>-0.112853</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 33 columns</p>
</div>

</div>




```python
print(preprocessed_df['cluster_num'].value_counts())
```

    2    309
    0    253
    3    128
    1    110
    Name: cluster_num, dtype: int64

<br />


**>> 군집 시각화**


```python
# Visualization

plt.scatter(preprocessed_df[preprocessed_df['cluster_num'] == 0]['Attack'],
            preprocessed_df[preprocessed_df['cluster_num'] == 0]['Defense'],
            s = 50, c = 'red', alpha = 0.5, label = 'Pokemon Group 1')
plt.scatter(preprocessed_df[preprocessed_df['cluster_num'] == 1]['Attack'],
            preprocessed_df[preprocessed_df['cluster_num'] == 1]['Defense'],
            s = 50, c = 'green', alpha = 0.7, label = 'Pokemon Group 2')
plt.scatter(preprocessed_df[preprocessed_df['cluster_num'] == 2]['Attack'],
            preprocessed_df[preprocessed_df['cluster_num'] == 2]['Defense'],
            s = 50, c = 'blue', alpha = 0.5, label = 'Pokemon Group 3')
plt.scatter(preprocessed_df[preprocessed_df['cluster_num'] == 3]['Attack'],
            preprocessed_df[preprocessed_df['cluster_num'] == 3]['Defense'],
            s = 50, c = 'yellow', alpha = 0.8, label = 'Pokemon Group 4')

plt.title('Pokemon Cluster by "Attack" & "Defense"')
plt.xlabel('Attack')
plt.ylabel('Defense')
plt.legend()
plt.show()
```


![output_157_0](/images/E-Python-Classification-1/output_157_0.png)

<br />


#### (2) 다차원 군집 분석


```python
from sklearn.cluster import KMeans

# K-Means train & Elbow method
X = preprocessed_df[['HP', 'Attack', 'Defense', 'Sp. Atk', 'Sp. Def', 'Speed']]

k_list = []
cost_list = []
for k in range (1, 15):
    kmeans = KMeans(n_clusters=k).fit(X)
    interia = kmeans.inertia_  # inertia: Sum of squared distances of samples to their closest cluster center.
    print("k:", k, "| cost:", interia)
    k_list.append(k)
    cost_list.append(interia)

plt.figure(figsize=(8, 6))
plt.plot(k_list, cost_list)
```

    k: 1 | cost: 4800.0
    k: 2 | cost: 3275.3812330305977
    k: 3 | cost: 2862.057922495397
    k: 4 | cost: 2566.5807792995274
    k: 5 | cost: 2328.0706840275643
    k: 6 | cost: 2182.759972635841
    k: 7 | cost: 2070.734327066247
    k: 8 | cost: 1957.5240844927844
    k: 9 | cost: 1854.3770148227836
    k: 10 | cost: 1778.3178764912984
    k: 11 | cost: 1721.845255688537
    k: 12 | cost: 1644.3967658442484
    k: 13 | cost: 1579.4938049394318
    k: 14 | cost: 1536.785887021493



    [<matplotlib.lines.Line2D at 0x2e930efbb88>]




![output_160_2](/images/E-Python-Classification-1/output_160_2.png)

<br />

이 경우에는 cluster가 5일 때가 제일 적당해 보입니다.


```python
# k-means fitting and predict
kmeans = KMeans(n_clusters=5).fit(X)
cluster_num = pd.Series(kmeans.predict(X))
preprocessed_df['cluster_num'] = cluster_num.values
preprocessed_df.head()
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
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Legendary</th>
      <th>Bug</th>
      <th>Dark</th>
      <th>...</th>
      <th>Rock</th>
      <th>Steel</th>
      <th>Water</th>
      <th>Generation_1</th>
      <th>Generation_2</th>
      <th>Generation_3</th>
      <th>Generation_4</th>
      <th>Generation_5</th>
      <th>Generation_6</th>
      <th>cluster_num</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.976765</td>
      <td>-0.950626</td>
      <td>-0.924906</td>
      <td>-0.797154</td>
      <td>-0.239130</td>
      <td>-0.248189</td>
      <td>-0.801503</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.251088</td>
      <td>-0.362822</td>
      <td>-0.524130</td>
      <td>-0.347917</td>
      <td>0.219560</td>
      <td>0.291156</td>
      <td>-0.285015</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.749845</td>
      <td>0.420917</td>
      <td>0.092448</td>
      <td>0.293849</td>
      <td>0.831146</td>
      <td>1.010283</td>
      <td>0.403635</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.583957</td>
      <td>0.420917</td>
      <td>0.647369</td>
      <td>1.577381</td>
      <td>1.503891</td>
      <td>1.729409</td>
      <td>0.403635</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.051836</td>
      <td>-1.185748</td>
      <td>-0.832419</td>
      <td>-0.989683</td>
      <td>-0.392027</td>
      <td>-0.787533</td>
      <td>-0.112853</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 33 columns</p>
</div>

</div>



<br />  

**>> 군집별 특성 시각화**

2차원이 아니기 때문에 위와 같이 군집 결과를 시각화하기 어렵습니다.  

군집화 결과를 확인하기 위해 **각 Feature의 군집별 특성**을 시각화하도록 하겠습니다.

  <br />


```python
# HP
sns.boxplot(x = "cluster_num", y = "HP", data = preprocessed_df)
plt.title('군집별 "HP" 분포')
plt.show()
```


![output_167_0](/images/E-Python-Classification-1/output_167_0.png)



<br />

```python
# Attack
sns.boxplot(x = 'cluster_num', y = 'Attack', data = preprocessed_df)
plt.title('군집별 "Attack" 분포')
plt.show()
```


![output_169_0](/images/E-Python-Classification-1/output_169_0.png)



<br />

```python
# Defense
sns.boxplot(x = 'cluster_num', y = 'Defense', data = preprocessed_df)
plt.title('군집별 "Defense" 분포')
plt.show()
```


![output_171_0](/images/E-Python-Classification-1/output_171_0.png)



<br />

```python
# Sp. Atk
sns.boxplot(x = 'cluster_num', y = 'Sp. Atk', data = preprocessed_df)
plt.title('군집별 "Sp. Atk" 분포')
plt.show()
```


![output_173_0](/images/E-Python-Classification-1/output_173_0.png)



<br />

```python
# Sp. Def
sns.boxplot(x = 'cluster_num', y = 'Sp. Def', data = preprocessed_df)
plt.title('군집별 "Sp. Def" 분포')
plt.show()
```


![output_175_0](/images/E-Python-Classification-1/output_175_0.png)



<br />

```python
# Speed
sns.boxplot(x = 'cluster_num', y = 'Speed', data = preprocessed_df)
plt.title('군집별 "Speed" 분포')
plt.show()
```


![output_177_0](/images/E-Python-Classification-1/output_177_0.png)

<br />

<br />
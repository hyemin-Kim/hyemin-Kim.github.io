---
title: Python >> sklearn - (1) 전처리
tags:
  - Python
  - sklearn
  - Machine Learning
  - 전처리
categories:
  - 【STUDY - Python】
  - Python - Machine Learning
cover: 'https://ohiing.com/wp-content/uploads/2020/02/scikit-learn-2.jpg'
abbrlink: 54817
date: 2020-07-17 16:37:50
---

# **전처리 (Pre-Processing)**

  @[toc]

<br/>

## **개요**

### 1. 전처리의 정의

**데이터 전처리**는 데이터 분석에 적합하게 데이터를 **가공/ 변경/ 처리/ 클리닝**하는 과정이다

  <br/>

### 2. 전처리의 종류

1. **결측치** - Imputer

2. **이상치**

3. **정규화 (Normalization)**
   - 0~1사이의 분포로 조정
   - <font size=4>$x_{new} = \frac{x-x_{min}}{x_{max}-x_{min}}$</font>  

4. **표준화 (Standardization)**
   - 평균을 0, 표준편차를 1로 맞춤
   - <font size=4>$x_{new} = \frac{x-\mu}{\sigma}$</font>  

5. **샘플링 (over/under sampling)**

6. **피처 공학 (Feature Engineering)**
   - feature 생성/ 연산
   - 구간 생성, 스케일 변경

<br/>  <br/>

  

## **실습 -- Titanic**


```python
import numpy as np
import pandas as pd
```


```python
train = pd.read_csv('train.csv')
test = pd.read_csv('test.csv')
```

  <br/>

### 0. 데이터 셋 파악


```python
train.head()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>

</div>

<br/>

  

* PassengerId: 승객 아이디

* Survived: 생존 여부, 1: 생존, 0: 사망

* Pclass: 등급

* Name: 성함

* Sex: 성별

* Age: 나이

* SibSp: 형제, 자매, 배우자 수

* Parch: 부모, 자식 수

* Ticket: 티켓번호

* Fare: 요즘

* Cabin: 좌석번호

* Embarked: 탑승 항구

  <br/>
  
  <br/>

### 1. train / validation 셋 나누기

**STEP 1. feature & label 정의하기**


```python
feature = [
    'Pclass', 'Sex', 'Age', 'Fare'
]
```


```python
label = [
    'Survived'
]
```


```python
train[feature].head()
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
      <th>Pclass</th>
      <th>Sex</th>
      <th>Age</th>
      <th>Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>7.2500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>71.2833</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>7.9250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>53.1000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>8.0500</td>
    </tr>
  </tbody>
</table>

</div>

<br/>


```python
train[label].head()
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
      <th>Survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
    </tr>
  </tbody>
</table>

</div>

<br/>

  

**STEP 2. 적절한 비율로 train / validation set 나누기**


```python
from sklearn.model_selection import train_test_split
```

> ***reference:*** [< train_test_split > Document](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html)

> **train_test_split** ( *X, y, test_size=.., random_state=.., shuffle=True* )
>
> * **test_size:** validation set에 할당할 비율 (20% -> 0.2)
> * **random_state:** random seed 설정
> * **shuffle:** 기본 True: shuffle the data before splitting

<br/>

```python
x_train, x_valid, y_train, y_valid = train_test_split(train[feature], train[label], test_size=0.2, random_state=30, shuffle=True)
```


```python
x_train.shape, y_train.shape
```


    ((712, 4), (712, 1))

<br/>


```python
x_valid.shape, y_valid.shape
```


    ((179, 4), (179, 1))



 <br/> <br/>

  

### 2. 결측치 처리

#### 2-0. 결측치 확인

**방법 1.** pandas의 ```info()```


```python
train.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 12 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   PassengerId  891 non-null    int64  
     1   Survived     891 non-null    int64  
     2   Pclass       891 non-null    int64  
     3   Name         891 non-null    object 
     4   Sex          891 non-null    object 
     5   Age          714 non-null    float64
     6   SibSp        891 non-null    int64  
     7   Parch        891 non-null    int64  
     8   Ticket       891 non-null    object 
     9   Fare         891 non-null    float64
     10  Cabin        204 non-null    object 
     11  Embarked     889 non-null    object 
    dtypes: float64(2), int64(5), object(5)
    memory usage: 83.7+ KB

<br/>


**방법 2.** pandas의 ```isnull()```  
합계를 구하는 sum()을 통해 한 눈에 확인할 수 있다


```python
train.isnull().sum()
```


    PassengerId      0
    Survived         0
    Pclass           0
    Name             0
    Sex              0
    Age            177
    SibSp            0
    Parch            0
    Ticket           0
    Fare             0
    Cabin          687
    Embarked         2
    dtype: int64

  







개별 column의 결측치 확인하기


```python
train['Age'].isnull().sum()
```


    177



<br/>  

#### 2-1. Numerical Column의 결측치 처리


```python
train.head()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>

</div>

<br/>


```python
train.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 12 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   PassengerId  891 non-null    int64  
     1   Survived     891 non-null    int64  
     2   Pclass       891 non-null    int64  
     3   Name         891 non-null    object 
     4   Sex          891 non-null    object 
     5   Age          714 non-null    float64
     6   SibSp        891 non-null    int64  
     7   Parch        891 non-null    int64  
     8   Ticket       891 non-null    object 
     9   Fare         891 non-null    float64
     10  Cabin        204 non-null    object 
     11  Embarked     889 non-null    object 
    dtypes: float64(2), int64(5), object(5)
    memory usage: 83.7+ KB

<br/>


**1. Pandas의 <font color='blue'>"fillna()"</font>를 사용**: 1개의 column을 처리할 때

**a. 숫자"0"으로 채우기**


```python
train['Age'].fillna(0).describe()
```


    count    891.000000
    mean      23.799293
    std       17.596074
    min        0.000000
    25%        6.000000
    50%       24.000000
    75%       35.000000
    max       80.000000
    Name: Age, dtype: float64



 <br/> 

**b. 통계값(평균)으로 채우기**


```python
train['Age'].fillna(train['Age'].mean()).describe()
```


    count    891.000000
    mean      29.699118
    std       13.002015
    min        0.420000
    25%       22.000000
    50%       29.699118
    75%       35.000000
    max       80.000000
    Name: Age, dtype: float64



 <br/> 

**2. sklearn의 <font color='blue'>"SimpleImputer"</font>를 사용**: 2개 이상의 column을 한 번에 처리할 때

> ***reference:***  
>
> 1. [Impute 도큐먼트](https://scikit-learn.org/stable/modules/impute.html)  
> 2. [SimplrImputer 도큐먼트](https://scikit-learn.org/stable/modules/generated/sklearn.impute.SimpleImputer.html)

> **SimpleImputer**( _*, missing_values=nan, strategy='mean', fill_value=None, verbose=0, copy=True, add_indicator=False_ )
>
> * strategy: "mean" / "median" / "most_frequent" / "constant"

<br/>

```python
from sklearn.impute import SimpleImputer
```

  <br/>

**a. 숫자"0"으로 채우기**


```python
# STEP 1. imputer 만들기
imputer = SimpleImputer(strategy='constant', fill_value=0)
```


```python
# STEP 2. fit() 을 통해 결측치에 대한 학습을 진행하기
imputer.fit(train[['Age', 'Pclass']])
```


    SimpleImputer(add_indicator=False, copy=True, fill_value=0, missing_values=nan,
                  strategy='constant', verbose=0)


```python
# STEP 3. transform() 을 통해 실제 결측치에 대해 처리하기
result = imputer.transform(train[['Age', 'Pclass']])
result
```


    array([[22.,  3.],
           [38.,  1.],
           [26.,  3.],
           ...,
           [ 0.,  3.],
           [26.,  1.],
           [32.,  3.]])


```python
# STEP 4. 처리 결과를 original data에 대입
train[['Age', 'Pclass']] = result
```


```python
train[['Age', 'Pclass']].isnull().sum()
```


    Age       0
    Pclass    0
    dtype: int64



<br/>  

**fit_transform()** 은 fit()과 transform()을 한 번에 해주는 합수다.


```python
train = pd.read_csv('train.csv')
```


```python
train[['Age', 'Pclass']].isnull().sum()
```


    Age       177
    Pclass      0
    dtype: int64

<br/>


```python
# STEP 1. imputer 만들기
imputer = SimpleImputer(strategy='constant', fill_value=0)
```


```python
# STEP 2. fit and transform
result = imputer.fit_transform(train[['Age', 'Pclass']])
```


```python
# STEP 3. 결과 대입
train[['Age', 'Pclass']] = result
```


```python
train[['Age', 'Pclass']].isnull().sum()
```


    Age       0
    Pclass    0
    dtype: int64


```python
train[['Age', 'Pclass']].describe()
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
      <th>Age</th>
      <th>Pclass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>891.000000</td>
      <td>891.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>23.799293</td>
      <td>2.308642</td>
    </tr>
    <tr>
      <th>std</th>
      <td>17.596074</td>
      <td>0.836071</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>24.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>35.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>80.000000</td>
      <td>3.000000</td>
    </tr>
  </tbody>
</table>

</div>



 <br/> 

**b. 통계값(평균)으로 채우기**


```python
train = pd.read_csv('train.csv')
```


```python
train[['Age', 'Pclass']].isnull().sum()
```


    Age       177
    Pclass      0
    dtype: int64

<br/>


```python
imputer = SimpleImputer(strategy='mean')
result = imputer.fit_transform(train[['Age', 'Pclass']])
train[['Age', 'Pclass']] = result
```


```python
train[['Age', 'Pclass']].isnull().sum()
```


    Age       0
    Pclass    0
    dtype: int64


```python
train[['Age', 'Pclass']].describe()
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
      <th>Age</th>
      <th>Pclass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>891.000000</td>
      <td>891.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>29.699118</td>
      <td>2.308642</td>
    </tr>
    <tr>
      <th>std</th>
      <td>13.002015</td>
      <td>0.836071</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.420000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>22.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>29.699118</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>35.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>80.000000</td>
      <td>3.000000</td>
    </tr>
  </tbody>
</table>

</div>

<br/>

  

#### 2-2. Categorical Column의 결측치 처리


```python
train = pd.read_csv('train.csv')
```


```python
train.head()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>

</div>

<br/>


```python
train.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 12 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   PassengerId  891 non-null    int64  
     1   Survived     891 non-null    int64  
     2   Pclass       891 non-null    int64  
     3   Name         891 non-null    object 
     4   Sex          891 non-null    object 
     5   Age          714 non-null    float64
     6   SibSp        891 non-null    int64  
     7   Parch        891 non-null    int64  
     8   Ticket       891 non-null    object 
     9   Fare         891 non-null    float64
     10  Cabin        204 non-null    object 
     11  Embarked     889 non-null    object 
    dtypes: float64(2), int64(5), object(5)
    memory usage: 83.7+ KB

<br/>


**1. Pandas의 <font color='blue'>"fillna()"</font>를 사용**: 1개의 column을 처리할 때


```python
train['Embarked'].fillna('S')
```


    0      S
    1      C
    2      S
    3      S
    4      S
          ..
    886    S
    887    S
    888    S
    889    C
    890    Q
    Name: Embarked, Length: 891, dtype: object

<br/>

  

**2. sklearn의 <font color='blue'>"SimpleImputer"</font>를 사용**: 2개 이상의 column을 한 번에 처리할 때


```python
imputer = SimpleImputer(strategy = 'most_frequent')
result = imputer.fit_transform(train[['Embarked', 'Cabin']])
train[['Embarked', 'Cabin']] = result
```


```python
train[['Embarked', 'Cabin']].isnull().sum()
```


    Embarked    0
    Cabin       0
    dtype: int64



<br/>  <br/>

  

### 3. Label Encoding: 문자(categorivcal)를 수치(numerical)로 변환

기계학습을 위해서 모든 **문자**로된 데이터는 **수치로 변환**해야 한다


```python
train = pd.read_csv('train.csv')
train.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 12 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   PassengerId  891 non-null    int64  
     1   Survived     891 non-null    int64  
     2   Pclass       891 non-null    int64  
     3   Name         891 non-null    object 
     4   Sex          891 non-null    object 
     5   Age          714 non-null    float64
     6   SibSp        891 non-null    int64  
     7   Parch        891 non-null    int64  
     8   Ticket       891 non-null    object 
     9   Fare         891 non-null    float64
     10  Cabin        204 non-null    object 
     11  Embarked     889 non-null    object 
    dtypes: float64(2), int64(5), object(5)
    memory usage: 83.7+ KB

<br/>

```python
train['Sex']  
```


    0        male
    1      female
    2      female
    3      female
    4        male
            ...  
    886      male
    887    female
    888    female
    889      male
    890      male
    Name: Sex, Length: 891, dtype: object

<br/>

  

**방법 1: convert함수를 직접 정의하기**


```python
train['Sex'].value_counts()
```


    male      577
    female    314
    Name: Sex, dtype: int64

<br/>


```python
# STEP 1. 함수 정의
def convert(data):
    if data == 'female':
        return 1
    elif data == 'male':
        return 0
```


```python
# STEP 2. 함수 apply
train['Sex'].apply(convert)
```


    0      0
    1      1
    2      1
    3      1
    4      0
          ..
    886    0
    887    1
    888    1
    889    0
    890    0
    Name: Sex, Length: 891, dtype: int64



  <br/>

**방법 2: sklearn의 <font color='blue'>"LabelEncoder"</font> 사용**

* 변환 규칙: value name의 **alphabet 순서대로** 0, 1, 2... 숫자를 부여


```python
from sklearn.preprocessing import LabelEncoder
```


```python
train['Sex'].value_counts()
```


    male      577
    female    314
    Name: Sex, dtype: int64

<br/>


```python
le = LabelEncoder()
```


```python
train['Sex_num'] = le.fit_transform(train['Sex'])
```


```python
train['Sex_num'].value_counts()
```


    1    577
    0    314
    Name: Sex_num, dtype: int64

<br/>


```python
# class 확인
le.classes_
```


    array(['female', 'male'], dtype=object)

<br/>


```python
# 숫자 -> 문자
le.inverse_transform([0, 1, 1, 0, 0, 1, 1])
```


    array(['female', 'male', 'male', 'female', 'female', 'male', 'male'],
          dtype=object)



<br/>  

NaN 값이 포함되어 있으면, ```LabeEncoder```가 정상 동작하지 않음


```python
train['Embarked']
```


    0      S
    1      C
    2      S
    3      S
    4      S
          ..
    886    S
    887    S
    888    S
    889    C
    890    Q
    Name: Embarked, Length: 891, dtype: object

<br/>


```python
train['Embarked'].value_counts()
```


    S    644
    C    168
    Q     77
    Name: Embarked, dtype: int64

<br/>


```python
le.fit_transform(train['Embarked'])
```


    ---------------------------------------------------------------------------
    
    TypeError                                 Traceback (most recent call last)
    
    D:\Anaconda\lib\site-packages\sklearn\preprocessing\_label.py in _encode(values, uniques, encode, check_unknown)
        111         try:
    --> 112             res = _encode_python(values, uniques, encode)
        113         except TypeError:


    D:\Anaconda\lib\site-packages\sklearn\preprocessing\_label.py in _encode_python(values, uniques, encode)
         59     if uniques is None:
    ---> 60         uniques = sorted(set(values))
         61         uniques = np.array(uniques, dtype=values.dtype)


    TypeError: '<' not supported between instances of 'float' and 'str'


​    

    During handling of the above exception, another exception occurred:


    TypeError                                 Traceback (most recent call last)
    
    <ipython-input-38-86525b1fc929> in <module>
    ----> 1 le.fit_transform(train['Embarked'])


    D:\Anaconda\lib\site-packages\sklearn\preprocessing\_label.py in fit_transform(self, y)
        250         """
        251         y = column_or_1d(y, warn=True)
    --> 252         self.classes_, y = _encode(y, encode=True)
        253         return y
        254 


    D:\Anaconda\lib\site-packages\sklearn\preprocessing\_label.py in _encode(values, uniques, encode, check_unknown)
        112             res = _encode_python(values, uniques, encode)
        113         except TypeError:
    --> 114             raise TypeError("argument must be a string or number")
        115         return res
        116     else:


    TypeError: argument must be a string or number

<br/>

```python
train['Embarked'] = train['Embarked'].fillna('S')
```


```python
train['Embarked'] = le.fit_transform(train['Embarked'])
```


```python
train['Embarked']
```


    0      2
    1      0
    2      2
    3      2
    4      2
          ..
    886    2
    887    2
    888    2
    889    0
    890    1
    Name: Embarked, Length: 891, dtype: int32

<br/>


```python
train['Embarked'].value_counts()
```


    2    646
    0    168
    1     77
    Name: Embarked, dtype: int64



  <br/>

  <br/>

### 4. 원 핫 인코딩 (One Hot Encoding)

> **pd.get_dummies** ( *df_name* [ *'col_name'* ] )


```python
train = pd.read_csv('train.csv')
```


```python
train.head()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>


</div>

<br/>


```python
train.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 12 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   PassengerId  891 non-null    int64  
     1   Survived     891 non-null    int64  
     2   Pclass       891 non-null    int64  
     3   Name         891 non-null    object 
     4   Sex          891 non-null    object 
     5   Age          714 non-null    float64
     6   SibSp        891 non-null    int64  
     7   Parch        891 non-null    int64  
     8   Ticket       891 non-null    object 
     9   Fare         891 non-null    float64
     10  Cabin        204 non-null    object 
     11  Embarked     889 non-null    object 
    dtypes: float64(2), int64(5), object(5)
    memory usage: 83.7+ KB

<br/>

**"Embarked"를 살펴보기**


```python
# Unique Value 확인하기
train['Embarked'].value_counts()
```


    S    644
    C    168
    Q     77
    Name: Embarked, dtype: int64

<br/>


```python
# NA 채우기
train['Embarked'] = train['Embarked'].fillna('S')
train['Embarked'].value_counts()
```


    S    646
    C    168
    Q     77
    Name: Embarked, dtype: int64

<br/>


```python
# Label Encoding (문자 to 숫자)
train['Embarked_num'] = LabelEncoder().fit_transform(train['Embarked'])
train['Embarked_num'].value_counts()
```


    2    646
    0    168
    1     77
    Name: Embarked_num, dtype: int64

<br/>

  

Embarked는 탑승 항구의 이니셜을 나타낸다. 우리는 ```LabelEncoder```를 통해서 값을 수치형으로 변환해주었다, 하지만 이대로 데이터를 기계학습 시키면, 기계는 데이터 안에서 관계를 학습한다.

예를 들면, 'S'= 2, 'Q'= 1 이라고 되어 있는데, ```Q```+```Q```=```S```가 된다라고 학습해버린다

그렇기 때문에, 우리는 <font color='blue'>각 unique value를 별도의 column으로 분리하고, 값에 해당하는 column는 **True (1)**, 나머지 column는 **False (0)** 를 갖게 한다</font>.이것이 바로 **원 핫 인코딩** 이다.

<br/>


```python
train['Embarked'][:6]
```


    0    S
    1    C
    2    S
    3    S
    4    S
    5    Q
    Name: Embarked, dtype: object

<br/>


```python
train['Embarked_num'][:6]
```


    0    2
    1    0
    2    2
    3    2
    4    2
    5    1
    Name: Embarked_num, dtype: int32

<br/>


```python
one_hot = pd.get_dummies(train['Embarked_num'][:6])
one_hot
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

</div>

<br/>


```python
one_hot.columns = ['C', 'Q', 'S']
one_hot
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
      <th>C</th>
      <th>Q</th>
      <th>S</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

</div>

<br/>

**원핫인코딩**은 카테고리의 특성을(계절, 항구, 성별, 종류...) 가지는 column에 대해서 적용한다

<br/>  <br/>

  

### 5. Normalize (정규화)

**정규화:** column간에 다른 min,max 값을 가지는 경우, 정규화를 통해 min / max 의 척도를 맞추어 주는 작업이다

> sklearn.preprocessing  -->  MinMaxScaler()

  <br/>

**예: 영화평점**  

* 네이버 영화평점 (0점 ~ 10점): [2, 4, 6, 8, 10]
* 넷플릭스 영화평점 (0점 ~ 5점): [1, 2, 3, 4, 5]


```python
movie = {'naver': [2, 4, 6, 8, 10],
         'netflix': [1, 2, 3, 4, 5]
        }
```


```python
movie = pd.DataFrame(data=movie)
movie
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
      <th>naver</th>
      <th>netflix</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>5</td>
    </tr>
  </tbody>
</table>

</div>

<br/>


```python
from sklearn.preprocessing import MinMaxScaler
```


```python
min_max_scaler = MinMaxScaler()
```


```python
min_max_movie = min_max_scaler.fit_transform(movie)
```


```python
pd.DataFrame(min_max_movie, columns = ['naver', 'netfllix'])
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
      <th>naver</th>
      <th>netfllix</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.25</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.50</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.75</td>
      <td>0.75</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>

</div>

<br/>

  <br/>

  

### 6. Standard Scaling (표준화)

**표준화:** 평균이 0, 표준편차가 1이 되도록 변환해주는 작업

> sklearn.preprocessing  -->  StandardScaler()


```python
from sklearn.preprocessing import StandardScaler
standard_scaler = StandardScaler()
```


```python
# 샘플데이터 생성
x = np.arange(10)
x[9] = 1000   # oulier 추가
```

```python
x.mean(), x.std()
```

    (103.6, 298.8100399919654)

<br/>

```python
# 원본 데이터 표준화하기
scaled = standard_scaler.fit_transform(x.reshape(-1, 1))
```


```python
scaled.mean(), scaled.std()
```


    (4.4408920985006264e-17, 1.0)

<br/>


```python
round(scaled.mean(), 2), scaled.std()  # mean값 반올림
```


    (0.0, 1.0)

<br/>

<br/>
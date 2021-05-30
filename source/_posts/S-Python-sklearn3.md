---
title: Python >> sklearn - (3) 회귀 (Regression)
tags:
  - Python
  - sklearn
  - Machine Learning
  - 회귀
categories:
  - 【STUDY - Python】
  - Python - Machine Learning
cover: 'https://ohiing.com/wp-content/uploads/2020/02/scikit-learn-2.jpg'
description: 'Linear Regression, Ridge, LASSO, ElasticNet, Scaling, Polynomial Features'
typora-root-url: ..
abbrlink: 6570
date: 2020-07-29 18:53:05
---

# 회귀 (Regression) 예측

@[toc]

<br/>

> [[Supervised Learning] Document](https://scikit-learn.org/stable/supervised_learning.html#supervised-learning)

**특성:** 수치형 값을 예측 (Y의 값이 연속형 수치로 표현)  

**예시:**

* 주택 가격 예측

* 매출앵 예측

  <br/>

## **0. 데이터 셋**


```python
import pandas as pd
import numpy as np

np.set_printoptions(suppress=True) # If True, print floating point numbers instead of scientific notation
```


```python
from sklearn.datasets import load_boston
```

[[Boston Dataset](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_boston.html#sklearn.datasets.load_boston)]

 <br/> 

### 0-1. 데이터 로드


```python
data = load_boston()
```


```python
print(data['DESCR'])  # data description
```

    .. _boston_dataset:
    
    Boston house prices dataset
    ---------------------------
    
    **Data Set Characteristics:**  
    
        :Number of Instances: 506 
    
        :Number of Attributes: 13 numeric/categorical predictive. Median Value (attribute 14) is usually the target.
    
        :Attribute Information (in order):
            - CRIM     per capita crime rate by town
            - ZN       proportion of residential land zoned for lots over 25,000 sq.ft.
            - INDUS    proportion of non-retail business acres per town
            - CHAS     Charles River dummy variable (= 1 if tract bounds river; 0 otherwise)
            - NOX      nitric oxides concentration (parts per 10 million)
            - RM       average number of rooms per dwelling
            - AGE      proportion of owner-occupied units built prior to 1940
            - DIS      weighted distances to five Boston employment centres
            - RAD      index of accessibility to radial highways
            - TAX      full-value property-tax rate per $10,000
            - PTRATIO  pupil-teacher ratio by town
            - B        1000(Bk - 0.63)^2 where Bk is the proportion of blacks by town
            - LSTAT    % lower status of the population
            - MEDV     Median value of owner-occupied homes in $1000's
    
        :Missing Attribute Values: None
    
        :Creator: Harrison, D. and Rubinfeld, D.L.
    
    This is a copy of UCI ML housing dataset.
    https://archive.ics.uci.edu/ml/machine-learning-databases/housing/


​    

    This dataset was taken from the StatLib library which is maintained at Carnegie Mellon University.
    
    The Boston house-price data of Harrison, D. and Rubinfeld, D.L. 'Hedonic
    prices and the demand for clean air', J. Environ. Economics & Management,
    vol.5, 81-102, 1978.   Used in Belsley, Kuh & Welsch, 'Regression diagnostics
    ...', Wiley, 1980.   N.B. Various transformations are used in the table on
    pages 244-261 of the latter.
    
    The Boston house-price data has been used in many machine learning papers that address regression
    problems.   
         
    .. topic:: References
    
       - Belsley, Kuh & Welsch, 'Regression diagnostics: Identifying Influential Data and Sources of Collinearity', Wiley, 1980. 244-261.
       - Quinlan,R. (1993). Combining Instance-Based and Model-Based Learning. In Proceedings on the Tenth International Conference of Machine Learning, 236-243, University of Massachusetts, Amherst. Morgan Kaufmann.


​    

  <br/>

### 0-2. 데이터프레임 만들기


```python
# step 1. features (X)
# data['data'] - feature data; data['feature_names'] - feature column names

df = pd.DataFrame(data['data'], columns = data['feature_names'])

# step 2. target (y) 추가 
df['MEDV'] = data['target']
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

<table  >
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
      <th>MEDV</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.00632</td>
      <td>18.0</td>
      <td>2.31</td>
      <td>0.0</td>
      <td>0.538</td>
      <td>6.575</td>
      <td>65.2</td>
      <td>4.0900</td>
      <td>1.0</td>
      <td>296.0</td>
      <td>15.3</td>
      <td>396.90</td>
      <td>4.98</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.02731</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0.0</td>
      <td>0.469</td>
      <td>6.421</td>
      <td>78.9</td>
      <td>4.9671</td>
      <td>2.0</td>
      <td>242.0</td>
      <td>17.8</td>
      <td>396.90</td>
      <td>9.14</td>
      <td>21.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.02729</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0.0</td>
      <td>0.469</td>
      <td>7.185</td>
      <td>61.1</td>
      <td>4.9671</td>
      <td>2.0</td>
      <td>242.0</td>
      <td>17.8</td>
      <td>392.83</td>
      <td>4.03</td>
      <td>34.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.03237</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0.0</td>
      <td>0.458</td>
      <td>6.998</td>
      <td>45.8</td>
      <td>6.0622</td>
      <td>3.0</td>
      <td>222.0</td>
      <td>18.7</td>
      <td>394.63</td>
      <td>2.94</td>
      <td>33.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.06905</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0.0</td>
      <td>0.458</td>
      <td>7.147</td>
      <td>54.2</td>
      <td>6.0622</td>
      <td>3.0</td>
      <td>222.0</td>
      <td>18.7</td>
      <td>396.90</td>
      <td>5.33</td>
      <td>36.2</td>
    </tr>
  </tbody>
</table>

</div>



<br/>  

**컬럼 소게** (feature 13 + target 1):

* **CRIM**: 범죄율

* **ZN**: 25,000 square feet 당 주거용 토지의 비율

* **INDUS**: 비소매(non-retail) 비즈니스 면적 비율

* **CHAS**: 찰스 강 더미 변수 (통로가 하천을 향하면 1; 그렇지 않으면 0)

* **NOX**: 산화 질소 농도 (천만 분의 1)

* **RM**:주거 당 평균 객실 수

* **AGE**: 1940 년 이전에 건축된 자가 소유 점유 비율

* **DIS**: 5 개의 보스턴 고용 센터까지의 가중 거리     

* **RAD**: 고속도로 접근성 지수

* **TAX**: 10,000 달러 당 전체 가치 재산 세율

* **PTRATIO**  도시 별 학생-교사 비율

* **B**: 1000 (Bk-0.63) ^ 2 여기서 Bk는 도시 별 검정 비율입니다.

* **LSTAT**: 인구의 낮은 지위

* **MEDV**: 자가 주택의 중앙값 (1,000 달러 단위)

  <br/>

  <br/>

## **1. Training set / Test set 나누기**


```python
from sklearn.model_selection import train_test_split
```


```python
x_train, x_test, y_train, y_test = train_test_split(df.drop('MEDV', 1), df['MEDV'], random_state=23)
```


```python
x_train.shape, y_train.shape
```


    ((379, 13), (379,))




```python
x_test.shape, y_test.shape
```


    ((127, 13), (127,))




```python
x_train.head()
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
      <th>112</th>
      <td>0.12329</td>
      <td>0.0</td>
      <td>10.01</td>
      <td>0.0</td>
      <td>0.547</td>
      <td>5.913</td>
      <td>92.9</td>
      <td>2.3534</td>
      <td>6.0</td>
      <td>432.0</td>
      <td>17.8</td>
      <td>394.95</td>
      <td>16.21</td>
    </tr>
    <tr>
      <th>301</th>
      <td>0.03537</td>
      <td>34.0</td>
      <td>6.09</td>
      <td>0.0</td>
      <td>0.433</td>
      <td>6.590</td>
      <td>40.4</td>
      <td>5.4917</td>
      <td>7.0</td>
      <td>329.0</td>
      <td>16.1</td>
      <td>395.75</td>
      <td>9.50</td>
    </tr>
    <tr>
      <th>401</th>
      <td>14.23620</td>
      <td>0.0</td>
      <td>18.10</td>
      <td>0.0</td>
      <td>0.693</td>
      <td>6.343</td>
      <td>100.0</td>
      <td>1.5741</td>
      <td>24.0</td>
      <td>666.0</td>
      <td>20.2</td>
      <td>396.90</td>
      <td>20.32</td>
    </tr>
    <tr>
      <th>177</th>
      <td>0.05425</td>
      <td>0.0</td>
      <td>4.05</td>
      <td>0.0</td>
      <td>0.510</td>
      <td>6.315</td>
      <td>73.4</td>
      <td>3.3175</td>
      <td>5.0</td>
      <td>296.0</td>
      <td>16.6</td>
      <td>395.60</td>
      <td>6.29</td>
    </tr>
    <tr>
      <th>69</th>
      <td>0.12816</td>
      <td>12.5</td>
      <td>6.07</td>
      <td>0.0</td>
      <td>0.409</td>
      <td>5.885</td>
      <td>33.0</td>
      <td>6.4980</td>
      <td>4.0</td>
      <td>345.0</td>
      <td>18.9</td>
      <td>396.90</td>
      <td>8.79</td>
    </tr>
  </tbody>
</table>

</div>




```python
y_train.head()
```


    112    18.8
    301    22.0
    401     7.2
    177    24.6
    69     20.9
    Name: MEDV, dtype: float64

<br/>

  <br/>

  

## **2. 평가 지표 만들기**

### 2-1. 평가 지표 계산식

**(1) MAE (Mean Absolute Error)**

MAE (평균 절대 오차): 에측값과 실제값의 차이의 **절대값**에 대하여 평균을 낸 것  

$$MAE = \frac{1}{n} \sum_{i=1}^n \left\vert y_i - \widehat{y_i} \right\vert$$

**(2) MSE (Mean Squared Error)**

MSE (평균 제곱 오차): 예측값과 실제값의 차이의 **제곱**에 대하여 평균을 낸 것  

$$MSE = \frac{1}{n} \sum_{i=1}^n \left( y_i - \widehat{y_i} \right)^2$$

**(3) RMSE (Root Mean Squared Error)**

RMSE (평균 제곱근 오차): 예측값과 실제값의 차이의 **제곱**에 대하여 평균을 낸 뒤 **루트**를 씌운 것  

$$ RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^n \left( y_i - \widehat{y_i} \right)^2}$$

  <br/>

### 2-2. 코딩으로 평가 지표 만들어 보기


```python
import numpy as np
```


```python
actual = np.array([1, 2, 3])
pred = np.array([3, 4, 5])
```


```python
# MAE
def my_mae(actual, pred):
    return np.abs(actual - pred).mean()

my_mae(actual, pred)
```


    2.0




```python
# MSE
def my_mse(actual, pred):
    return ((actual - pred)**2).mean()

my_mse(actual, pred)
```


    4.0




```python
# RMSE
def my_rmse(actual, pred):
    return np.sqrt(my_mse(actual, pred))

my_rmse(actual, pred)
```


    2.0



<br/>  

### 2-3. sklearn의 평가 지표 활용하기


```python
from sklearn.metrics import mean_absolute_error, mean_squared_error
```

> [[sklearn.metrics.**mean_absolute_error**]](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.mean_absolute_error.html)
> [[sklearn.metrics.**mean_squared_error**]](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.mean_squared_error.html)


```python
# MAE (my_mae VS sklearn_mae)
my_mae(actual, pred), mean_absolute_error(actual, pred)
```


    (2.0, 2.0)




```python
# MSE (my_mse VS sklearn_mse)
my_mse(actual, pred), mean_squared_error(actual, pred)
```


    (4.0, 4.0)



 <br/> 

### 2-4. 모델 성능 확인을 위한 함수


```python
import matplotlib.pyplot as plt
import seaborn as sns

my_predictions = {}

colors = ['r', 'c', 'm', 'y', 'k', 'khaki', 'teal', 'orchid', 'sandybrown',
          'greenyellow', 'dodgerblue', 'deepskyblue', 'rosybrown', 'firebrick',
          'deeppink', 'crimson', 'salmon', 'darkred', 'olivedrab', 'olive', 
          'forestgreen', 'royalblue', 'indigo', 'navy', 'mediumpurple', 'chocolate',
          'gold', 'darkorange', 'seagreen', 'turquoise', 'steelblue', 'slategray', 
          'peru', 'midnightblue', 'slateblue', 'dimgray', 'cadetblue', 'tomato'
         ]

# prediction plot
def plot_predictions(name_, actual, pred):
    df = pd.DataFrame({'actual': y_test, 'prediction': pred})
    df = df.sort_values(by='actual').reset_index(drop=True)

    plt.figure(figsize=(12, 9))
    plt.scatter(df.index, df['prediction'], marker='x', color='r')
    plt.scatter(df.index, df['actual'], alpha=0.7, marker='o', color='black')
    plt.title(name_, fontsize=15)
    plt.legend(['prediction', 'actual'], fontsize=12)
    plt.show()

# evaluation plot
def mse_eval(name_, actual, pred):
    global predictions
    global colors

    plot_predictions(name_, actual, pred)

    mse = mean_squared_error(actual, pred)
    my_predictions[name_] = mse

    y_value = sorted(my_predictions.items(), key=lambda x: x[1], reverse=True)
    
    df = pd.DataFrame(y_value, columns=['model', 'mse'])
    print(df)
    min_ = df['mse'].min() - 10
    max_ = df['mse'].max() + 10
    
    length = len(df)
    
    plt.figure(figsize=(10, length))
    ax = plt.subplot()
    ax.set_yticks(np.arange(len(df)))
    ax.set_yticklabels(df['model'], fontsize=15)
    bars = ax.barh(np.arange(len(df)), df['mse'])
    
    for i, v in enumerate(df['mse']):
        idx = np.random.choice(len(colors))
        bars[i].set_color(colors[idx])
        ax.text(v + 2, i, str(round(v, 3)), color='k', fontsize=15, fontweight='bold')
        
    plt.title('MSE Error', fontsize=18)
    plt.xlim(min_, max_)
    
    plt.show()

# remove model
def remove_model(name_):
    global my_predictions
    try:
        del my_predictions[name_]
    except KeyError:
        return False
    return True
```

  <br/>

  <br/>

## **3. 회귀 알고리즘**

### 3-1. Linear Regression

[[sklearn.linear_model.**LinearRegression**] Document](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)


```python
from sklearn.linear_model import LinearRegression
```


```python
model = LinearRegression(n_jobs=-1)  # n_jobs: CPU코어의 사용
model.fit(x_train, y_train)
pred = model.predict(x_test)
```


```python
mse_eval('LinearRegression', y_test, pred)
```


![output_59_0](/images/S-Python-sklearn3/output_59_0.png)


                  model        mse
    0  LinearRegression  22.770784



![output_59_2](/images/S-Python-sklearn3/output_59_2.png)

<br/>


### 3-2. Ridge & LASSO & ElasticNet

#### (1) 개념

[참고](https://medium.com/mighty-data-science-bootcamp/linear-regression-ridge-lasso-elastic-net-fb8115c0a635)

**규제(Regularization):** 학습이 과적합 되는 것을 방지하고자 일종의 **penalty**를 부여하는 것.  
[원리] penalty를 부여하여 가중치($\beta$)를 축소함으로써 학습 모델의 예측 variance를 감소 시키는 것

<br/>

**>> L2 규제 & Ridge (릿지)**

* **L2 규제 (L2 Regularization):**  각 <font color='blue'>가중치 제곱의 합</font>에 규제 강도 (Regularization Strength) $\lambda$ 를 곱한다  

  $$L2 \ 규제 = \lambda \sum_{j=1}^p \beta_j^2 = \lambda\  \lVert \beta \rVert_2^2$$
  $$l_2 \ norm:  \lVert \beta \rVert_2 = \sqrt{\sum_{j=1}^p \beta_j^2}$$  


* **Ridge:** Loss Function에 L2 규제를 더한 값을 최소화 시키는 것  

  $$\min_{\beta_j} \ \left[ \sum_{i=1}^n \left( y_i-\beta_0-\sum_{j=1}^p\beta_jx_{ij} \right) + \lambda\ \sum_{j=1}^p\beta_j^2 \right]= \min_{\beta_j} \ \left[ RSS + \lambda\ \sum_{j=1}^p\beta_j^2 \right]$$  

* $\lambda$ 를 크게 하면 가중치($\beta$) 가 더 많이 감소되고(규제를 중요시 함), $\lambda$ 를 작게 하면 가중치($\beta$) 가 증가한다(규제를 중요시하지 않음)

  <br/>

**>> L1 규제 & LASSO (라쏘)**

* **L1 규제 (L1 Regularization):** 각 <font color='blue'>가중치 절대값의 합</font>에 규제 강도 (Regularization Strength) $\lambda$ 를 곱한다  

  $$L1\ 규제 = \lambda \sum_{j=1}^p \left| \beta_j \right| = \lambda \ \lVert \beta \rVert_1$$
  $$l1\ norm: \lVert \beta \rVert_1 = \sum_{j=1}^p \left| \beta_j \right|$$      

* **LASSO:** Loss Function에 L1 규제를 더한 값을 최소화 시키는 것  

  $$\min_{\beta_j} \ \left[ \sum_{i=1}^n \left( y_i-\beta_0-\sum_{j=1}^p\beta_jx_{ij} \right) + \lambda \sum_{j=1}^p \left| \beta_j \right| \right]= \min_{\beta_j} \ \left[ RSS + \lambda \sum_{j=1}^p \left| \beta_j \right| \right]$$  


* 어떤 가중치($\beta$) 는 실제로 0이 된다. 즉, 모델에서 완전히 제외되는 특성이 생기는 것이다

  <br/>

**>> ElasticNet**  

**l1_ratio (default=0.5)**  

* l1_ratio = 0 (L2 규제만 사용)  

* l1_ratio = 1 (L1 규제만 사용)  

* 0 < l1_ratio <1 (L1 and L2 규제 혼합사용)

  <br/>

#### (2) 실습

**>> Ridge**   [[Document]](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Ridge.html)


```python
from sklearn.linear_model import Ridge
```

* **예측 결과 확인**


```python
# lambda (규제강도) 범위 설정
alphas = [100, 10, 1, 0.1, 0.01, 0.001]

# 모델 학습
for alpha in alphas:
    ridge = Ridge(alpha = alpha)
    ridge.fit(x_train, y_train)
    ridge_pred = ridge.predict(x_test)
    mse_eval('Ridge(alpha={})'.format(alpha), y_test, ridge_pred)
```


![output_75_0](/images/S-Python-sklearn3/output_75_0.png)


                  model        mse
    0  Ridge(alpha=100)  23.487453
    1  LinearRegression  22.770784



![output_75_2](/images/S-Python-sklearn3/output_75_2.png)



![output_75_3](/images/S-Python-sklearn3/output_75_3.png)


                  model        mse
    0  Ridge(alpha=100)  23.487453
    1   Ridge(alpha=10)  22.793119
    2  LinearRegression  22.770784



![output_75_5](/images/S-Python-sklearn3/output_75_5.png)



![output_75_6](/images/S-Python-sklearn3/output_75_6.png)


                  model        mse
    0  Ridge(alpha=100)  23.487453
    1   Ridge(alpha=10)  22.793119
    2  LinearRegression  22.770784
    3    Ridge(alpha=1)  22.690411



![output_75_8](/images/S-Python-sklearn3/output_75_8.png)



![output_75_9](/images/S-Python-sklearn3/output_75_9.png)


                  model        mse
    0  Ridge(alpha=100)  23.487453
    1   Ridge(alpha=10)  22.793119
    2  LinearRegression  22.770784
    3  Ridge(alpha=0.1)  22.718126
    4    Ridge(alpha=1)  22.690411



![output_75_11](/images/S-Python-sklearn3/output_75_11.png)



![output_75_12](/images/S-Python-sklearn3/output_75_12.png)


                   model        mse
    0   Ridge(alpha=100)  23.487453
    1    Ridge(alpha=10)  22.793119
    2   LinearRegression  22.770784
    3  Ridge(alpha=0.01)  22.764254
    4   Ridge(alpha=0.1)  22.718126
    5     Ridge(alpha=1)  22.690411



![output_75_14](/images/S-Python-sklearn3/output_75_14.png)



![output_75_15](/images/S-Python-sklearn3/output_75_15.png)


                    model        mse
    0    Ridge(alpha=100)  23.487453
    1     Ridge(alpha=10)  22.793119
    2    LinearRegression  22.770784
    3  Ridge(alpha=0.001)  22.770117
    4   Ridge(alpha=0.01)  22.764254
    5    Ridge(alpha=0.1)  22.718126
    6      Ridge(alpha=1)  22.690411



![output_75_17](/images/S-Python-sklearn3/output_75_17.png)

<br/>


* **coefficents 값 확인**


```python
x_train.columns
```


    Index(['CRIM', 'ZN', 'INDUS', 'CHAS', 'NOX', 'RM', 'AGE', 'DIS', 'RAD', 'TAX',
           'PTRATIO', 'B', 'LSTAT'],
          dtype='object')




```python
ridge.coef_  # for the last alpha in 'alphas' 
```


    array([ -0.09608448,   0.04753482,   0.0259022 ,   3.24479273,
           -18.89579975,   4.06725732,   0.0020486 ,  -1.46883742,
             0.28149275,  -0.0094656 ,  -0.87454099,   0.01240815,
            -0.52406249])




```python
# coefficients visulization

def plot_coef(columns, coef):
    coef_df = pd.DataFrame(list(zip(columns, coef)))
    coef_df.columns=['feature', 'coef']
    coef_df = coef_df.sort_values('coef', ascending=False).reset_index(drop=True)
    
    fig, ax = plt.subplots(figsize=(9, 7))
    ax.barh(np.arange(len(coef_df)), coef_df['coef'])
    idx = np.arange(len(coef_df))
    ax.set_yticks(idx)
    ax.set_yticklabels(coef_df['feature'])
    fig.tight_layout()
    plt.show()
```


```python
plot_coef(x_train.columns, ridge.coef_)   # alpha = 0.001
```


![output_81_0](/images/S-Python-sklearn3/output_81_0.png)

<br/>


* **alpha 값에 따른 coef의 차이**


```python
ridge_1 = Ridge(alpha=1)
ridge_1.fit(x_train, y_train)
ridge_pred_1 = ridge_1.predict(x_test)

ridge_100 = Ridge(alpha=100)
ridge_100.fit(x_train, y_train)
ridge_pred_100 = ridge_100.predict(x_test)
```


```python
plot_coef(x_train.columns, ridge_1.coef_)   # alpha = 1
```


![output_85_0](/images/S-Python-sklearn3/output_85_0.png)



```python
plot_coef(x_train.columns, ridge_100.coef_)   # alpha = 100
```


![output_86_0](/images/S-Python-sklearn3/output_86_0.png)



<br/>


**>> LASSO** [[Document]](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Lasso.html)


```python
from sklearn.linear_model import Lasso
```

* **예측 결과 확인**


```python
# lambda (규제강도) 범위 설정
alphas = [100, 10, 1, 0.1, 0.01, 0.001]

# 모델 학습
for alpha in alphas:
    lasso = Lasso(alpha=alpha)
    lasso.fit(x_train, y_train)
    lasso_pred = lasso.predict(x_test)
    mse_eval('Lasso(alpha={})'.format(alpha), y_test, lasso_pred)
```


![output_92_0](/images/S-Python-sklearn3/output_92_0.png)


                    model        mse
    0    Lasso(alpha=100)  63.348818
    1    Ridge(alpha=100)  23.487453
    2     Ridge(alpha=10)  22.793119
    3    LinearRegression  22.770784
    4  Ridge(alpha=0.001)  22.770117
    5   Ridge(alpha=0.01)  22.764254
    6    Ridge(alpha=0.1)  22.718126
    7      Ridge(alpha=1)  22.690411



![output_92_2](/images/S-Python-sklearn3/output_92_2.png)



![output_92_3](/images/S-Python-sklearn3/output_92_3.png)


                    model        mse
    0    Lasso(alpha=100)  63.348818
    1     Lasso(alpha=10)  42.436622
    2    Ridge(alpha=100)  23.487453
    3     Ridge(alpha=10)  22.793119
    4    LinearRegression  22.770784
    5  Ridge(alpha=0.001)  22.770117
    6   Ridge(alpha=0.01)  22.764254
    7    Ridge(alpha=0.1)  22.718126
    8      Ridge(alpha=1)  22.690411



![output_92_5](/images/S-Python-sklearn3/output_92_5.png)



![output_92_6](/images/S-Python-sklearn3/output_92_6.png)


                    model        mse
    0    Lasso(alpha=100)  63.348818
    1     Lasso(alpha=10)  42.436622
    2      Lasso(alpha=1)  27.493672
    3    Ridge(alpha=100)  23.487453
    4     Ridge(alpha=10)  22.793119
    5    LinearRegression  22.770784
    6  Ridge(alpha=0.001)  22.770117
    7   Ridge(alpha=0.01)  22.764254
    8    Ridge(alpha=0.1)  22.718126
    9      Ridge(alpha=1)  22.690411



![output_92_8](/images/S-Python-sklearn3/output_92_8.png)



![output_92_9](/images/S-Python-sklearn3/output_92_9.png)


                     model        mse
    0     Lasso(alpha=100)  63.348818
    1      Lasso(alpha=10)  42.436622
    2       Lasso(alpha=1)  27.493672
    3     Ridge(alpha=100)  23.487453
    4     Lasso(alpha=0.1)  22.979708
    5      Ridge(alpha=10)  22.793119
    6     LinearRegression  22.770784
    7   Ridge(alpha=0.001)  22.770117
    8    Ridge(alpha=0.01)  22.764254
    9     Ridge(alpha=0.1)  22.718126
    10      Ridge(alpha=1)  22.690411



![output_92_11](/images/S-Python-sklearn3/output_92_11.png)



![output_92_12](/images/S-Python-sklearn3/output_92_12.png)


                     model        mse
    0     Lasso(alpha=100)  63.348818
    1      Lasso(alpha=10)  42.436622
    2       Lasso(alpha=1)  27.493672
    3     Ridge(alpha=100)  23.487453
    4     Lasso(alpha=0.1)  22.979708
    5      Ridge(alpha=10)  22.793119
    6     LinearRegression  22.770784
    7   Ridge(alpha=0.001)  22.770117
    8    Ridge(alpha=0.01)  22.764254
    9     Ridge(alpha=0.1)  22.718126
    10      Ridge(alpha=1)  22.690411
    11   Lasso(alpha=0.01)  22.635614



![output_92_14](/images/S-Python-sklearn3/output_92_14.png)



![output_92_15](/images/S-Python-sklearn3/output_92_15.png)


                     model        mse
    0     Lasso(alpha=100)  63.348818
    1      Lasso(alpha=10)  42.436622
    2       Lasso(alpha=1)  27.493672
    3     Ridge(alpha=100)  23.487453
    4     Lasso(alpha=0.1)  22.979708
    5      Ridge(alpha=10)  22.793119
    6     LinearRegression  22.770784
    7   Ridge(alpha=0.001)  22.770117
    8    Ridge(alpha=0.01)  22.764254
    9   Lasso(alpha=0.001)  22.753017
    10    Ridge(alpha=0.1)  22.718126
    11      Ridge(alpha=1)  22.690411
    12   Lasso(alpha=0.01)  22.635614



![output_92_17](/images/S-Python-sklearn3/output_92_17.png)

<br/>


* **coefficients 값 확인**


```python
# alpha = 0.01
lasso_01 = Lasso(alpha=0.01)
lasso_01.fit(x_train, y_train)
lasso_pred_01 = lasso_01.predict(x_test)

# alpha = 100
lasso_100 = Lasso(alpha=100)
lasso_100.fit(x_train, y_train)
lasso_pred_100 = lasso_100.predict(x_test)
```

  <br/>

[alpha = 0.01]


```python
x_train.columns
```


    Index(['CRIM', 'ZN', 'INDUS', 'CHAS', 'NOX', 'RM', 'AGE', 'DIS', 'RAD', 'TAX',
           'PTRATIO', 'B', 'LSTAT'],
          dtype='object')




```python
lasso_01.coef_
```


    array([ -0.09427142,   0.04759954,   0.01255668,   3.08256139,
           -15.36800113,   4.07373679,  -0.00100439,  -1.40819927,
             0.27152905,  -0.0097157 ,  -0.84377679,   0.01249204,
            -0.52790174])




```python
plot_coef(x_train.columns, lasso_01.coef_)
```


![output_100_0](/images/S-Python-sklearn3/output_100_0.png)

<br/>


[alpha = 100]


```python
x_train.columns
```


    Index(['CRIM', 'ZN', 'INDUS', 'CHAS', 'NOX', 'RM', 'AGE', 'DIS', 'RAD', 'TAX',
           'PTRATIO', 'B', 'LSTAT'],
          dtype='object')




```python
lasso_100.coef_
```


    array([-0.        ,  0.        , -0.        ,  0.        , -0.        ,
            0.        , -0.        ,  0.        , -0.        , -0.02078349,
           -0.        ,  0.00644409, -0.        ])




```python
plot_coef(x_train.columns, lasso_100.coef_)
```


![output_105_0](/images/S-Python-sklearn3/output_105_0.png)

<br/>


**>> ElasticNet**  [[Document]](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.ElasticNet.html)


```python
from sklearn.linear_model import ElasticNet
```

* **예측 결과 확인**


```python
ratios = [0.2, 0.5, 0.8]
```


```python
# alpha = 0.5 로 고정

for ratio in ratios:
    elasticnet = ElasticNet(alpha=0.1, l1_ratio=ratio)
    elasticnet.fit(x_train, y_train)
    elas_pred = elasticnet.predict(x_test)
    mse_eval('ElasticNet(l1_ratio={})'.format(ratio), y_test, elas_pred)
```


![output_111_0](/images/S-Python-sklearn3/output_111_0.png)


                           model        mse
    0           Lasso(alpha=100)  63.348818
    1            Lasso(alpha=10)  42.436622
    2             Lasso(alpha=1)  27.493672
    3           Ridge(alpha=100)  23.487453
    4           Lasso(alpha=0.1)  22.979708
    5            Ridge(alpha=10)  22.793119
    6           LinearRegression  22.770784
    7         Ridge(alpha=0.001)  22.770117
    8          Ridge(alpha=0.01)  22.764254
    9         Lasso(alpha=0.001)  22.753017
    10  ElasticNet(l1_ratio=0.2)  22.749018
    11          Ridge(alpha=0.1)  22.718126
    12            Ridge(alpha=1)  22.690411
    13         Lasso(alpha=0.01)  22.635614



![output_111_2](/images/S-Python-sklearn3/output_111_2.png)



![output_111_3](/images/S-Python-sklearn3/output_111_3.png)


                           model        mse
    0           Lasso(alpha=100)  63.348818
    1            Lasso(alpha=10)  42.436622
    2             Lasso(alpha=1)  27.493672
    3           Ridge(alpha=100)  23.487453
    4           Lasso(alpha=0.1)  22.979708
    5            Ridge(alpha=10)  22.793119
    6   ElasticNet(l1_ratio=0.5)  22.787269
    7           LinearRegression  22.770784
    8         Ridge(alpha=0.001)  22.770117
    9          Ridge(alpha=0.01)  22.764254
    10        Lasso(alpha=0.001)  22.753017
    11  ElasticNet(l1_ratio=0.2)  22.749018
    12          Ridge(alpha=0.1)  22.718126
    13            Ridge(alpha=1)  22.690411
    14         Lasso(alpha=0.01)  22.635614



![output_111_5](/images/S-Python-sklearn3/output_111_5.png)



![output_111_6](/images/S-Python-sklearn3/output_111_6.png)


                           model        mse
    0           Lasso(alpha=100)  63.348818
    1            Lasso(alpha=10)  42.436622
    2             Lasso(alpha=1)  27.493672
    3           Ridge(alpha=100)  23.487453
    4           Lasso(alpha=0.1)  22.979708
    5   ElasticNet(l1_ratio=0.8)  22.865628
    6            Ridge(alpha=10)  22.793119
    7   ElasticNet(l1_ratio=0.5)  22.787269
    8           LinearRegression  22.770784
    9         Ridge(alpha=0.001)  22.770117
    10         Ridge(alpha=0.01)  22.764254
    11        Lasso(alpha=0.001)  22.753017
    12  ElasticNet(l1_ratio=0.2)  22.749018
    13          Ridge(alpha=0.1)  22.718126
    14            Ridge(alpha=1)  22.690411
    15         Lasso(alpha=0.01)  22.635614



![output_111_8](/images/S-Python-sklearn3/output_111_8.png)

<br/>


* **coefficients 값 확인**


```python
# ㅣ1_ratio = 0.2
elasticnet_2 = ElasticNet(alpha = 0.1, l1_ratio = 0.2)
elasticnet_2.fit(x_train, y_train)
elast_pred_2 = elasticnet_2.predict(x_test)

# l1_ratio = 0.8
elasticnet_8 = ElasticNet(alpha=0.1, l1_ratio = 0.8)
elasticnet_8.fit(x_train, y_train)
elast_pred_8 = elasticnet_8.predict(x_test)
```

  <br/>

[ l1_ratio = 0.2 ]


```python
x_train.columns
```


    Index(['CRIM', 'ZN', 'INDUS', 'CHAS', 'NOX', 'RM', 'AGE', 'DIS', 'RAD', 'TAX',
           'PTRATIO', 'B', 'LSTAT'],
          dtype='object')




```python
elasticnet_2.coef_
```


    array([-0.09297585,  0.05293361, -0.03950412,  1.30126199, -0.41996826,
            3.15838796, -0.00644646, -1.15290012,  0.25973467, -0.01231233,
           -0.77186571,  0.01201684, -0.60780037])




```python
plot_coef(x_train.columns, elasticnet_2.coef_)
```


![output_119_0](/images/S-Python-sklearn3/output_119_0.png)

<br/>


[ l1_ratio = 0.8 ]


```python
x_train.columns
```


    Index(['CRIM', 'ZN', 'INDUS', 'CHAS', 'NOX', 'RM', 'AGE', 'DIS', 'RAD', 'TAX',
           'PTRATIO', 'B', 'LSTAT'],
          dtype='object')




```python
elasticnet_8.coef_
```


    array([-0.08797633,  0.05035601, -0.03058513,  1.51071961, -0.        ,
            3.70247373, -0.01017259, -1.12431077,  0.24389841, -0.01189981,
           -0.73481448,  0.01259147, -0.573733  ])




```python
plot_coef(x_train.columns, elasticnet_8.coef_)
```


![output_124_0](/images/S-Python-sklearn3/output_124_0.png)

<br/>

<br/>


## **4. Scaling**

### 4-1. Scaler 소개

* StandardScaler

* MinMaxScaler

* RobustScaler

  <br/>


```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler, RobustScaler
```


```python
x_train.describe()
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
<table  >
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
      <th>count</th>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
      <td>379.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>3.512192</td>
      <td>11.779683</td>
      <td>10.995013</td>
      <td>0.076517</td>
      <td>0.548712</td>
      <td>6.266953</td>
      <td>67.223483</td>
      <td>3.917811</td>
      <td>9.282322</td>
      <td>404.680739</td>
      <td>18.448549</td>
      <td>357.048100</td>
      <td>12.633773</td>
    </tr>
    <tr>
      <th>std</th>
      <td>8.338717</td>
      <td>23.492842</td>
      <td>6.792065</td>
      <td>0.266175</td>
      <td>0.115006</td>
      <td>0.681796</td>
      <td>28.563787</td>
      <td>2.084167</td>
      <td>8.583051</td>
      <td>166.813256</td>
      <td>2.154917</td>
      <td>92.745266</td>
      <td>7.259213</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.006320</td>
      <td>0.000000</td>
      <td>0.460000</td>
      <td>0.000000</td>
      <td>0.385000</td>
      <td>3.561000</td>
      <td>2.900000</td>
      <td>1.129600</td>
      <td>1.000000</td>
      <td>188.000000</td>
      <td>12.600000</td>
      <td>2.520000</td>
      <td>1.730000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.078910</td>
      <td>0.000000</td>
      <td>5.190000</td>
      <td>0.000000</td>
      <td>0.445000</td>
      <td>5.876500</td>
      <td>42.250000</td>
      <td>2.150900</td>
      <td>4.000000</td>
      <td>278.000000</td>
      <td>17.150000</td>
      <td>375.425000</td>
      <td>6.910000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.228760</td>
      <td>0.000000</td>
      <td>9.690000</td>
      <td>0.000000</td>
      <td>0.532000</td>
      <td>6.208000</td>
      <td>74.400000</td>
      <td>3.414500</td>
      <td>5.000000</td>
      <td>330.000000</td>
      <td>19.000000</td>
      <td>392.110000</td>
      <td>11.380000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2.756855</td>
      <td>19.000000</td>
      <td>18.100000</td>
      <td>0.000000</td>
      <td>0.624000</td>
      <td>6.611000</td>
      <td>93.850000</td>
      <td>5.400900</td>
      <td>8.000000</td>
      <td>666.000000</td>
      <td>20.200000</td>
      <td>396.260000</td>
      <td>16.580000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>73.534100</td>
      <td>100.000000</td>
      <td>27.740000</td>
      <td>1.000000</td>
      <td>0.871000</td>
      <td>8.398000</td>
      <td>100.000000</td>
      <td>10.585700</td>
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



 <br/> 

**>> StandardScaler**

평균(mean)을 0, 표준편차(std)를 1로 만들어 주는 scaler


```python
std_scaler = StandardScaler()
std_scaled = std_scaler.fit_transform(x_train)
round(pd.DataFrame(std_scaled).describe(), 2)
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>-0.00</td>
      <td>-0.00</td>
      <td>-0.00</td>
      <td>-0.00</td>
      <td>0.00</td>
      <td>-0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-0.42</td>
      <td>-0.50</td>
      <td>-1.55</td>
      <td>-0.29</td>
      <td>-1.43</td>
      <td>-3.97</td>
      <td>-2.25</td>
      <td>-1.34</td>
      <td>-0.97</td>
      <td>-1.30</td>
      <td>-2.72</td>
      <td>-3.83</td>
      <td>-1.50</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-0.41</td>
      <td>-0.50</td>
      <td>-0.86</td>
      <td>-0.29</td>
      <td>-0.90</td>
      <td>-0.57</td>
      <td>-0.88</td>
      <td>-0.85</td>
      <td>-0.62</td>
      <td>-0.76</td>
      <td>-0.60</td>
      <td>0.20</td>
      <td>-0.79</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-0.39</td>
      <td>-0.50</td>
      <td>-0.19</td>
      <td>-0.29</td>
      <td>-0.15</td>
      <td>-0.09</td>
      <td>0.25</td>
      <td>-0.24</td>
      <td>-0.50</td>
      <td>-0.45</td>
      <td>0.26</td>
      <td>0.38</td>
      <td>-0.17</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>-0.09</td>
      <td>0.31</td>
      <td>1.05</td>
      <td>-0.29</td>
      <td>0.66</td>
      <td>0.51</td>
      <td>0.93</td>
      <td>0.71</td>
      <td>-0.15</td>
      <td>1.57</td>
      <td>0.81</td>
      <td>0.42</td>
      <td>0.54</td>
    </tr>
    <tr>
      <th>max</th>
      <td>8.41</td>
      <td>3.76</td>
      <td>2.47</td>
      <td>3.47</td>
      <td>2.81</td>
      <td>3.13</td>
      <td>1.15</td>
      <td>3.20</td>
      <td>1.72</td>
      <td>1.84</td>
      <td>1.65</td>
      <td>0.43</td>
      <td>3.49</td>
    </tr>
  </tbody>
</table>

</div>



<br/>  

**>> MinMaxScaler**

min값과 max값을 0~1사이로 정규화 (Normalize)


```python
minmax_scaler = MinMaxScaler()
minmax_scaled = minmax_scaler.fit_transform(x_train)
round(pd.DataFrame(minmax_scaled).describe(), 2)
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
      <td>379.00</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.05</td>
      <td>0.12</td>
      <td>0.39</td>
      <td>0.08</td>
      <td>0.34</td>
      <td>0.56</td>
      <td>0.66</td>
      <td>0.29</td>
      <td>0.36</td>
      <td>0.41</td>
      <td>0.62</td>
      <td>0.90</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.11</td>
      <td>0.23</td>
      <td>0.25</td>
      <td>0.27</td>
      <td>0.24</td>
      <td>0.14</td>
      <td>0.29</td>
      <td>0.22</td>
      <td>0.37</td>
      <td>0.32</td>
      <td>0.23</td>
      <td>0.24</td>
      <td>0.20</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.17</td>
      <td>0.00</td>
      <td>0.12</td>
      <td>0.48</td>
      <td>0.41</td>
      <td>0.11</td>
      <td>0.13</td>
      <td>0.17</td>
      <td>0.48</td>
      <td>0.95</td>
      <td>0.14</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.34</td>
      <td>0.00</td>
      <td>0.30</td>
      <td>0.55</td>
      <td>0.74</td>
      <td>0.24</td>
      <td>0.17</td>
      <td>0.27</td>
      <td>0.68</td>
      <td>0.99</td>
      <td>0.27</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.04</td>
      <td>0.19</td>
      <td>0.65</td>
      <td>0.00</td>
      <td>0.49</td>
      <td>0.63</td>
      <td>0.94</td>
      <td>0.45</td>
      <td>0.30</td>
      <td>0.91</td>
      <td>0.81</td>
      <td>1.00</td>
      <td>0.41</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>

</div>



<br/>  

**>> RobustScaler**

중앙값(median)이 0, IQR(interquartile rage)이 1이 되도록 변환  
**outlier 처리에 유용**


```python
robust_scaler = RobustScaler()
robust_scaled = robust_scaler.fit_transform(x_train)
round(pd.DataFrame(robust_scaled).median(), 2)
```


    0     0.0
    1     0.0
    2     0.0
    3     0.0
    4     0.0
    5     0.0
    6     0.0
    7     0.0
    8     0.0
    9     0.0
    10    0.0
    11    0.0
    12    0.0
    dtype: float64



  <br/>

### 4-2. Scaling 후 모델 학습 -- 파이프라인 활용


```python
from sklearn.pipeline import make_pipeline
```


```python
# elasticnet(alpha=0.1, l1_ratio=0.2) < without standard scaling >
elasticnet_no_scale = ElasticNet(alpha=0.1, l1_ratio=0.2)
no_scale_pred = elasticnet_no_scale.fit(x_train, y_train).predict(x_test)
mse_eval('No Standard ElasticNet', y_test, no_scale_pred)


# elasticnet(alpha=0.1, l1_ratio=0.2) < with standard scaling >
elasticnet_pipeline = make_pipeline(
    StandardScaler(),
    ElasticNet(alpha=0.1, l1_ratio=0.2)
)

with_scale_pred = elasticnet_pipeline.fit(x_train, y_train).predict(x_test)
mse_eval('With Standard ElasticNet', y_test, with_scale_pred)
```


![output_148_0](/images/S-Python-sklearn3/output_148_0.png)


                           model        mse
    0           Lasso(alpha=100)  63.348818
    1            Lasso(alpha=10)  42.436622
    2             Lasso(alpha=1)  27.493672
    3           Ridge(alpha=100)  23.487453
    4           Lasso(alpha=0.1)  22.979708
    5   ElasticNet(l1_ratio=0.8)  22.865628
    6            Ridge(alpha=10)  22.793119
    7   ElasticNet(l1_ratio=0.5)  22.787269
    8           LinearRegression  22.770784
    9         Ridge(alpha=0.001)  22.770117
    10         Ridge(alpha=0.01)  22.764254
    11        Lasso(alpha=0.001)  22.753017
    12  ElasticNet(l1_ratio=0.2)  22.749018
    13    No Standard ElasticNet  22.749018
    14          Ridge(alpha=0.1)  22.718126
    15            Ridge(alpha=1)  22.690411
    16         Lasso(alpha=0.01)  22.635614



![output_148_2](/images/S-Python-sklearn3/output_148_2.png)



![output_148_3](/images/S-Python-sklearn3/output_148_3.png)


                           model        mse
    0           Lasso(alpha=100)  63.348818
    1            Lasso(alpha=10)  42.436622
    2             Lasso(alpha=1)  27.493672
    3           Ridge(alpha=100)  23.487453
    4   With Standard ElasticNet  23.230164
    5           Lasso(alpha=0.1)  22.979708
    6   ElasticNet(l1_ratio=0.8)  22.865628
    7            Ridge(alpha=10)  22.793119
    8   ElasticNet(l1_ratio=0.5)  22.787269
    9           LinearRegression  22.770784
    10        Ridge(alpha=0.001)  22.770117
    11         Ridge(alpha=0.01)  22.764254
    12        Lasso(alpha=0.001)  22.753017
    13  ElasticNet(l1_ratio=0.2)  22.749018
    14    No Standard ElasticNet  22.749018
    15          Ridge(alpha=0.1)  22.718126
    16            Ridge(alpha=1)  22.690411
    17         Lasso(alpha=0.01)  22.635614



![output_148_5](/images/S-Python-sklearn3/output_148_5.png)

<br/>

<br/>


## **5. Polynomial Features**

[[Document]](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.PolynomialFeatures.html?highlight=poly%20feature#sklearn.preprocessing.PolynomialFeatures)

다항식의 계수간 상호작용을 통해 **새로운 feature를 생성**한다.  
예를 들면, [a, b] 2개의 feature가 존재한다고 가정하고,  
degree=2로 설정한다면, polynomial features 는 [1, a, b, a^2, ab, b^2]가 돤다  

<br/>

```python
from sklearn.preprocessing import PolynomialFeatures
```

**Polynomial Features 생성**


```python
poly = PolynomialFeatures(degree=2, include_bias=False)
```


```python
poly_features = poly.fit_transform(x_train)[0]
poly_features
```




    array([     0.12329   ,      0.        ,     10.01      ,      0.        ,
                0.547     ,      5.913     ,     92.9       ,      2.3534    ,
                6.        ,    432.        ,     17.8       ,    394.95      ,
               16.21      ,      0.01520042,      0.        ,      1.2341329 ,
                0.        ,      0.06743963,      0.72901377,     11.453641  ,
                0.29015069,      0.73974   ,     53.26128   ,      2.194562  ,
               48.6933855 ,      1.9985309 ,      0.        ,      0.        ,
                0.        ,      0.        ,      0.        ,      0.        ,
                0.        ,      0.        ,      0.        ,      0.        ,
                0.        ,      0.        ,    100.2001    ,      0.        ,
                5.47547   ,     59.18913   ,    929.929     ,     23.557534  ,
               60.06      ,   4324.32      ,    178.178     ,   3953.4495    ,
              162.2621    ,      0.        ,      0.        ,      0.        ,
                0.        ,      0.        ,      0.        ,      0.        ,
                0.        ,      0.        ,      0.        ,      0.299209  ,
                3.234411  ,     50.8163    ,      1.2873098 ,      3.282     ,
              236.304     ,      9.7366    ,    216.03765   ,      8.86687   ,
               34.963569  ,    549.3177    ,     13.9156542 ,     35.478     ,
             2554.416     ,    105.2514    ,   2335.33935   ,     95.84973   ,
             8630.41      ,    218.63086   ,    557.4       ,  40132.8       ,
             1653.62      ,  36690.855     ,   1505.909     ,      5.53849156,
               14.1204    ,   1016.6688    ,     41.89052   ,    929.47533   ,
               38.148614  ,     36.        ,   2592.        ,    106.8       ,
             2369.7       ,     97.26      , 186624.        ,   7689.6       ,
           170618.4       ,   7002.72      ,    316.84      ,   7030.11      ,
              288.538     , 155985.5025    ,   6402.1395    ,    262.7641    ])




```python
x_train.iloc[0]
```


    CRIM         0.12329
    ZN           0.00000
    INDUS       10.01000
    CHAS         0.00000
    NOX          0.54700
    RM           5.91300
    AGE         92.90000
    DIS          2.35340
    RAD          6.00000
    TAX        432.00000
    PTRATIO     17.80000
    B          394.95000
    LSTAT       16.21000
    Name: 112, dtype: float64



  <br/>

**Polynomial Features + Standard Scaling 후 모델 학습**


```python
poly_pipeline = make_pipeline(
    PolynomialFeatures(degree=2, include_bias=False),
    StandardScaler(),
    ElasticNet(alpha=0.1, l1_ratio=0.2)
)
```


```python
poly_pred = poly_pipeline.fit(x_train, y_train).predict(x_test)
```

    D:\Anaconda\lib\site-packages\sklearn\linear_model\_coordinate_descent.py:476: ConvergenceWarning: Objective did not converge. You might want to increase the number of iterations. Duality gap: 32.61172784964583, tolerance: 3.2374824854881266
      positive)



```python
mse_eval('Poly ElasticNet', y_test, poly_pred)
```


![output_163_0](/images/S-Python-sklearn3/output_163_0.png)


                           model        mse
    0           Lasso(alpha=100)  63.348818
    1            Lasso(alpha=10)  42.436622
    2             Lasso(alpha=1)  27.493672
    3           Ridge(alpha=100)  23.487453
    4   With Standard ElasticNet  23.230164
    5           Lasso(alpha=0.1)  22.979708
    6   ElasticNet(l1_ratio=0.8)  22.865628
    7            Ridge(alpha=10)  22.793119
    8   ElasticNet(l1_ratio=0.5)  22.787269
    9           LinearRegression  22.770784
    10        Ridge(alpha=0.001)  22.770117
    11         Ridge(alpha=0.01)  22.764254
    12        Lasso(alpha=0.001)  22.753017
    13  ElasticNet(l1_ratio=0.2)  22.749018
    14    No Standard ElasticNet  22.749018
    15          Ridge(alpha=0.1)  22.718126
    16            Ridge(alpha=1)  22.690411
    17         Lasso(alpha=0.01)  22.635614
    18           Poly ElasticNet  17.526214



![output_163_2](/images/S-Python-sklearn3/output_163_2.png)



2차 Polynomial Features 추가 후 학습된 모델의 성능이 많이 향상 된것을 확인할 수 있다

<br/>

<br/>
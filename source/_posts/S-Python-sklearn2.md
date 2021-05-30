---
title: Python >> sklearn - (2) 분류 (Classification)
tags:
  - Python
  - sklearn
  - Machine Learning
  - 분류
categories:
  - 【STUDY - Python】
  - Python - Machine Learning
cover: 'https://ohiing.com/wp-content/uploads/2020/02/scikit-learn-2.jpg'
description: >-
  Logistic Regression, SGD, KNN, SVM, Decision Tree, 분류 모델 성능 평가 (confusion
  matrix)

abbrlink: 150
date: 2020-07-26 20:23:49
---

# **분류 (Classification)**

@[toc] 

 <br/>


```python
import warnings
warnings.filterwarnings('ignore') # 불필요한 경고 출력을 방지함
```


```python
import pandas as pd
```

  <br/>

## **0. 데이터 셋**

[sklearn.dataset](https://scikit-learn.org/stable/modules/classes.html#module-sklearn.datasets) 에서 제공해주는 다양한 샘플 데이터를 활용한다

여기서는 iris 데이터 셋을 활용한다

 <br/> 

### 0-1. iris 데이터 셋

**Mission:** 꽃 종류 분류하기

[iris 데이터 셋](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_iris.html#sklearn.datasets.load_iris)


```python
from sklearn.datasets import load_iris
```


```python
# iris 데이터 셋 로드
iris = load_iris()
```

 <br/>

**iris 데이터 셋 구성 (key values):**

* ```DESCR```: 데이터 셋의 정보를 보여줌

* ```data```: feature data

* ```feature_names```: feature data의 컬럼 이름

* ```target```: label data (수치형)

* ```target_names```: label data의 value 이름 (문자형)

   <br/>


```python
# 데이터 셋 정보 확인하기
print(iris['DESCR'])
```

    .. _iris_dataset:
    
    Iris plants dataset
    --------------------
    
    **Data Set Characteristics:**
    
        :Number of Instances: 150 (50 in each of three classes)
        :Number of Attributes: 4 numeric, predictive attributes and the class
        :Attribute Information:
            - sepal length in cm
            - sepal width in cm
            - petal length in cm
            - petal width in cm
            - class:
                    - Iris-Setosa
                    - Iris-Versicolour
                    - Iris-Virginica
                    
        :Summary Statistics:
    
        ============== ==== ==== ======= ===== ====================
                        Min  Max   Mean    SD   Class Correlation
        ============== ==== ==== ======= ===== ====================
        sepal length:   4.3  7.9   5.84   0.83    0.7826
        sepal width:    2.0  4.4   3.05   0.43   -0.4194
        petal length:   1.0  6.9   3.76   1.76    0.9490  (high!)
        petal width:    0.1  2.5   1.20   0.76    0.9565  (high!)
        ============== ==== ==== ======= ===== ====================
    
        :Missing Attribute Values: None
        :Class Distribution: 33.3% for each of 3 classes.
        :Creator: R.A. Fisher
        :Donor: Michael Marshall (MARSHALL%PLU@io.arc.nasa.gov)
        :Date: July, 1988
    
    The famous Iris database, first used by Sir R.A. Fisher. The dataset is taken
    from Fisher's paper. Note that it's the same as in R, but not as in the UCI
    Machine Learning Repository, which has two wrong data points.
    
    This is perhaps the best known database to be found in the
    pattern recognition literature.  Fisher's paper is a classic in the field and
    is referenced frequently to this day.  (See Duda & Hart, for example.)  The
    data set contains 3 classes of 50 instances each, where each class refers to a
    type of iris plant.  One class is linearly separable from the other 2; the
    latter are NOT linearly separable from each other.
    
    .. topic:: References
    
       - Fisher, R.A. "The use of multiple measurements in taxonomic problems"
         Annual Eugenics, 7, Part II, 179-188 (1936); also in "Contributions to
         Mathematical Statistics" (John Wiley, NY, 1950).
       - Duda, R.O., & Hart, P.E. (1973) Pattern Classification and Scene Analysis.
         (Q327.D83) John Wiley & Sons.  ISBN 0-471-22361-1.  See page 218.
       - Dasarathy, B.V. (1980) "Nosing Around the Neighborhood: A New System
         Structure and Classification Rule for Recognition in Partially Exposed
         Environments".  IEEE Transactions on Pattern Analysis and Machine
         Intelligence, Vol. PAMI-2, No. 1, 67-71.
       - Gates, G.W. (1972) "The Reduced Nearest Neighbor Rule".  IEEE Transactions
         on Information Theory, May 1972, 431-433.
       - See also: 1988 MLC Proceedings, 54-64.  Cheeseman et al"s AUTOCLASS II
         conceptual clustering system finds 3 classes in the data.
       - Many, many more ...



<br/>

```python
# data 불러오기
data = iris['data']
data[:5]
```


    array([[5.1, 3.5, 1.4, 0.2],
           [4.9, 3. , 1.4, 0.2],
           [4.7, 3.2, 1.3, 0.2],
           [4.6, 3.1, 1.5, 0.2],
           [5. , 3.6, 1.4, 0.2]])

<br/>


```python
# feature names 확인하기
feature_names = iris['feature_names']
feature_names
```


    ['sepal length (cm)',
     'sepal width (cm)',
     'petal length (cm)',
     'petal width (cm)']

**[해석]** sepal: 꽃 받침;  petal: 꽃잎 

<br/>


```python
# label data 확인하기
target = iris['target']
target[:5]
```


    array([0, 0, 0, 0, 0])

 <br/>


```python
# target names 확인하기
iris['target_names']
```


    array(['setosa', 'versicolor', 'virginica'], dtype='<U10')

<br/>

  

### 0-2. 데이터프레임 만들기


```python
# feature data 먼저 생성하기
df_iris = pd.DataFrame(data, columns = feature_names)
df_iris.head()
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
      <th>sepal length (cm)</th>
      <th>sepal width (cm)</th>
      <th>petal length (cm)</th>
      <th>petal width (cm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>

</div>

<br/>


```python
# target column 추가하기
df_iris['target'] = target
df_iris.head()  # 최종 dataframe
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
      <th>sepal length (cm)</th>
      <th>sepal width (cm)</th>
      <th>petal length (cm)</th>
      <th>petal width (cm)</th>
      <th>target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

</div>



<br/>  

### 0-3. 시각화로 데이터셋 파악하기


```python
import matplotlib.pyplot as plt
import seaborn as sns
```

 <br/> 

**1. Sepal data로 보는 꽃 종류**


```python
df_iris.columns
```


    Index(['sepal length (cm)', 'sepal width (cm)', 'petal length (cm)',
           'petal width (cm)', 'target'],
          dtype='object')




```python
sns.scatterplot('sepal width (cm)', 'sepal length (cm)', hue='target', palette='muted', data=df_iris)
plt.title('Sepal')
plt.show()
```


![png](/images/S-Python-sklearn2/output_32_0.png)

<br/>


**2. petal data로 보는 꽃 종류**


```python
sns.scatterplot('petal width (cm)', 'petal length (cm)', hue='target', palette='muted', data=df_iris)
plt.title('Petal')
plt.show()
```


![png](/images/S-Python-sklearn2/output_35_0.png)

<br/>


**3. 3D plot로 보는 꽃 종류 (PCA 이용)**


```python
from mpl_toolkits.mplot3d import Axes3D
from sklearn.decomposition import PCA

fig = plt.figure(figsize=(8, 6))
ax = Axes3D(fig, elev=-150, azim=110)
X_reduced = PCA(n_components=3).fit_transform(df_iris.drop('target', 1))
ax.scatter(X_reduced[:, 0], X_reduced[:, 1], X_reduced[:, 2], c=df_iris['target'],
           cmap=plt.cm.Set1, edgecolor='k', s=40)
ax.set_title("Iris 3D")
ax.set_xlabel("x")
ax.w_xaxis.set_ticklabels([])
ax.set_ylabel("y")
ax.w_yaxis.set_ticklabels([])
ax.set_zlabel("z")
ax.w_zaxis.set_ticklabels([])

plt.show()
```


![png](/images/S-Python-sklearn2/output_38_0.png)

<br/>

<br/>


## **1. training set / validation set 나누기**


```python
from sklearn.model_selection import train_test_split
```


```python
x_train, x_valid, y_train, y_valid = train_test_split(df_iris.drop('target', 1), df_iris['target'])
```


```python
x_train.shape, y_train.shape
```


    ((112, 4), (112,))


```python
x_valid.shape, y_valid.shape
```


    ((38, 4), (38,))

<br/>


```python
sns.countplot(y_train)
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1cb7aaaeec8>




![png](/images/S-Python-sklearn2/output_46_1.png)

'target'값이 0, 1, 2인 데이터가 Original dataset으로 부터 랜덤으로 뽑히기 때문에 **비율의 차이가 존재**할 수 있다. 따라서 기계학습할 때 **sample size가 큰 데이터 위주로 학습**하여 모델의 **예측성능이 떨어질** 수 있다. (위 상황에서, 학습된 머신러닝 모델이 sample size가 큰 target=1인 경우를 좀 더 잘 예측하고, target=2에 대한 예측도가 떨어질 수 있다)   



이를 방지하기 위해 우리는 **```stratify```옵션**을 이용하여 label의 class 분포를 균등하게 배분한다.

 <br/>


```python
x_train, x_valid, y_train, y_valid = train_test_split(df_iris.drop('target', 1), df_iris['target'], stratify=df_iris['target'])
```


```python
sns.countplot(y_train)
```


    <matplotlib.axes._subplots.AxesSubplot at 0x1cb7b17b508>




![png](/images/S-Python-sklearn2/output_50_1.png)



```python
x_train.shape, y_train.shape
```


    ((112, 4), (112,))




```python
x_valid.shape, y_valid.shape
```


    ((38, 4), (38,))

<br/>

  <br/>

  

## **2. 하이퍼 파라미터 (hyper-parameter) 튜닝**

모델 학습할 때 설정 한 옵션들은 **하이퍼 파라미터 (hyper-parameter)**라고 한다. 설정한 값에 따라 모델 성능도 달라질 수 있다.  

각 알고리즘 별, hyper-parameter의 종류가 매우 다양하다. 다음 두 가지 parameter는 기본적으로 설정해주는 것이 좋다:

* random_state: sampling seed 설정 (항상 동일하게 sampling 하기)

* n_jobs=-1: CPU를 모두 사용 (학습속도가 빠름)

  

  <br/>

## **3. 분류 알고리즘**

### 3-1. Logistic Regression

> [[sklearn.linear_model.**LogisticRegression**] Document](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html?highlight=logistic%20regression#sklearn.linear_model.LogisticRegression)

Logistic Regression, SVM(Support Vector Machine)과 같은 알고리즘은 **이진(Binary Class) 분류만 가능**한다. (2개의 클래스 판별만 가능한다.)

하지만, **3개 이상의 클래스에 대한 판별** **[다중 클래스(Multi-Class) 분류]**을 진행하는 경우, 다음과 같은 전략으로 판별한다.

* **one-vs-one (OvO)**:   K 개의 클래스가 존재할 때, 이 중 2개의 클래스 조합을 선택하여  <font color='blue'>K(K−1)/2 개</font>의 이진 클래스 분류 문제를 풀고 이진판별을 통해 가장 많은 판별값을 얻은 클래스를 선택하는 방법이다.

* **one-vs-rest (OvR)**: K 개의 클래스가 존재할 때, 클래스들을 "k번째 클래스(one)" & "나머지(rest)"로 나누어서 <font color='blue'>K개</font>의 개별 이진 분류 문제를 푼다. 즉, 각각의 클래스에 대해 표본이 속하는지(y=1) 속하지 않는지(y=0)의 이진 분류 문제를 푸는 것이다. OvO와 달리 클래스 수만큼의 이진 분류 문제를 풀면 된다.

대부분 **OvsR 전략을 선호**합니다.

  <br/>


```python
from sklearn.linear_model import LogisticRegression
```

**step 1: 모델 선언**


```python
lr = LogisticRegression(random_state=0)
```



**step 2: 모델 학습**


```python
lr.fit(x_train, y_train)
```


    LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,
                       intercept_scaling=1, l1_ratio=None, max_iter=100,
                       multi_class='auto', n_jobs=None, penalty='l2',
                       random_state=0, solver='lbfgs', tol=0.0001, verbose=0,
                       warm_start=False)



**step 3: 예측**


```python
prediction = lr.predict(x_valid)
```


```python
prediction[:5]
```


    array([0, 1, 2, 2, 0])



**step 4: 평가**


```python
(prediction == y_valid).mean()  # 정확도
```


    0.9473684210526315



 <br/> 

  

### 3-2. SGD (SGDClassifier)

> [[sklearn.linear_model.**SGDClassifier**] Document](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.SGDClassifier.html)

**stochastic gradient descent (SGD):** 확률적 경사 하강법


```python
from IPython.display import Image
```


```python
# 출처: https://machinelearningnotepad.wordpress.com/
Image('https://machinelearningnotepad.files.wordpress.com/2018/04/yk1mk.png', width=500)
```



<img src="/images/S-Python-sklearn2/output_80_0.png" alt="png" style="zoom: 33%;" />

<br/>


```python
from sklearn.linear_model import SGDClassifier
```

**step 1: 모델 선언**


```python
sgd = SGDClassifier(random_state=0)
```

**step 2: 모델 학습**


```python
sgd.fit(x_train, y_train)
```


    SGDClassifier(alpha=0.0001, average=False, class_weight=None,
                  early_stopping=False, epsilon=0.1, eta0=0.0, fit_intercept=True,
                  l1_ratio=0.15, learning_rate='optimal', loss='hinge',
                  max_iter=1000, n_iter_no_change=5, n_jobs=None, penalty='l2',
                  power_t=0.5, random_state=0, shuffle=True, tol=0.001,
                  validation_fraction=0.1, verbose=0, warm_start=False)



**step 3: 예측**


```python
prediction = sgd.predict(x_valid)
```

**step 4: 평가**


```python
(prediction == y_valid).mean()
```


    0.9473684210526315



 <br/> 

**Change hyper-parameter values:**

e.g.: penalty = 'l1', random_state = 1, n_jobs = -1


```python
sgd2 = SGDClassifier(penalty='l1', random_state=1, n_jobs=-1)
```


```python
sgd2.fit(x_train, y_train)
```


    SGDClassifier(alpha=0.0001, average=False, class_weight=None,
                  early_stopping=False, epsilon=0.1, eta0=0.0, fit_intercept=True,
                  l1_ratio=0.15, learning_rate='optimal', loss='hinge',
                  max_iter=1000, n_iter_no_change=5, n_jobs=-1, penalty='l1',
                  power_t=0.5, random_state=1, shuffle=True, tol=0.001,
                  validation_fraction=0.1, verbose=0, warm_start=False)


```python
prediction2 = sgd2.predict(x_valid)
```


```python
(prediction2 == y_valid).mean()
```


    1.0



 <br/> 

  

### 3-3. KNN (KNeighborsClassifier)

> [[sklearn.neighbors.**KNeighborsClassifier**] Document](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html)

**KNN (K Nearest Neighbors):** K 최근접 이웃 알고리즘

새로운 데이터의 분류 결과가 K 개 최근접 이웃의 클래스에 의해서 결정되며, 데이터는 가장 많이 할당되는 클래스로 분류하게 된다.


```python
# 출처: 데이터 캠프
Image('https://res.cloudinary.com/dyd911kmh/image/upload/f_auto,q_auto:best/v1531424125/KNN_final_a1mrv9.png')
```




![png](/images/S-Python-sklearn2/output_102_0.png)

<br/>


```python
from sklearn.neighbors import KNeighborsClassifier
```


```python
# 1. 모델 선언
knn = KNeighborsClassifier()
```


```python
# 2. 모델 학습
knn.fit(x_train, y_train)  # default: n_neighbors=5
```


    KNeighborsClassifier(algorithm='auto', leaf_size=30, metric='minkowski',
                         metric_params=None, n_jobs=None, n_neighbors=5, p=2,
                         weights='uniform')


```python
# 3. 예측
prediction = knn.predict(x_valid)
```


```python
# 4. 평가
(prediction == y_valid).mean()
```


    0.9210526315789473



  <br/>

n_neighnors를 9개로 설정하여 다시 예측해본다:


```python
knn2 = KNeighborsClassifier(n_neighbors=9)
knn2.fit(x_train, y_train)
knn2_pred = knn2.predict(x_valid)
```


```python
(knn2_pred == y_valid).mean()
```


    0.9473684210526315



<br/>  

  

### 3-4. SVM (SVC)

> [[sklearn.svm.**SVC**] Document](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html#sklearn.svm.SVC)

* 새로운 데이터가 어느 카테고리에 속할지 판단하는 비확률적 이진 선형 분류 모델을 만듦.
* 경계로 표현되는 데이터들 중 가장 큰 폭을 가진 경계를 찾는 알고리즘.


```python
Image('https://csstudy.files.wordpress.com/2011/03/screen-shot-2011-02-28-at-5-53-26-pm.png')
```




![png](/images/S-Python-sklearn2/output_117_0.png)

<br/>

SVM은 Logistic Regression과 같이 이진 분류만 가능하다. (2개의 클래스 판별만 가능)  
3개 이상의 클래스인 경우: **OvsR 전략** 사용


```python
from sklearn.svm import SVC  # SVC: Support Vector Classification
```


```python
svc = SVC(random_state=0)
svc.fit(x_train, y_train)
svc_pred = svc.predict(x_valid)
```


```python
svc  # hyper-parameter 확인
```


    SVC(C=1.0, break_ties=False, cache_size=200, class_weight=None, coef0=0.0,
        decision_function_shape='ovr', degree=3, gamma='scale', kernel='rbf',
        max_iter=-1, probability=False, random_state=0, shrinking=True, tol=0.001,
        verbose=False)




```python
(svc_pred == y_valid).mean()
```


    0.9473684210526315

<br/>

각 클래스 별 확률값을 return해주는 ```decision_function()```


```python
svc.decision_function(x_valid)[:5]
```


    array([[ 2.22273426,  1.18194657, -0.25426485],
           [-0.22060229,  2.23192595,  0.91725911],
           [-0.23638817,  1.18969144,  2.17593611],
           [-0.23457057,  1.07146337,  2.22588253],
           [ 2.22808358,  1.16872302, -0.25381783]])




```python
svc_pred[:5]
```


    array([0, 1, 2, 2, 0])



**확률값이 제일 높은 클래스**로 분류(예측) 된 것을 확인하실 수 있다

<br/>  

  

### 3-5. Decision Tree (DecisionTreeClassifier)

> [[sklearn.tree.**DecisionTreeClassifier**] Document](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html?highlight=decision%20tree#sklearn.tree.DecisionTreeClassifier)

#### 1. Decision Tree (의사 결정 나무): 나무 가지치기를 통해 소그룹으로 나누어 판별하는것


```python
Image('https://www.researchgate.net/profile/Ludmila_Aleksejeva/publication/293194222/figure/fig1/AS:669028842487827@1536520314657/Decision-tree-for-Iris-dataset.png', width=500)
```



<img src="/images/S-Python-sklearn2/output_132_0.png" alt="png" style="zoom: 67%;" />




```python
from sklearn.tree import DecisionTreeClassifier
```


```python
dt = DecisionTreeClassifier(random_state=0)
```


```python
dt.fit(x_train, y_train)
```


    DecisionTreeClassifier(ccp_alpha=0.0, class_weight=None, criterion='gini',
                           max_depth=None, max_features=None, max_leaf_nodes=None,
                           min_impurity_decrease=0.0, min_impurity_split=None,
                           min_samples_leaf=1, min_samples_split=2,
                           min_weight_fraction_leaf=0.0, presort='deprecated',
                           random_state=0, splitter='best')




```python
dt_pred = dt.predict(x_valid)
```


```python
(dt_pred == y_valid).mean()
```


    0.9210526315789473



<br/>  

#### 2. Decision Tree 분류 결과 시각화


```python
from sklearn.tree import export_graphviz
from IPython.display import Image
import numpy as np
```

  <br/>

**방법 1:** ```pydot```을 사용하여 "_dot_ 파일"을 "_png_ 이미지"로 전환 ([참고](https://niceman.tistory.com/169))


```python
pip install pydot
```

    Collecting pydotNote: you may need to restart the kernel to use updated packages.
      Downloading pydot-1.4.1-py2.py3-none-any.whl (19 kB)
    Requirement already satisfied: pyparsing>=2.1.4 in d:\anaconda\lib\site-packages (from pydot) (2.4.6)
    Installing collected packages: pydot
    Successfully installed pydot-1.4.1


​    <br/>


```python
# 참고: https://niceman.tistory.com/169
import pydot

# .dot결과 생성
export_graphviz(dt, out_file='tree.dot', feature_names=feature_names, class_names=np.unique(iris['target_names']))

# Encoding
(graph,) = pydot.graph_from_dot_file('tree.dot', encoding='utf8')

# .dot파일을 .png이미지로 저장
graph.write_png('tree.png')

Image(filename = 'tree.png', width=600)
```



<img src="/images/S-Python-sklearn2/output_144_0.png" alt="png" style="zoom: 80%;" />



  <br/>

 <br/>

**방법 2:** ```graphviz.Source```이용 ([참고](https://www.kaggle.com/praanj/titanic-decision-tree-complete-evaluation))


```python
pip install -U graphviz
```

    Requirement already up-to-date: graphviz in d:\anaconda\lib\site-packages (0.14.1)
    Note: you may need to restart the kernel to use updated packages.

```python
import graphviz
```


```python
# 참고: https://www.kaggle.com/vaishvik25/titanic-eda-fe-3-model-decision-tree-viz
from sklearn.tree import DecisionTreeClassifier, export_graphviz

tree_dot = export_graphviz(dt,out_file=None, feature_names=feature_names, class_names=np.unique(iris['target_names']))
tree = graphviz.Source(tree_dot)
tree
```



<img src="/images/S-Python-sklearn2/output_149_0.svg" alt="svg" style="zoom: 80%;" />



 <br/>

**gini계수:** 불순도를 의미함. gini계수가 높을 수록 엔트로피(Entropy)가 큼. 즉, 클래스가 혼잡하게 섞여 있음.

  <br/>

#### 3. 가지 치기 (pruning)

Overfitting을 방지하기 위해 적당히 가지 치기를 진행한다.


```python
# 수동으로 max_depth 설정
dt2 = DecisionTreeClassifier(max_depth=2)
dt2.fit(x_train, y_train)
dt2_pred = dt2.predict(x_valid)
```


```python
(dt2_pred == y_valid).mean()
```


    0.9210526315789473

<br/>


```python
tree2_dot = export_graphviz(dt2,out_file=None, feature_names=feature_names, class_names=np.unique(iris['target_names']))
tree2 = graphviz.Source(tree2_dot)
tree2
```




![svg](/images/S-Python-sklearn2/output_156_0.svg)



  <br/>

  <br/>

## **4. 모델 성능 평가 지표**

> 참고자료: [분류성능평가지표 - Precision(정밀도), Recall(재현율) and Accuracy(정확도)](https://sumniya.tistory.com/26)

### 4-1. 오차 행렬 (Confusion Matrix)

<img src="/images/S-Python-sklearn2/a9psOK.png" alt="confusion_matrix" style="zoom: 67%;" />

  <br/>

### 4-2. 정확도 (Accuracy)

**정확도 (Accuracy):** 모델이 샘플을 올바르게 예측하는 비율

$$Accuracy = \frac{TP+TN}{TP+FP+TN+FN}$$

 <br/> 

**!!정확도의 함정!!**

정확도는 모델의 성능을 가장 지관적으로 나타낼 수 있는 평가 지표다. 하지만, 만약 Actual positive sample과 Actual negative sample의 비율이 차이가 많이 나면 **정확도의 함정**에 빠질 수 있다.  

즉, ***모두 positive / negative로 예측*** 했을 때 모델의 정확도가 매우 높은 경우다. 이 경우에 <font color='blue'>**예측 정확도가 높지만, 모델의 예측 성능이 좋다라고 말할 수는 없다.**</font>

  <br/>

유방암 환자 데이터셋을 이용하여 한번 이해해 볼게요.


```python
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
import numpy as np
```


```python
cancer = load_breast_cancer(유방암 환자 데이터셋)
```


```python
print(cancer['DESCR'])  # describe
```

    .. _breast_cancer_dataset:
    
    Breast cancer wisconsin (diagnostic) dataset
    --------------------------------------------
    
    **Data Set Characteristics:**
    
        :Number of Instances: 569
    
        :Number of Attributes: 30 numeric, predictive attributes and the class
    
        :Attribute Information:
            - radius (mean of distances from center to points on the perimeter)
            - texture (standard deviation of gray-scale values)
            - perimeter
            - area
            - smoothness (local variation in radius lengths)
            - compactness (perimeter^2 / area - 1.0)
            - concavity (severity of concave portions of the contour)
            - concave points (number of concave portions of the contour)
            - symmetry 
            - fractal dimension ("coastline approximation" - 1)
    
            The mean, standard error, and "worst" or largest (mean of the three
            largest values) of these features were computed for each image,
            resulting in 30 features.  For instance, field 3 is Mean Radius, field
            13 is Radius SE, field 23 is Worst Radius.
    
            - class:
                    - WDBC-Malignant
                    - WDBC-Benign
    
        :Summary Statistics:
    
        ===================================== ====== ======
                                               Min    Max
        ===================================== ====== ======
        radius (mean):                        6.981  28.11
        texture (mean):                       9.71   39.28
        perimeter (mean):                     43.79  188.5
        area (mean):                          143.5  2501.0
        smoothness (mean):                    0.053  0.163
        compactness (mean):                   0.019  0.345
        concavity (mean):                     0.0    0.427
        concave points (mean):                0.0    0.201
        symmetry (mean):                      0.106  0.304
        fractal dimension (mean):             0.05   0.097
        radius (standard error):              0.112  2.873
        texture (standard error):             0.36   4.885
        perimeter (standard error):           0.757  21.98
        area (standard error):                6.802  542.2
        smoothness (standard error):          0.002  0.031
        compactness (standard error):         0.002  0.135
        concavity (standard error):           0.0    0.396
        concave points (standard error):      0.0    0.053
        symmetry (standard error):            0.008  0.079
        fractal dimension (standard error):   0.001  0.03
        radius (worst):                       7.93   36.04
        texture (worst):                      12.02  49.54
        perimeter (worst):                    50.41  251.2
        area (worst):                         185.2  4254.0
        smoothness (worst):                   0.071  0.223
        compactness (worst):                  0.027  1.058
        concavity (worst):                    0.0    1.252
        concave points (worst):               0.0    0.291
        symmetry (worst):                     0.156  0.664
        fractal dimension (worst):            0.055  0.208
        ===================================== ====== ======
    
        :Missing Attribute Values: None
    
        :Class Distribution: 212 - Malignant, 357 - Benign
    
        :Creator:  Dr. William H. Wolberg, W. Nick Street, Olvi L. Mangasarian
    
        :Donor: Nick Street
    
        :Date: November, 1995
    
    This is a copy of UCI ML Breast Cancer Wisconsin (Diagnostic) datasets.
    https://goo.gl/U2Uwz2
    
    Features are computed from a digitized image of a fine needle
    aspirate (FNA) of a breast mass.  They describe
    characteristics of the cell nuclei present in the image.
    
    Separating plane described above was obtained using
    Multisurface Method-Tree (MSM-T) [K. P. Bennett, "Decision Tree
    Construction Via Linear Programming." Proceedings of the 4th
    Midwest Artificial Intelligence and Cognitive Science Society,
    pp. 97-101, 1992], a classification method which uses linear
    programming to construct a decision tree.  Relevant features
    were selected using an exhaustive search in the space of 1-4
    features and 1-3 separating planes.
    
    The actual linear program used to obtain the separating plane
    in the 3-dimensional space is that described in:
    [K. P. Bennett and O. L. Mangasarian: "Robust Linear
    Programming Discrimination of Two Linearly Inseparable Sets",
    Optimization Methods and Software 1, 1992, 23-34].
    
    This database is also available through the UW CS ftp server:
    
    ftp ftp.cs.wisc.edu
    cd math-prog/cpo-dataset/machine-learn/WDBC/
    
    .. topic:: References
    
       - W.N. Street, W.H. Wolberg and O.L. Mangasarian. Nuclear feature extraction 
         for breast tumor diagnosis. IS&T/SPIE 1993 International Symposium on 
         Electronic Imaging: Science and Technology, volume 1905, pages 861-870,
         San Jose, CA, 1993.
       - O.L. Mangasarian, W.N. Street and W.H. Wolberg. Breast cancer diagnosis and 
         prognosis via linear programming. Operations Research, 43(4), pages 570-577, 
         July-August 1995.
       - W.H. Wolberg, W.N. Street, and O.L. Mangasarian. Machine learning techniques
         to diagnose breast cancer from fine-needle aspirates. Cancer Letters 77 (1994) 
         163-171.

<br/>

```python
data = cancer['data']
target = cancer['target']
feature_names = cancer['feature_names']
```


```python
# 데이터 프레임 생성
df = pd.DataFrame(data = data, columns = feature_names)
df['target'] = target
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
      <th>mean radius</th>
      <th>mean texture</th>
      <th>mean perimeter</th>
      <th>mean area</th>
      <th>mean smoothness</th>
      <th>mean compactness</th>
      <th>mean concavity</th>
      <th>mean concave points</th>
      <th>mean symmetry</th>
      <th>mean fractal dimension</th>
      <th>...</th>
      <th>worst texture</th>
      <th>worst perimeter</th>
      <th>worst area</th>
      <th>worst smoothness</th>
      <th>worst compactness</th>
      <th>worst concavity</th>
      <th>worst concave points</th>
      <th>worst symmetry</th>
      <th>worst fractal dimension</th>
      <th>target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17.99</td>
      <td>10.38</td>
      <td>122.80</td>
      <td>1001.0</td>
      <td>0.11840</td>
      <td>0.27760</td>
      <td>0.3001</td>
      <td>0.14710</td>
      <td>0.2419</td>
      <td>0.07871</td>
      <td>...</td>
      <td>17.33</td>
      <td>184.60</td>
      <td>2019.0</td>
      <td>0.1622</td>
      <td>0.6656</td>
      <td>0.7119</td>
      <td>0.2654</td>
      <td>0.4601</td>
      <td>0.11890</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20.57</td>
      <td>17.77</td>
      <td>132.90</td>
      <td>1326.0</td>
      <td>0.08474</td>
      <td>0.07864</td>
      <td>0.0869</td>
      <td>0.07017</td>
      <td>0.1812</td>
      <td>0.05667</td>
      <td>...</td>
      <td>23.41</td>
      <td>158.80</td>
      <td>1956.0</td>
      <td>0.1238</td>
      <td>0.1866</td>
      <td>0.2416</td>
      <td>0.1860</td>
      <td>0.2750</td>
      <td>0.08902</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>19.69</td>
      <td>21.25</td>
      <td>130.00</td>
      <td>1203.0</td>
      <td>0.10960</td>
      <td>0.15990</td>
      <td>0.1974</td>
      <td>0.12790</td>
      <td>0.2069</td>
      <td>0.05999</td>
      <td>...</td>
      <td>25.53</td>
      <td>152.50</td>
      <td>1709.0</td>
      <td>0.1444</td>
      <td>0.4245</td>
      <td>0.4504</td>
      <td>0.2430</td>
      <td>0.3613</td>
      <td>0.08758</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11.42</td>
      <td>20.38</td>
      <td>77.58</td>
      <td>386.1</td>
      <td>0.14250</td>
      <td>0.28390</td>
      <td>0.2414</td>
      <td>0.10520</td>
      <td>0.2597</td>
      <td>0.09744</td>
      <td>...</td>
      <td>26.50</td>
      <td>98.87</td>
      <td>567.7</td>
      <td>0.2098</td>
      <td>0.8663</td>
      <td>0.6869</td>
      <td>0.2575</td>
      <td>0.6638</td>
      <td>0.17300</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20.29</td>
      <td>14.34</td>
      <td>135.10</td>
      <td>1297.0</td>
      <td>0.10030</td>
      <td>0.13280</td>
      <td>0.1980</td>
      <td>0.10430</td>
      <td>0.1809</td>
      <td>0.05883</td>
      <td>...</td>
      <td>16.67</td>
      <td>152.20</td>
      <td>1575.0</td>
      <td>0.1374</td>
      <td>0.2050</td>
      <td>0.4000</td>
      <td>0.1625</td>
      <td>0.2364</td>
      <td>0.07678</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 31 columns</p>
</div>


</div>

<br/>

**target:** 0: Malignant (악성종양);  1: Benign (양성종양)


```python
pos = df.loc[df['target'] == 1] # 앙성 sample
neg = df.loc[df['target'] == 0] # 음성 sample
```


```python
pos.shape, neg.shape  
```


    ((357, 31), (212, 31))

<br/>

  

**시범용 sample data를 생성:** 양성 환자 357 + 음성 환자 5


```python
sample = pd.concat([pos, neg[:5]], sort=True)
```


```python
x_train, x_test, y_train, y_test = train_test_split(sample.drop('target',1), sample['target'], random_state=42)
```


```python
x_train.shape, y_train.shape
```


    ((271, 30), (271,))




```python
x_test.shape, y_test.shape
```


    ((91, 30), (91,))

<br/>


```python
# 모델 정의 및 학습
model = LogisticRegression()
model.fit(x_train, y_train)
model_pred = model.predict(x_test)
```

  <br/>

* Confusion Matrix


```python
from sklearn.metrics import confusion_matrix
```


```python
confusion_matrix(y_test, model_pred)
```


    array([[ 1,  0],
           [ 2, 88]], dtype=int64)




```python
sns.heatmap(confusion_matrix(y_test, model_pred), annot=True, cmap='Reds')
plt.xlabel('Predict')
plt.ylabel('Actual')
plt.show()
```


![png](/images/S-Python-sklearn2/output_192_0.png)

<br/>


* 정확도 (Accuracy)


```python
# logistic 모델 정확도
(model_pred == y_test).mean()
```


    0.978021978021978




```python
# 모두 양성으로 예측한 경우
my_pred = np.ones(shape=y_test.shape)

# 정확도
(my_pred == y_test).mean()
```


    0.989010989010989



정확도만 놓고 본다면, 무조건 양성 환자로 예측하는 분류기가 성능이 더 좋다. 하지만 **무조건 양성 환자로 예측해서 예측율이 98.9%로 말하는 의사는** 당영히 자질이 좋은 의사라고 볼 수 없다

정확도(Accuracy)만 보고 분류기의 성능을 판별하는 것은 위와 같은 오류에 빠질 수 있다. 이를 보완하기 위해 다음과 같은 지표들도 같이 활용하게 된다

  <br/>

### 4-3. 정밀도 (Precision)

**정밀도 (Precision):** 양성 예측의 정확도. 즉, Positive Prediction 중에서 올바르게 예측되는 비율

$$Precision=\frac{TP}{TP+FP}$$


```python
from sklearn.metrics import precision_score
```


```python
precision_score(y_test, model_pred)
```


    1.0

<br/>

  

### 4-4. 민감도 (Sensitivity)  /  재현율 (Recall)

**민감도 (Sensitivity) / 재현율 (Recall):**  
분류기가 양성 샘플에 대한 식별력을 나타남. 즉, Positive Condition 중에서 올바르게 예측되는 비율. True Positive Rate (TPR) 이라고도 불린다.   

$$Sensitivity / Recall = \frac{TP}{TP+FN}$$


```python
from sklearn.metrics import recall_score
```


```python
recall_score(y_test, model_pred)
```


    0.9777777777777777



  <br/>

### 4-5. 특이도 (Specificity)

**특이도 (Specificity):** 분류기가 음성 샘플에 대한 식별력을 나타남. 즉, Negative Condition 중에서 올바르게 예측되는 비율. True Negative Rate (TNR) 이라고도 불린다.

$$Specificity = \frac{TN}{TN+FP}$$

<br/>  

### 4-6. F1 Score

**F1 Score:** 정밀도(Precision)와 재현율(Recall)의 조화 평균을 나타나는 지표임.  
데이터 label이 불균형 구조일 때, 모델의 성능을 정확하게 평가할 수 있으며, 성능을 하나의 숫자로 표현할 수 있다.

$$F1\ Score = 2*\frac{Precision * Recall}{Precision + Recall}=\frac{TP}{TP+\frac{FN+FP}{2}}$$


```python
from sklearn.metrics import f1_score
```


```python
f1_score(y_test, model_pred)
```


    0.9887640449438202

<br/>

<br/>


### 
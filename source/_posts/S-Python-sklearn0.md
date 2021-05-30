---
title: Python >> sklearn -(0) sklearn 개요
tags:
  - Python
  - sklearn
  - Machine Learning
categories:
  - 【STUDY - Python】
  - Python - Machine Learning
cover: 'https://ohiing.com/wp-content/uploads/2020/02/scikit-learn-2.jpg'
abbrlink: 51119
date: 2020-07-17 16:36:59
typora-root-url: ..
---

# **scikit-learn 개요**

@[toc]

<br />

> [< scikit-learn > Homepage](https://scikit-learn.org/stable/)

scikit-learn 패키지는 지도학습, 비지도학습 등 대부분의 머신러닝 알고리즘을 제공하고 있으며, Python에서 머신러닝을 수행할 때 굉장히 많이 쓰이는 패키지 중의 하나다

![sk_learn](/images/S-Python-sklearn0/NzXkk9.png)

  <br />

## **Install Package**


```python
pip install -U scikit-learn  # -U: Update
```

    Note: you may need to restart the kernel to use updated packages.


​    

    Usage:   
      D:\Anaconda\python.exe -m pip install [options] <requirement specifier> [package-index-options] ...
      D:\Anaconda\python.exe -m pip install [options] -r <requirements file> [package-index-options] ...
      D:\Anaconda\python.exe -m pip install [options] [-e] <vcs project url> ...
      D:\Anaconda\python.exe -m pip install [options] [-e] <local project path> ...
      D:\Anaconda\python.exe -m pip install [options] <archive url/path> ...
    
    no such option: -:

<br />


## **Import Functions from Sub-packages**


```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
```

  <br />

## **3 Steps to Fit Model and Do Prediction**

**STEP 1. 모델 정의**


```python
from sklearn.linear_model import LinearRegression
model = LinearRegression()
```

  <br />

**STEP 2. 학습 (Fit in Training set)**

* 명령어:  *model_name* <font color='red'>.fit</font>


```python
model.fit(x_train, y_train)
```

  <br />

**STEP 3. 예측 (Predict in Test set)**

* 명령어: *model_name* <font color='red'>.predict</font>


```python
prediction = model.predict(x_test)
```

<br />

<br />
---
uuid: 3e52cdcf-9e56-b464-bbf4-2c108c17d3b7
title: Python 기초문법 - (6) Package
tags: 
 - Python
 - Python_Base
categories: [【STUDY - Python】, Python - 0. Base]
description: 패키지(Package) 와 import
cover: https://ih1.redbubble.net/image.452049706.1381/flat,750x,075,f-pad,750x1000,f8f8f8.u5.jpg
abbrlink: 58823
date: 2020-05-16 13:52:05
---

패키지(Package) 와 import
<!-- more -->

# **목록**

@[toc]

<br />

# **패키지(Package) 와 import**



## **1. 패키지와 모듈 그리고 함수의 관계도**

* **함수**들이 뭉쳐진 하나의 .py파일 안에 이루어진 것을 **모듈**이라고 한다  

* 여러 개의 모듈을 그룹화 하면 **패키지**가 된다  

* **패키지**는 종종 **라이브러비**라고도 불린다

  <br />


```python
from IPython.display import Image
# 출척: pythonstudy.xyz
Image('http://pythonstudy.xyz/images/basics/python-package.png')
```

<br />

![png](https://z3.ax1x.com/2021/08/25/hVR129.png)

<br /><br />

## **2. 모듈 import 하기**

**import 하는 방법**

.py (파이썬 파일 확장자)로 된 파일을 우리는 **모듈** 이라고 한다, import 구문을 통해 해당 파일을 불러올 수 있다


```python
import pandas
```

위의 코드는 pandas라는 모듈을 우리가 불러오겠다라는 의미이다

 <br /> <br /> 

## **3. 패키지 에서 import하기** 

* 패키지 안에서 하나의 모듈을 불러온다


```python
from pandas import DataFrame   # pandas라는 패키지 안에서 DataFrame이라는 모듈을 불러온다
```


```python
DataFrame()  # 모듈 DataFrame사용
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
<br />

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

</div>

<br />

* 통째로 패키지나 모듈을 불러온다


```python
import pandas
```


```python
pandas.DataFrame()  # DataFrame이라는 모듈을 사용하기 위해서는 .을 찍고 이어서 쓰면 됨
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
<br />

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

</div>

<br />

  <br />

## **4. 별칭 (alias) 지어주기**

pandas라는 패키지 이름이 너무 길기 때문에 우리는 약어로 줄여쓸 수 있다. 보통 pd를 보편적으로 많이 사용한다.

줄여서 별명을 지어줄 때는 as를 붙혀준다 


```python
import pandas as pd
```


```python
pd.DataFrame()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
<br />

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

</div>

<br />

 <br /> 

## **5. 앞으로 자주 사용할 패키지, 모듈 미리보기**


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

* numpy: 과학계산을 위한 패키지
* pandas: 데이터 분석을 할 때 가장 많이 쓰이는 패키지
* matplotlib: 시각확를 위한 패키지
* seaborn: 시각화를 위한 패키지 (matplotlib을 더 쉽게 사용할 수 있도록 도와주는 패키지)

<br /><br />
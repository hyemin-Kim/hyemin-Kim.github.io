---
title: Python >> Pandas 시각화
tags:
  - Python
  - Pandas
  - 시각화
categories: 
 - [【STUDY - Python】, Python - 2. Pandas]
 - [【STUDY - Python】, Python - 시각화]
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
typora-root-url: ..
abbrlink: 41067
date: 2020-06-25 14:09:37
---

# Pandas - 데이터 시각화

@[toc]

  <br />


```python
import pandas as pd
```


```python
df = pd.read_csv("house_price_clean.csv")
```


```python
df
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
      <th>지역</th>
      <th>규모</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>4</th>
      <td>인천</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>3488</td>
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
      <th>3288</th>
      <td>경남</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3065</td>
    </tr>
    <tr>
      <th>3289</th>
      <td>경남</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3247</td>
    </tr>
    <tr>
      <th>3290</th>
      <td>제주</td>
      <td>60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>4039</td>
    </tr>
    <tr>
      <th>3291</th>
      <td>제주</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3962</td>
    </tr>
    <tr>
      <th>3292</th>
      <td>제주</td>
      <td>102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>3601</td>
    </tr>
  </tbody>
</table>
<p>3293 rows × 5 columns</p>

</div>

<br />

  <br />

## **0. 준비 -- 한글폰트 깨짐현상 해결**

> ***reference:***  
> 1. [주피터 노트북(Jupyter notebook) - Matplotlib 한글 깨짐 현상 해결](https://blog.naver.com/itisik/221789012960)  
> 2. [matplotlib/seaborn으로 시각화할 때 한글 폰트 깨짐현상 해결방법](https://teddylee777.github.io/visualization/matplotlib-%EC%8B%9C%EA%B0%81%ED%99%94-%ED%95%9C%EA%B8%80%ED%8F%B0%ED%8A%B8%EC%A0%81%EC%9A%A9)

<br />

Jupyter Notebook에서 그래프를 그릴 때 한글 깨짐 현상이 발생한다


```python
df.plot()
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179eb070ac8>



![png](/images/S-Python-Pandas-visual/output_9_2.png)




> 우리는 **설정 파일을 수정하여 한글 폰트를 영구 등록**함으로써 이 문제를 해결할 수 있다  

<br />

**(1) 설정 파일 위치 찾기**


```python
import matplotlib as mpl

#font 설정 파일 위치 출력
mpl.matplotlib_fname()
```


    'D:\\Anaconda\\lib\\site-packages\\matplotlib\\mpl-data\\matplotlibrc'

<br />

  

**(2) 설정 파일 수정하기**

맨 마지막 ***matplotlibrc*** 는 우리가 수정해야할 파일의 이름이다

* step 1. 한글 폰트 적용  
  수정전: *==#== font.family   : ==sans-serif==*  
  수정후: *font.family   : ==Malgun Gothic==*

* step 2. minus 깨짐 방지  
  수정전: *==#== axes.unicode_minus  : ==True== ## use unicode for the minus symbol*  
  수정후: *axes.unicode_minus  : ==False== ## use unicode for the minus symbol*

<br />

**(3) Tip: 전역으로 시각화 figsize 조절**


```python
import matplotlib.pyplot as plt
plt.rcParams['figure.figsize'] = (8, 5)
```

 <br /> 

**설정을 완료한 후 jupyter notebook의 kernel을 리셋하고 다시 그래프를 그리면,
한글폰트가 깨지지 않고 잘 출력되는 것을 확인하실 수 있다.**


```python
df.plot()
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f01b0c48>




![png](/images/S-Python-Pandas-visual/output_24_1.png)

<br />

<br />


## **1. Plot 그래프**

> *df_name* [ *col_name* ] **.plot** ( **kind** = '...' )

> * plot은 일반 선그래프를 나타난다
> * kind 옵션을 통해 원하는 그패프를 그릴 수 있다

<br />

**kind 옵션:**

 * line: 선 그래프

 * bar: 바 그래프

 * barh: 수평 바 프래프

 * hist: 히스토르램

 * kde: 커널 밀도 그래프

 * hexbin: 고밀도 산점도 그래프

 * box: 박스 플롯

 * area: 면적 그래프

 * pie: 파이 그래프

 * scatter: 산점도 그래프

   <br /> 

### line 그래프

> line 그래프는 데이터가 연속적인 경우 사용하기 적절하다. (예를 들면, 주가 데이터)

  <br />


```python
df
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
      <th>지역</th>
      <th>규모</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>4</th>
      <td>인천</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>3488</td>
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
      <th>3288</th>
      <td>경남</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3065</td>
    </tr>
    <tr>
      <th>3289</th>
      <td>경남</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3247</td>
    </tr>
    <tr>
      <th>3290</th>
      <td>제주</td>
      <td>60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>4039</td>
    </tr>
    <tr>
      <th>3291</th>
      <td>제주</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3962</td>
    </tr>
    <tr>
      <th>3292</th>
      <td>제주</td>
      <td>102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>3601</td>
    </tr>
  </tbody>
</table>
<p>3293 rows × 5 columns</p>

</div>



<br />  

**(1) 모든 observation의 분양가 살펴보기**


```python
# index - 분양가
df["분양가"].plot(kind = 'line')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f01a0bc8>




![png](/images/S-Python-Pandas-visual/output_38_1.png)

<br />


**(2) 연도에 따른 서울 분양가 변화 추세**


```python
# select "서울" data
df_seoul = df.loc[df["지역"] == "서울"]
df_seoul
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
      <th>지역</th>
      <th>규모</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>64</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>11</td>
      <td>6320</td>
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
      <th>3178</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2020</td>
      <td>1</td>
      <td>8779</td>
    </tr>
    <tr>
      <th>3234</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>8193</td>
    </tr>
    <tr>
      <th>3235</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>8140</td>
    </tr>
    <tr>
      <th>3236</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>13835</td>
    </tr>
    <tr>
      <th>3237</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>9039</td>
    </tr>
  </tbody>
</table>
<p>212 rows × 5 columns</p>

</div>

<br />


```python
# group by "year" 
df_seoul_year = df_seoul.groupby('연도').mean()
df_seoul_year
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
      <th>월</th>
      <th>분양가</th>
    </tr>
    <tr>
      <th>연도</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015</th>
      <td>11.0</td>
      <td>6201.000000</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>6.5</td>
      <td>6674.520833</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>6.5</td>
      <td>6658.729167</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>6.5</td>
      <td>7054.687500</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>6.5</td>
      <td>8735.083333</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>1.5</td>
      <td>9647.375000</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
# line plot
df_seoul_year["분양가"].plot(kind = 'line')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f028b5c8>




![png](/images/S-Python-Pandas-visual/output_43_1.png)

<br />


### bar 그래프

> bar 그패프는 그룹별로 비교할 때 유용하다

 <br /> 

**지역별 평균 분양가 살펴보기**


```python
df.groupby("지역")["분양가"].mean()
```


    지역
    강원    2448.156863
    경기    4133.952830
    경남    2858.932367
    경북    2570.465000
    광주    3055.043750
    대구    3679.620690
    대전    3176.127389
    부산    3691.981132
    서울    7308.943396
    세종    2983.543147
    울산    2990.373913
    인천    3684.302885
    전남    2326.250000
    전북    2381.416268
    제주    3472.677966
    충남    2534.950000
    충북    2348.183962
    Name: 분양가, dtype: float64

<br />


```python
# 수직 바 그래프
df.groupby("지역")["분양가"].mean().plot(kind = 'bar')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f028b548>




![png](/images/S-Python-Pandas-visual/output_50_1.png)

<br />

```python
# 수평 바 그래프
df.groupby("지역")["분양가"].mean().plot(kind = 'barh')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179edd9d4c8>




![png](/images/S-Python-Pandas-visual/output_51_1.png)

<br />


### 히스토그램 (hist)

> 히스토그램은 **분포-빈도 를 시각화**하여 보여준다.  
> 가로축에는 분포를, 세로축에는 빈도가 시각화되어 보여짐.

  <br />


```python
df["분양가"].plot(kind = "hist")
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f021cc88>




![png](/images/S-Python-Pandas-visual/output_56_1.png)

<br />


### 커널 밀도 그래프 (kde)

> * 히스토그램과 유사하게 밀도를 보여주는 그래프다
> * 히스토그램과 유사한 모양새를 각추고 있다
> * 하지만 히스토그램과 다르게 부드러운 라인을 가지고 있다

  <br />


```python
df["분양가"].plot(kind = "kde")
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f043d608>




![png](/images/S-Python-Pandas-visual/output_61_1.png)

<br />


### 고밀도 산점도 그래프 (hexbin)

> * hexbin은 고밀고 산점도 그래프다
> * x와 y 키 값을 넣어 주어야 한다
> * x, y 값 모두 numeric value 이어야한다
> * 데이터의 밀도를 추정한다

  <br />


```python
df.plot(kind = "hexbin", x = "분양가", y = "연도", gridsize = 20)
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f028a9c8>




![png](/images/S-Python-Pandas-visual/output_66_1.png)

<br />


### 박스 플롯 (box)


```python
df_seoul = df.loc[df["지역"] == "서울"]
```


```python
df_seoul["분양가"].plot(kind = "box")
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f226d748>




![png](/images/S-Python-Pandas-visual/output_70_1.png)

<br />


**box plot 해석**

![box plot 해석](/images/S-Python-Pandas-visual/R800x0)

  <br />

* __IQR (Inter Quantile Range)__   = 3Q - 1Q

* __Upper fence__ = 75th Percentile + 1.5*IQR

* __Lower fence__ = 25th Percentile - 1.5*IQR

  <br />

box plot은 데이터 outlier 감지할 때 가장 많이 활용되며, 25%, median, 75% 분위값을 활용하는 용도로도 많이 활용된다

  <br />

### area plot

> area plot은 line 그래프에서 아래 area를 모두 색칠해 주는 것이 특징이다.

<br />

```python
df
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
      <th>지역</th>
      <th>규모</th>
      <th>연도</th>
      <th>월</th>
      <th>분양가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5652</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5882</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>5721</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울</td>
      <td>102㎡초과</td>
      <td>2015</td>
      <td>10</td>
      <td>5879</td>
    </tr>
    <tr>
      <th>4</th>
      <td>인천</td>
      <td>60㎡이하</td>
      <td>2015</td>
      <td>10</td>
      <td>3488</td>
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
      <th>3288</th>
      <td>경남</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3065</td>
    </tr>
    <tr>
      <th>3289</th>
      <td>경남</td>
      <td>85㎡초과 102㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3247</td>
    </tr>
    <tr>
      <th>3290</th>
      <td>제주</td>
      <td>60㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>4039</td>
    </tr>
    <tr>
      <th>3291</th>
      <td>제주</td>
      <td>60㎡초과 85㎡이하</td>
      <td>2020</td>
      <td>2</td>
      <td>3962</td>
    </tr>
    <tr>
      <th>3292</th>
      <td>제주</td>
      <td>102㎡초과</td>
      <td>2020</td>
      <td>2</td>
      <td>3601</td>
    </tr>
  </tbody>
</table>
<p>3293 rows × 5 columns</p>

</div>



 <br /> 


```python
df.groupby("월")["분양가"].count().plot(kind = "line")
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f22a6688>




![png](/images/S-Python-Pandas-visual/output_83_1.png)

<br />

```python
df.groupby("월")["분양가"].count().plot(kind = "area")
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f2267588>




![png](/images/S-Python-Pandas-visual/output_84_1.png)

<br />


### 파이 그래프 (pie plot)

> pie는 대표적으로 데이터의 점유율을 보유줄 때 유용하다

<br />  

**연도별 분양가 데이터 점유율**


```python
df.groupby("연도")["분양가"].count().plot(kind = 'pie')
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f224fec8>




![png](/images/S-Python-Pandas-visual/output_90_1.png)

<br />


### 산점도 그래프 (scatter plot)

> * 점으로 데이터를 표기해준다
> * x, y값을 넣어주어야한다 (hexbin과 유사)
> * x축과 y축을 지정해주면 그에 맞는 데이터 분포를 볼 수 있다
> * 역시 numeric column 만 지정할 수 있다

  <br />


```python
df.plot(x = "월", y = "분양가", kind = "scatter")
```


    <matplotlib.axes._subplots.AxesSubplot at 0x179f23372c8>




![png](/images/S-Python-Pandas-visual/output_95_1.png)

<br />

<br />
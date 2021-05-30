---
title: Python >> Pandas 전처리 - (3) DataFrame의 합침 및 병합
tags:
  - Python
  - Pandas
  - 전처리
categories: 
  - [【STUDY - Python】, Python - 2. Pandas]
  - [【STUDY - Python】, Python - 전처리]
cover: 'https://s1.ax1x.com/2020/05/22/YjVKwF.png'
description: DataFrame 합치기 (concat); DataFrame 병합하기 (merge)
abbrlink: 57901
date: 2020-06-19 15:52:54
---

# DataFrame의 합침 및 병합

@[toc]

<br />

  


```python
import pandas as pd
```


```python
df = pd.read_csv('korean-idol.csv')
```


```python
df2 = pd.read_csv('korean-idol-2.csv')
```

  <br />

<br />

  

## **1. DataFrame 합치기 (concat)**

### 1-1. Row 기준 합치기 (밑으로 합침)

> *df_concat* = **pd.concat** ( [ *df_name1* , *df_name2* ], sort = False)  
> *df_concat* **.reset_index** (drop = True)

> * 합칠 데이터프리임을 list로 묶어준다.
> * **sort=False 옵션**을 주어 column의 순서가 유지되도록 한다
> * 합친 dataframe을 새 변수에 대입한 뒤 **reset_index 옵션**으로 index를 초기화한다 (아님 각각 원래의 index을 가지고 있음)
> * reseet_index에서 **drop=True 옵션**을 사용해 원래의 행 index가 새로 index column으로 생성되지 않도록 한다

<br />

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

<table>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
  </tbody>
</table>

</div>




```python
df_copy = df.copy()
```

  <br />

**(1) sort 옵션**

**sort = False:** column 순서 유지;  
**sort = True:** column을 이름순으로 재정열 


```python
pd.concat([df, df_copy], sort = False)
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

<table>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>




```python
pd.concat([df, df_copy], sort = True)
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
      <th>그룹</th>
      <th>브랜드평판지수</th>
      <th>생년월일</th>
      <th>성별</th>
      <th>소속사</th>
      <th>이름</th>
      <th>키</th>
      <th>혈액형</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>방탄소년단</td>
      <td>10523260</td>
      <td>1995-10-13</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>지민</td>
      <td>173.6</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>빅뱅</td>
      <td>9916947</td>
      <td>1988-08-18</td>
      <td>남자</td>
      <td>YG</td>
      <td>지드래곤</td>
      <td>177.0</td>
      <td>A</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8273745</td>
      <td>1996-12-10</td>
      <td>남자</td>
      <td>커넥트</td>
      <td>강다니엘</td>
      <td>180.0</td>
      <td>A</td>
    </tr>
    <tr>
      <th>3</th>
      <td>방탄소년단</td>
      <td>8073501</td>
      <td>1995-12-30</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>뷔</td>
      <td>178.0</td>
      <td>AB</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마마무</td>
      <td>7650928</td>
      <td>1995-07-23</td>
      <td>여자</td>
      <td>RBW</td>
      <td>화사</td>
      <td>162.1</td>
      <td>A</td>
    </tr>
    <tr>
      <th>5</th>
      <td>방탄소년단</td>
      <td>5208335</td>
      <td>1997-09-01</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>정국</td>
      <td>178.0</td>
      <td>A</td>
    </tr>
    <tr>
      <th>6</th>
      <td>뉴이스트</td>
      <td>4989792</td>
      <td>1995-08-09</td>
      <td>남자</td>
      <td>플레디스</td>
      <td>민현</td>
      <td>182.3</td>
      <td>O</td>
    </tr>
    <tr>
      <th>7</th>
      <td>아이들</td>
      <td>4668615</td>
      <td>1998-08-26</td>
      <td>여자</td>
      <td>큐브</td>
      <td>소연</td>
      <td>NaN</td>
      <td>B</td>
    </tr>
    <tr>
      <th>8</th>
      <td>방탄소년단</td>
      <td>4570308</td>
      <td>1992-12-04</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>진</td>
      <td>179.2</td>
      <td>O</td>
    </tr>
    <tr>
      <th>9</th>
      <td>핫샷</td>
      <td>4036489</td>
      <td>1994-03-22</td>
      <td>남자</td>
      <td>스타크루이엔티</td>
      <td>하성운</td>
      <td>167.1</td>
      <td>A</td>
    </tr>
    <tr>
      <th>10</th>
      <td>소녀시대</td>
      <td>3918661</td>
      <td>1989-03-09</td>
      <td>여자</td>
      <td>SM</td>
      <td>태연</td>
      <td>NaN</td>
      <td>A</td>
    </tr>
    <tr>
      <th>11</th>
      <td>아스트로</td>
      <td>3506027</td>
      <td>1997-03-30</td>
      <td>남자</td>
      <td>판타지오</td>
      <td>차은우</td>
      <td>183.0</td>
      <td>B</td>
    </tr>
    <tr>
      <th>12</th>
      <td>뉴이스트</td>
      <td>3301654</td>
      <td>1995-07-21</td>
      <td>남자</td>
      <td>플레디스</td>
      <td>백호</td>
      <td>175.0</td>
      <td>AB</td>
    </tr>
    <tr>
      <th>13</th>
      <td>뉴이스트</td>
      <td>3274137</td>
      <td>1995-06-08</td>
      <td>남자</td>
      <td>플레디스</td>
      <td>JR</td>
      <td>176.0</td>
      <td>O</td>
    </tr>
    <tr>
      <th>14</th>
      <td>방탄소년단</td>
      <td>2925442</td>
      <td>1993-03-09</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>슈가</td>
      <td>174.0</td>
      <td>O</td>
    </tr>
    <tr>
      <th>0</th>
      <td>방탄소년단</td>
      <td>10523260</td>
      <td>1995-10-13</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>지민</td>
      <td>173.6</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>빅뱅</td>
      <td>9916947</td>
      <td>1988-08-18</td>
      <td>남자</td>
      <td>YG</td>
      <td>지드래곤</td>
      <td>177.0</td>
      <td>A</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8273745</td>
      <td>1996-12-10</td>
      <td>남자</td>
      <td>커넥트</td>
      <td>강다니엘</td>
      <td>180.0</td>
      <td>A</td>
    </tr>
    <tr>
      <th>3</th>
      <td>방탄소년단</td>
      <td>8073501</td>
      <td>1995-12-30</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>뷔</td>
      <td>178.0</td>
      <td>AB</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마마무</td>
      <td>7650928</td>
      <td>1995-07-23</td>
      <td>여자</td>
      <td>RBW</td>
      <td>화사</td>
      <td>162.1</td>
      <td>A</td>
    </tr>
    <tr>
      <th>5</th>
      <td>방탄소년단</td>
      <td>5208335</td>
      <td>1997-09-01</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>정국</td>
      <td>178.0</td>
      <td>A</td>
    </tr>
    <tr>
      <th>6</th>
      <td>뉴이스트</td>
      <td>4989792</td>
      <td>1995-08-09</td>
      <td>남자</td>
      <td>플레디스</td>
      <td>민현</td>
      <td>182.3</td>
      <td>O</td>
    </tr>
    <tr>
      <th>7</th>
      <td>아이들</td>
      <td>4668615</td>
      <td>1998-08-26</td>
      <td>여자</td>
      <td>큐브</td>
      <td>소연</td>
      <td>NaN</td>
      <td>B</td>
    </tr>
    <tr>
      <th>8</th>
      <td>방탄소년단</td>
      <td>4570308</td>
      <td>1992-12-04</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>진</td>
      <td>179.2</td>
      <td>O</td>
    </tr>
    <tr>
      <th>9</th>
      <td>핫샷</td>
      <td>4036489</td>
      <td>1994-03-22</td>
      <td>남자</td>
      <td>스타크루이엔티</td>
      <td>하성운</td>
      <td>167.1</td>
      <td>A</td>
    </tr>
    <tr>
      <th>10</th>
      <td>소녀시대</td>
      <td>3918661</td>
      <td>1989-03-09</td>
      <td>여자</td>
      <td>SM</td>
      <td>태연</td>
      <td>NaN</td>
      <td>A</td>
    </tr>
    <tr>
      <th>11</th>
      <td>아스트로</td>
      <td>3506027</td>
      <td>1997-03-30</td>
      <td>남자</td>
      <td>판타지오</td>
      <td>차은우</td>
      <td>183.0</td>
      <td>B</td>
    </tr>
    <tr>
      <th>12</th>
      <td>뉴이스트</td>
      <td>3301654</td>
      <td>1995-07-21</td>
      <td>남자</td>
      <td>플레디스</td>
      <td>백호</td>
      <td>175.0</td>
      <td>AB</td>
    </tr>
    <tr>
      <th>13</th>
      <td>뉴이스트</td>
      <td>3274137</td>
      <td>1995-06-08</td>
      <td>남자</td>
      <td>플레디스</td>
      <td>JR</td>
      <td>176.0</td>
      <td>O</td>
    </tr>
    <tr>
      <th>14</th>
      <td>방탄소년단</td>
      <td>2925442</td>
      <td>1993-03-09</td>
      <td>남자</td>
      <td>빅히트</td>
      <td>슈가</td>
      <td>174.0</td>
      <td>O</td>
    </tr>
  </tbody>
</table>

</div>



  <br />

**(2) reset_index 옵션**

**reset_index():** index가 초기화됨, 원래의 index가 새로 index column으로 저장됨  
**reset_index(drop = True):**  index가 초기화됨, 원래의 index가 새로 index column으로 생성되지 않음


```python
df_concat = pd.concat([df, df_copy], sort = False)
```


```python
df_concat.reset_index()
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
      <th>index</th>
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0</td>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1</td>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2</td>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>18</th>
      <td>3</td>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>19</th>
      <td>4</td>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>20</th>
      <td>5</td>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>21</th>
      <td>6</td>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>22</th>
      <td>7</td>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>23</th>
      <td>8</td>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>24</th>
      <td>9</td>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>25</th>
      <td>10</td>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>26</th>
      <td>11</td>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>27</th>
      <td>12</td>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>28</th>
      <td>13</td>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>29</th>
      <td>14</td>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>




```python
df_concat.reset_index(drop = True)
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
    <tr>
      <th>15</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>16</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>17</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>18</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>19</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>20</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>21</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>22</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>23</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>24</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>25</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>26</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>27</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>28</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>29</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>



  <br />

<br />

  

### 1-2. column 기준으로 합치기 (옆으로 합침)

> column 기준으로 합치고자 할 때는 **axis = 1 옵션**을 준다:  
> **pd.concat** ( [*df_name1*, *df_name2*], **axis = 1**)


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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
  </tbody>
</table>

</div>




```python
df2 = pd.read_csv('korean-idol-2.csv')
```


```python
df2.head()
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
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>3500</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>3050</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> 


```python
pd.concat([df, df2], axis = 1)
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
      <td>지드래곤</td>
      <td>3500</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
      <td>뷔</td>
      <td>3050</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
      <td>정국</td>
      <td>2900</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
      <td>민현</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
      <td>소연</td>
      <td>4500</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
      <td>진</td>
      <td>4200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
      <td>하성운</td>
      <td>4300</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
      <td>태연</td>
      <td>3700</td>
      <td>3</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
      <td>차은우</td>
      <td>3850</td>
      <td>5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
      <td>백호</td>
      <td>3900</td>
      <td>4</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
      <td>JR</td>
      <td>4100</td>
      <td>3</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
      <td>슈가</td>
      <td>4150</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> 

> 행의 갯수가 맞지 않을 시 
>
> * 두 DataFrame이 행 index기준으로 합치게 됨
> * 행 갯수가 적은 DataFrame의 빈칸에는 NaN로 채워지게 됨


```python
df3 = df2.drop([3,5])
df3
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
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>3500</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>4500</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>4200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>4300</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>3700</td>
      <td>3</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>3850</td>
      <td>5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>3900</td>
      <td>4</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>4100</td>
      <td>3</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>4150</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>




```python
pd.concat([df, df3], axis = 1)
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
      <td>지민</td>
      <td>3000.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
      <td>지드래곤</td>
      <td>3500.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
      <td>강다니엘</td>
      <td>3200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
      <td>화사</td>
      <td>4300.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
      <td>민현</td>
      <td>3400.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
      <td>소연</td>
      <td>4500.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
      <td>진</td>
      <td>4200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
      <td>하성운</td>
      <td>4300.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
      <td>태연</td>
      <td>3700.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
      <td>차은우</td>
      <td>3850.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
      <td>백호</td>
      <td>3900.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
      <td>JR</td>
      <td>4100.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
      <td>슈가</td>
      <td>4150.0</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
df4 = df2.drop([13, 14])
pd.concat([df,df4], axis = 1)
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
      <td>지민</td>
      <td>3000.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
      <td>지드래곤</td>
      <td>3500.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
      <td>강다니엘</td>
      <td>3200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
      <td>뷔</td>
      <td>3050.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
      <td>화사</td>
      <td>4300.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
      <td>정국</td>
      <td>2900.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
      <td>민현</td>
      <td>3400.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
      <td>소연</td>
      <td>4500.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
      <td>진</td>
      <td>4200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
      <td>하성운</td>
      <td>4300.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
      <td>태연</td>
      <td>3700.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
      <td>차은우</td>
      <td>3850.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
      <td>백호</td>
      <td>3900.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

</div>



<br />

<br />  

## **2. DataFrame 병합하기 (merge)**

> **concat과 merge의 차이:**
>
> * **concat:** row 나 column 기준으로 단순하게 이어 붙히기
> * **merge:** 특정 고유한 키(unique id) 값을 기준으로 병합하기

<br />

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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
  </tbody>
</table>

</div>




```python
df2.head()
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
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>3500</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>3050</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



<br />

df와 df2는 **"이름"이라는 column이 겹친다**  
따라서, 우리는 "이름"을 기준으로 두 DataFrame을 **병합**할 수 있다

> **pd.merge (*left_df*, *right_df*, on = "기준 column", how = "..." )**
>
> * left_df와 right_df 에는 병합할 두 DataFrame을 대입한다
> * on 에는 병합의 기준이 되는 column을 넣어 준다
> * how 에는 'left', 'right', 'inner', 'outer'라는 4가지의 병합 방식중 한가지를 택한다

<br />  

### 2-0. 예제 데이터 만들기


```python
df_right = df2.drop([1,3,5,7])
```


```python
df_right
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
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>4200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>4300</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>3700</td>
      <td>3</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>3850</td>
      <td>5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>3900</td>
      <td>4</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>4100</td>
      <td>3</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>4150</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>




```python
df_right = df_right.reset_index(drop = True)
df_right
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
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>민현</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>진</td>
      <td>4200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>하성운</td>
      <td>4300</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>태연</td>
      <td>3700</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>차은우</td>
      <td>3850</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>백호</td>
      <td>3900</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>JR</td>
      <td>4100</td>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>슈가</td>
      <td>4150</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>




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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>



 <br /> 

**concat로 합치는 경우:**  
데이터가 행 index기준으로 합치게 되기 때문에 **이름이 다른 시람의 데이터가 합치게 된다**


```python
pd.concat([df, df_right], axis = 1)
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
      <td>지민</td>
      <td>3000.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
      <td>강다니엘</td>
      <td>3200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
      <td>화사</td>
      <td>4300.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
      <td>민현</td>
      <td>3400.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
      <td>진</td>
      <td>4200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
      <td>하성운</td>
      <td>4300.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
      <td>태연</td>
      <td>3700.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
      <td>차은우</td>
      <td>3850.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
      <td>백호</td>
      <td>3900.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
      <td>JR</td>
      <td>4100.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
      <td>슈가</td>
      <td>4150.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

</div>

<br />

따리서, 우리는 merge를 사용하여 두 DataFrame를 "이름" 기준으로 병합한다

 <br /> 

### 2-1. left, right 방식

> * "left"옵션을 부여할 때: left DataFrame에 키 값이 존재하면 해당 데이터를 유지하고, 병합한 right DataFrame의 값은 NaN이 대입 됨
> * 반대로, "right"옵션을 부여할 때 right DataFrame을 기준으로 병합하게 됨

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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>




```python
df_right
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
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>민현</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>진</td>
      <td>4200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>하성운</td>
      <td>4300</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>태연</td>
      <td>3700</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>차은우</td>
      <td>3850</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>백호</td>
      <td>3900</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>JR</td>
      <td>4100</td>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>슈가</td>
      <td>4150</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
pd.merge(df, df_right, on = "이름", how = "left")
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
      <td>3000.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
      <td>3200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
      <td>4300.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
      <td>3400.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
      <td>4200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
      <td>4300.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
      <td>3700.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
      <td>3850.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
      <td>3900.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
      <td>4100.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
      <td>4150.0</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>

</div>




```python
pd.merge(df, df_right, on = "이름", how = "right")
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
      <td>4200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
      <td>4300</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
      <td>3700</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
      <td>3850</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
      <td>3900</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
      <td>4100</td>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
      <td>4150</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>

<br />

현재, left DataFrame이 더 많은 데이터를 보유하고 있으니, right를 기준으로 병합하면 DataFrame 사이즈가 줄어드게 된다

 <br /> 

### 2-2. inner, outer 방식  

> * inner 방식은 두 DataFrame에 **모두 키 값이 존재**하는 경우만 병합한다 (교집합과 비슷)
> * outer 방식은 **하나의 DataFrame에만 키 값이 존재**하더라도 모두 병합한다 (합집합과 비슷)
> * outer 방식에서는 없는 값은 NaN으로 대입된다

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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
    </tr>
  </tbody>
</table>

</div>




```python
df_right
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
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>민현</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>진</td>
      <td>4200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>하성운</td>
      <td>4300</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>태연</td>
      <td>3700</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>차은우</td>
      <td>3850</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>백호</td>
      <td>3900</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>JR</td>
      <td>4100</td>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>슈가</td>
      <td>4150</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>

<br />


```python
pd.merge(df, df_right, on = "이름", how = 'inner')
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
      <td>4200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
      <td>4300</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
      <td>3700</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
      <td>3850</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
      <td>3900</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
      <td>4100</td>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
      <td>4150</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

</div>




```python
pd.merge(df, df_right, on = "이름", how = 'outer')
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
      <td>3000.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
      <td>3200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
      <td>4300.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
      <td>3400.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
      <td>4200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
      <td>4300.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
      <td>3700.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
      <td>3850.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
      <td>3900.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
      <td>4100.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
      <td>4150.0</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

### 2-3. column명은 다르지만, 동일한 성질의 데이터 인 경우?  

> **pd.merge** ( *left_df*, *right_df*, **left_on = "*left_col*", right_on = "*right_col*"**, how = "..." )

<br />

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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
    </tr>
  </tbody>
</table>

</div>




```python
df_right.head()
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
      <th>이름</th>
      <th>연봉</th>
      <th>가족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>민현</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>진</td>
      <td>4200</td>
      <td>4</td>
    </tr>
  </tbody>
</table>

</div>




```python
df_right.columns = ["성함", "연봉", "기족수"]
```


```python
df_right.head()
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
      <th>성함</th>
      <th>연봉</th>
      <th>기족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>3000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강다니엘</td>
      <td>3200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>화사</td>
      <td>4300</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>민현</td>
      <td>3400</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>진</td>
      <td>4200</td>
      <td>4</td>
    </tr>
  </tbody>
</table>

</div>



<br />  

df의 "이름"과  df_right의 "성함"은 column name이 다르지만, 동일한 성질의 데이터다.  
이럴 때는 left_on, right_on 옵션을 사용해 기준 column을 지정한다


```python
pd.merge(df, df_right, left_on = "이름", right_on = "성함", how = "outer")
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
      <th>이름</th>
      <th>그룹</th>
      <th>소속사</th>
      <th>성별</th>
      <th>생년월일</th>
      <th>키</th>
      <th>혈액형</th>
      <th>브랜드평판지수</th>
      <th>성함</th>
      <th>연봉</th>
      <th>기족수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>지민</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-10-13</td>
      <td>173.6</td>
      <td>A</td>
      <td>10523260</td>
      <td>지민</td>
      <td>3000.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>지드래곤</td>
      <td>빅뱅</td>
      <td>YG</td>
      <td>남자</td>
      <td>1988-08-18</td>
      <td>177.0</td>
      <td>A</td>
      <td>9916947</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강다니엘</td>
      <td>NaN</td>
      <td>커넥트</td>
      <td>남자</td>
      <td>1996-12-10</td>
      <td>180.0</td>
      <td>A</td>
      <td>8273745</td>
      <td>강다니엘</td>
      <td>3200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뷔</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1995-12-30</td>
      <td>178.0</td>
      <td>AB</td>
      <td>8073501</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>화사</td>
      <td>마마무</td>
      <td>RBW</td>
      <td>여자</td>
      <td>1995-07-23</td>
      <td>162.1</td>
      <td>A</td>
      <td>7650928</td>
      <td>화사</td>
      <td>4300.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>정국</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1997-09-01</td>
      <td>178.0</td>
      <td>A</td>
      <td>5208335</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>민현</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-08-09</td>
      <td>182.3</td>
      <td>O</td>
      <td>4989792</td>
      <td>민현</td>
      <td>3400.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>소연</td>
      <td>아이들</td>
      <td>큐브</td>
      <td>여자</td>
      <td>1998-08-26</td>
      <td>NaN</td>
      <td>B</td>
      <td>4668615</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>진</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1992-12-04</td>
      <td>179.2</td>
      <td>O</td>
      <td>4570308</td>
      <td>진</td>
      <td>4200.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>하성운</td>
      <td>핫샷</td>
      <td>스타크루이엔티</td>
      <td>남자</td>
      <td>1994-03-22</td>
      <td>167.1</td>
      <td>A</td>
      <td>4036489</td>
      <td>하성운</td>
      <td>4300.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>태연</td>
      <td>소녀시대</td>
      <td>SM</td>
      <td>여자</td>
      <td>1989-03-09</td>
      <td>NaN</td>
      <td>A</td>
      <td>3918661</td>
      <td>태연</td>
      <td>3700.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>차은우</td>
      <td>아스트로</td>
      <td>판타지오</td>
      <td>남자</td>
      <td>1997-03-30</td>
      <td>183.0</td>
      <td>B</td>
      <td>3506027</td>
      <td>차은우</td>
      <td>3850.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>백호</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-07-21</td>
      <td>175.0</td>
      <td>AB</td>
      <td>3301654</td>
      <td>백호</td>
      <td>3900.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>JR</td>
      <td>뉴이스트</td>
      <td>플레디스</td>
      <td>남자</td>
      <td>1995-06-08</td>
      <td>176.0</td>
      <td>O</td>
      <td>3274137</td>
      <td>JR</td>
      <td>4100.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>슈가</td>
      <td>방탄소년단</td>
      <td>빅히트</td>
      <td>남자</td>
      <td>1993-03-09</td>
      <td>174.0</td>
      <td>O</td>
      <td>2925442</td>
      <td>슈가</td>
      <td>4150.0</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>

</div>

<br />

<br />
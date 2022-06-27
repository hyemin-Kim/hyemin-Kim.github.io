---
title: Tableau >> Intermediate (11) Filtering and LOD Expression
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 61762
date: 2022-06-27 14:31:28
---

# Filtering and LOD Expression

@[toc]

<br />

## **1. Level of Details (LOD) Expression**

우리가 [Measure]필드를 View에 추가했을 때 Tableau는 자동으로 [Measure]의 집계값을 계산하여 보여줍니다.
집계의 기준이 기본적으로 [View에 있는 최하위 세부 수준]으로 되어 있습니다.

하지만 만약에 우리가 다른 기준으로 집계하고 싶다면 어떻게 해야할까요?
이런 경우에 LoD 계산식을 이용하면 됩니다!

<br />

**LoD 계산식 :** View에 있는 최하위 세부수준(LoD)과 **<font color = 'darkblue'>다른</font>** 세부수준 (Grouping 기준)으로 집계하고 싶은 경우에 사용

1. **FIXED():** View에 있는 세부수준을 **<font color = 'darkblue'>무시</font>**하고 원하는 그룹핑 기준 (세부수준)을 **<font color = 'darkblue'>직접 정하</font>**고 싶을 때

2. **INCLUDE():** View에 없는 세부수준을 **<font color = 'darkblue'>추가</font>**하고 싶을 때

3. **EXCLUDE():** View에 있는 일부 세부수준을 **<font color = 'darkblue'>제거</font>**하고 싶을 때

<br />

​															**각 LoD 계산식을 적용했을 때 실제 집계 시 사용되는 집계 기준**

|                |    View에 있는 최하위 세부수준 보다    |                          |
| :------------: | :------------------------------------: | :----------------------: |
|                |        **A가 더 상위수준일 때**        | **A가 더 하위수준일 때** |
|  **FIXED(A)**  |                   A                    |            A             |
| **INCLUDE(A)** |      View에 있는 최하위 세부수준       |            A             |
| **EXCLUDE(A)** | A를 제외한 View에 있는 최하위 세부수준 |         해당없음         |

<br />

<br />

## **2. Using LOD Expression with Filters**

**Order of Filters：**

<img src="/images/S-Tableau-Intermediate-11-Filtering-and-LOD-Expression/image-20210610165738698.png" alt="image-20210610165738698" style="zoom: 50%;" />

<br />

<br />

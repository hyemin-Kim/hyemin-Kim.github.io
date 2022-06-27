---
title: Tableau >> Intermediate (10) Controlling Table Calculations
date: 2022-06-27 14:17:18
tags:
 - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
---

# Controlling Table Calculations

@[toc]

<br />

## **1. Scope and Direction**

Table calculations are performed with a scope and direction. The scope and direction make the results relative to other data in the view.

<br />

**Options for scope:** 

* Table

* Pane: *Panes are created when multiple dimensions are used in the view*

* Cell

  <img src="/images/S-Tableau-Intermediate-10-Controlling-Table-Calculations/image-20210609161229115.png" alt="image-20210609161229115" style="zoom: 40%;" /> 

<br />

**Options for direction:**

* across
* down
* across then down (only available in specific contexts)
* down then across (only available in specific contexts)

​                            **across then down**                                                                                **down then across**

​	<img src="/images/S-Tableau-Intermediate-10-Controlling-Table-Calculations/image-20210609162057744.png" alt="image-20210609162057744" style="zoom: 60%;" />				<img src="D:\1. 아이투맥스\3. Tableau 학습\Typora Note\E_Analyst\3. Intermediate\3-10. Controlling Table Calculations.assets\image-20210609162020611.png" alt="image-20210609162020611" style="zoom: 60%;" />

<br />

<br />

## **2. Table Calculations with Null Values**

If there are null values in the table calculations:

* In some cases, like [Running Total], the null value gets skipped over. Regardless of the scope and direction I pick, the nulls are just treated like zeros, which is fine.
* But in some cases like [Difference From], there will be a bunch of blank values at the beginning since there is no previous value to compare to

<br />

In the second situation, we'll get an indicator (<img src="/images/S-Tableau-Intermediate-10-Controlling-Table-Calculations/image-20210609163417803.png" alt="image-20210609163417803" style="zoom:67%;" />) that there are blank values.   

If clicking the indicator about the nulls, 

* using [Filter Data] will show only non-null values on the table calculation

* using [Show data at default position] will make the null values shown as zeros 

  <img src="/images/S-Tableau-Intermediate-10-Controlling-Table-Calculations/image-20210609163533924.png" alt="image-20210609163533924" style="zoom:67%;" /> 

<br />

<br />

---
title: Tableau >> Intermediate (9) Advanced Calculations Aggregating Dimensions
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 456
date: 2022-06-27 14:13:32
---

# Advanced Calculations: Aggregating Dimensions

@[toc]

<br />

## 1. Three situations that dimension aggregations are needed

1. When blending multiple data sources
   * When blending multiple data sources in which the dimensions don't have a consistent level of detail, Tableau will aggregate the linked dimensions to the same level of detail
2. In calculations
   * When dimensions are used in calculations with aggregated measures, they must be aggregated
   * Tableau can't mix aggregate and non-aggregate comparisons in calculations
3. When you just want to know the aggregation of a dimension

<br />

## 2. Three ways to aggregate dimensions

1. Aggregated in a calculated field

2. Aggregated by right-clicking and dragging the dimension into the view

   ​							<img src="/images/S-Tableau-Intermediate-9-Advanced-Calculations-Aggregating-Dimensions/image-20210608162432334.png" alt="image-20210608162432334" style="zoom:80%;" /> 

3. Aggregated after they are added to the view by using the context menu

   [dimension] field --> drop-down menu --> Attribute / [Measure]

   ​		<img src="/images/S-Tableau-Intermediate-9-Advanced-Calculations-Aggregating-Dimensions/image-20210608162831618.png" alt="image-20210608162831618" style="zoom:80%;" />

<br />

<br />

## 3. Five types of aggregations that can be applied to dimensions

1. Minimum <font color = 'blue'>[dimension]</font>
   * returns the first alphabetic value (the top of the list)
2. Maximum <font color = 'blue'>[dimension]</font>
   * returns the last alphabetic value (the last of the list)
3. Count <font color = 'viridens'>[measure]</font>
   * returns the total number of entries in the field
4. Count (Distinct) <font color = 'viridens'>[measure]</font>
   * returns the total number of unique entries in the field
5. Attribute
   * if it has a single value for all rows --> returns the value of the expression
   * otherwise --> returns an asterisk (*)

<br />

<br />

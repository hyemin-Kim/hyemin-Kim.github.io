---
title: Tableau >> Intermediate (7) Using Context Filters to Limit Scope
date: 2022-06-27 14:02:19
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
---

# Using Context Filters to Limit Scope

@[toc]

<br />

## **1. Concept**

By default, all filters set in Tableau are computed independently. That is, each filter accesses all rows in your data source without regard to other filters. However, you can set one or more categorical filters as context filters for the view.

A context filter will pre-filter the data to create a context for this worksheet, making other dimension and measure filters dependent on this result.

<br />

## **2. Creating Context Filter**

Use [Add To Context] function:

* field --> drop-down arrow --> [Add to Context]

  <img src="/images/S-Tableau-Intermediate-7-Using-Context-Filters-to-Limit-Scope/image-20210607172541543.png" alt="image-20210607172541543" style="zoom:80%;" /> 	 <img src="D:\1. 아이투맥스\3. Tableau 학습\Typora Note\E_Analyst\3. Intermediate\3-7. Using Context Filters to Limit Scope.assets\image-20210607172600720.png" alt="image-20210607172600720" style="zoom:80%;" />

<br />

<br />

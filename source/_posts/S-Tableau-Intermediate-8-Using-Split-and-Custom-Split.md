---
title: Tableau >> Intermediate (8) Using Split and Custom Split
tags: '-Tableau'
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 63576
date: 2022-06-27 14:04:54
---

# Using Split and Custom Split

@[toc]

<br />

## **1. Concept**

If you have string fields in your data that contain multiple units of information, you can use split or custom split options in Tableau to separate the values based on a separator or a repeated pattern of values present in each row of the field.

* [Split] : Split strings based on a default separator, like a space or a comma
* [Custom Split] : Split strings based on a custom separator

<br />

<br />

## **2. Using Splits**

### \>> Two places to create splits / custom splits

* On the Data Source Page:

  the dimension you want to split --> drop-down menu --> [Split] / [Custom Split]

  <img src="/images/S-Tableau-Intermediate-8-Using-Split-and-Custom-Split/image-20210608154104954.png" alt="image-20210608154104954" style="zoom:67%;" /> 	<img src="/images/S-Tableau-Intermediate-8-Using-Split-and-Custom-Split/image-20210608154203595-16563144840331.png" alt="image-20210608154203595" style="zoom:67%;" />

  <br />

* On the Data pane in the worksheet:

  right-click the dimension you want to split --> [Transform] --> [Split] / [Custom Split]

  <img src="/images/S-Tableau-Intermediate-8-Using-Split-and-Custom-Split/image-20210608154938851.png" alt="image-20210608154938851" style="zoom:67%;" /> 

  <br />

### \>> Custom splits

<img src="/images/S-Tableau-Intermediate-8-Using-Split-and-Custom-Split/image-20210608154337879-16563145155593.png" alt="image-20210608154337879" style="zoom:95%;" />		 <img src="/images/S-Tableau-Intermediate-8-Using-Split-and-Custom-Split/image-20210608154622042.png" alt="image-20210608154622042" style="zoom:80%;" />

* [Use the separator] : the specific separator to split fields
* [Split off] : the component of the fields you want to split off

<br />

<br />

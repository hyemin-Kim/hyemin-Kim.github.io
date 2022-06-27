---
title: Tableau >> Intermediate (2) Joining Tables
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 60079
date: 2022-06-27 13:32:43
---

# Joining Tables

@[toc]

<br />

## **1. Table joins**

### \>> 4 types of joins in Tableau

* inner joins  (default)
* left joins
* right joins
* full outer joins

<br />

### \>> How to join tables?

> [[Tableau Help] -- Join Your Data](https://help.tableau.com/current/pro/desktop/en-us/joining_tables.htm) ([中: 联接数据](https://help.tableau.com/current/pro/desktop/zh-cn/joining_tables.htm) / [한: 데이터 조인](https://help.tableau.com/current/pro/desktop/ko-kr/joining_tables.htm))

<br />

**Two situations :**

* **<font color = 'darkblue'>Join tables in the same data database</font>**

* **<font color = 'darkblue'>Join tables in different databases</font>**

  Connecting to multiple databases:

  * <font color = 'blue'>blue</font>:      primary database
  * <font color = 'orange'>orange</font>: secondary database

  <img src="/images/S-Tableau-Intermediate-2-Joining-Tables/image-20210603084026249.png" alt="image-20210603084026249" style="zoom:67%;" /> 

<br />

**How to join tables?**

1. Connect to the relevant data source or sources

2. Drag the first table to the canvas

3. Select [Open] from the menu or double-click the first table to open the join canvas

   <img src="/images/S-Tableau-Intermediate-2-Joining-Tables/image-20210603165714869.png" alt="image-20210603165714869" style="zoom: 50%;" /> 

   

   <img src="/images/S-Tableau-Intermediate-2-Joining-Tables/image-20210603165828247.png" alt="image-20210603165828247" style="zoom:50%;" /> 

   <br />

4. Double-click or drag another table to the join canvas

5. Select a join type --> Add one or more join clauses

   <img src="/images/S-Tableau-Intermediate-2-Joining-Tables/image-20210603170308172.png" alt="image-20210603170308172" style="zoom: 67%;" /> 

<br />

<br />

## **2. Joining Tables Using Calculations**

### \>> When we use Join calculations?

Join calculations are typically used to fix mismatched field types, or just a mismatch in the values in the two tables when adding the join clause.

We can use Join calculation to create a new field that match the field use for join clause in the other table 

<br />

**[Example]** 

We have [Name] field in table A, [First Name] and [Last Name] fields in table B. To join these two tables:

* Use Join calculation to create a new field "[Name]" for table B, which will be used for matching the [Name] field in table A

* Join calculation function:

  `[First Name] + " " + [Last Name]`

<br />

<br />

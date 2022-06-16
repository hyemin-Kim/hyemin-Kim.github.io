---
title: Tableau >> Fundamentals (8) Using Calculations
date: 2022-06-16 14:32:04
tags:
 - Tableau
categories:
 - 【STUDY - Tableau】
 - Tableau - 2. Fundamentals
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
---

# Using Calculations

@[toc]



## **1. Working with Strings and Type Conversion Functions**

#### Concatenate string fields

To concatenate strings means to add them together

* Use "+" operator to connect strings

  <img src="../images/S-Tableau-Fundamentals-8-Using-Calculations/image-20210528101257676.png" alt="image-20210528101257676" style="zoom:80%;" /> 

  

* For fields with other data types, use type conversion function "STR()" to change them into strings

  <img src="../images/S-Tableau-Fundamentals-8-Using-Calculations/image-20210528102740095.png" alt="image-20210528102740095" style="zoom:80%;" /> 

 



## **2. Working with Dates**

#### Using Date-specific Calculations

> [[Tableau Help] -- Date Functions](https://help.tableau.com/current/pro/desktop/en-us/functions_functions_date.htm)

**[Example - DATEDIFF]**

DATEDIFF: Returns the difference between two dates. The difference is expressed in units of date_part

<img src="../images/S-Tableau-Fundamentals-8-Using-Calculations/image-20210528104621973.png" alt="image-20210528104621973" style="zoom:80%;" />





## **3. Working with Aggregations**

When dragging [measure] fields into the view, Tableau automatically aggregates [measure] to the lowest level of detail in the view.



|                       Calculated Field                       |                     Bring into the view                      |                     Order of Operations                      |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| <img src="../images/S-Tableau-Fundamentals-8-Using-Calculations/image-20210528123951612.png" alt="image-20210528123951612" style="zoom:30%;" /> | <img src="../images/S-Tableau-Fundamentals-8-Using-Calculations/image-20210528124107136.png" alt="image-20210528124107136" style="zoom:40%;" /> | 1. calculate the ratio for each row<br/>2. sum the results of those ratios |
| <img src="../images/S-Tableau-Fundamentals-8-Using-Calculations/image-20210528124605478.png" alt="image-20210528124605478" style="zoom:30%;" /> | <img src="../images/S-Tableau-Fundamentals-8-Using-Calculations/image-20210528124624680.png" alt="image-20210528124624680" style="zoom:40%;" /> | 1. sum the Profit values and Sales values<br>2. divide two totals and calculate the ratio |

\* When you pre-define aggregation in a calculated field, Tableau won't perform further aggregation when you bring the field into the view. Instead, Tableau adds an "AGG" at the start of the field to indicate that the aggregation was pre-defined in the calculation.



**[calculation without aggregation]  VS  [calculation including aggregation]**

|                               |               calculation without aggregation                |              calculation including aggregation               |
| :---------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|          **Example**          | <img src="../images/S-Tableau-Fundamentals-8-Using-Calculations/image-20210528123951612.png" alt="image-20210528123951612" style="zoom:30%;" /> | <img src="../images/S-Tableau-Fundamentals-8-Using-Calculations/image-20210528124605478.png" alt="image-20210528124605478" style="zoom:30%;" /> |
|      **Level of Detail**      | 1. first performed at the row-level detail<br/>2. then aggregated and brought into the view |    the result will be at the level of detail in the view     |
| **Brought into <br>the view** |              perform aggregation automatically               |            further aggregation can't be performed            |


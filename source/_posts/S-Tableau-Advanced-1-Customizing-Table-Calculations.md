---
title: Tableau >> Advanced (1) Customizing Table Calculations
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 4. Advanced
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 14180
date: 2022-06-27 15:15:41
---

# Table Calculations

@[toc]

<br />

## **1. Including Helper Functions in Table Calculations**

### \>> Helper Functions  

You might need to write a custom table calculation when you want your calculation to reference another row or column of the table. To direct Tableau to the correct values, we can make use of **Helper functions**. 

Helper functions are special table calculations that can be used to point to a location of specific values in the data table. They're often combined with other expressions or functions to build more powerful calculations.

<br />

### \>> Four Helper Functions

* **INDEX():** Shows the current row of the partition

  Scope: Table  -->	<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210701092512144.png" alt="image-20210701092512144" style="zoom:80%;" />	     	 Scope: Pane  -- 	<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210701092656339-165631081898731.png" alt="image-20210701092656339" style="zoom:80%;" />

  <br />

* **FIRST():** Reports how far each cell is from the first cell in the partition	<font color = 'blue'>[ INDEX(FIRST) - INDEX(now) ]</font>

  Scope: Table  -->	<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210628170447588.png" alt="image-20210628170447588" style="zoom:80%;" />

  Scope: Pane   -->	<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210628170412602.png" alt="image-20210628170412602" style="zoom:80%;" />

  <br />

* **LAST():** Reports how far each cell is from the last cell in the partition     <font color = 'blue'>[ INDEX(LAST) - INDEX(now) ]</font>

  Scope: Table  -->	<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210701091652724.png" alt="image-20210701091652724" style="zoom:80%;" />

  Scope: Pane   -->	<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210701091812692.png" alt="image-20210701091812692" style="zoom:80%;" />

  <br />

* **SIZE():** Returns the number of rows in the current scope

  **<font color = 'darkblue'>SIZE()</font>** returns 12 if the current part of the table shows sales for months in a year

<br />

<br />

### \>> Using Helper Functions with Another Function

Helper functions can be used alone or with another function. 

When using with other functions (like LOOKUP function), helper functions can be used to direct the expressions to the location of a specific value based on the structure of the table.

<br />

**[ <font color = 'navy'>LOOKUP</font>** function  +  **<font color = 'navy'>Helper</font>** functions **]**

* **LOOKUP(expression, offset):** 

  Returns the value of the given expression in a target row, specified as a relative offset from the current row.

  <br />

* **[Example] :** 

  * Find the profit value from three rows up the table:

    `LOOKUP( SUM([Profit]), -3 )`

    ​		<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210701102902227.png" alt="image-20210701102902227" style="zoom:80%;" /> 

    <br />

  * Compare the profit value to the last month of the year:

    1. Use LAST() function as the offset of the LOOKUP function to return the value of the SUM of Profit for the last month in the partition)

       `LOOKUP( SUM([Profit]), LAST() )`	+	Change the scope to  [ Pane (down) ] 

       ​		<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210701104404674.png" alt="image-20210701104404674" style="zoom:80%;" />

    2. Calculate how monthly profits compared to the last month of each year

       `SUM([Profit]) - LOOKUP( SUM([Profit]), LAST() )  `

       ​		<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210701105519703.png" alt="image-20210701105519703" style="zoom:80%;" />

<br />

<br />

## **2. Secondary Calculations**

Often, we use table calculations to add another layer of meaning to our data. 

Especially, with the table calculations **Running Total** and **Moving Calculation**, we have the option to add one more layer of meaning to our view — that is, to add a secondary table calculation on top of the primary one. 

Since secondary calculations can be displayed with an independent scope and direction from the primary calculation, it's important to consider how the secondary calculation changes the story your data tells.

<br />

**[Example]**

**<font color = 'navy'><< Goal >></font>** 

With the Superstore dataset, we wonder the contribution of each segment to the running total of sales for the quarter.

 <br />

**<font color='navy'>[Step 1]</font>** **Create the Basic View:** sum of sales by quarter for each segment

<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702103708499.png" alt="image-20210702103708499" style="zoom: 40%;" />

<br />

**<font color='navy'>[Step 2]</font>** **< Primary Table Calculation >** Calculate the running total of SUM(sales) for each quarter 

​			<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702104129698.png" alt="image-20210702104129698" style="zoom:55%;" /> 	<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702104202709-165631085320633.png" alt="image-20210702104202709" style="zoom: 40%;" />

<br />

**<font color='navy'>[Step 3]</font>** **< Secondary Table Calculation >** Calculate the contribution of each segment to the running total

<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702104824578.png" alt="image-20210702104824578" style="zoom: 50%;" />

<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702104947979.png" alt="image-20210702104947979" style="zoom: 40%;" />

<br />

<br />

## **3. Pareto Charts**

The Pareto Chart was designed to help highlight the [Pareto principle](https://en.wikipedia.org/wiki/Pareto_principle), which is sometimes called the Law of the Vital Few or the 80/20 rule. The Pareto principle states that in many cases, the majority of the results will come from a vital few of the causes. 

<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702130301577.png" alt="image-20210702130301577" style="zoom:50%;" />

<br />

A Pareto chart can help highlight the uneven distribution of contributions to your KPIs, so you can focus your efforts for the greatest impact. 

<br />

**[Example]**

**<font color = 'navy'><< Goal >></font>**

Build a Pareto chart to show how customers contribute to profitability, including how much is lost to unprofitable customers. 

<br />

**<font color='navy'>[Step 1]</font>** Create a sorted bar chart to show the profit by customer

* Sort Customer ID by Descending Profit

* Fit it to the Entire View

  <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702154222851.png" alt="image-20210702154222851" style="zoom:60%;" />

<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702133813598.png" alt="image-20210702133813598" style="zoom:45%;" />

<br />

**<font color='navy'>[Step 2]</font>** Use table calculations to show the percentage of total running sum of profit

* **Primary calculation:**      [Running Total] -- [Sum]  /  Compute using: [Specific Dimensions] -- [Customer ID]
* **Secondary calculation:** [Percent of Total] / Compute using: [Specific Dimensions] -- [Customer ID]

<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702134001248.png" alt="image-20210702134001248" style="zoom:50%;" />

<br />

<img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702134302137.png" alt="image-20210702134302137" style="zoom:45%;" />

<br />

**<font color='navy'>[Step 3]</font>** Color the profitable and unprofitable parts

* Add [SUM(Profit)] to the [Color] Mark 
* Edit colors:  use the full color range

   <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702140759224.png" alt="image-20210702140759224" style="zoom:50%;" />    <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702140631532-165631099939437.png" alt="image-20210702140631532" style="zoom:40%;" />

<br />

**<font color='navy'>[Step 4]</font>** Add reference lines to highlight the 80/20 rules

* **[4-1]  Add a 20% reference line to x-axis**

  To add the 20% reference line, we first need to change the x-axis (Customer ID axis) to a percent of total

  1. Ctrl + drag a copy of [Customer ID] to [Detail]

     (Since the profit table calculation is using [Customer ID] to set the scope and direction, if there isn't a copy of this dimension in the view, we'll break the calculation)

     <br />

  2. change the [Customer ID] on Columns to a Measure, showing the [Count(Distinct)]

  <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702142913450.png" alt="image-20210702142913450" style="zoom: 50%;" />

  <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702142945118.png" alt="image-20210702142945118" style="zoom: 50%;" />

  <br />

  3. Add a similar table calculation on the Count (Distinct) of Custom ID

     <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702155034147.png" alt="image-20210702155034147" style="zoom:50%;" />

     <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702155133673.png" alt="image-20210702155133673" style="zoom:50%;" />

  <br />

  4. Change the mark type to Bar

     <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702155326064.png" alt="image-20210702155326064" style="zoom:50%;" />

     <br />

  5. Add a 20% reference line to x-axis and simplify the axis label.

     <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702155536598.png" alt="image-20210702155536598" style="zoom:50%;" />

     <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702160104585.png" alt="image-20210702160104585" style="zoom:50%;" />

  <br />

* **[4-2] Add a 80% reference line to y-axis and simplify the axis label.**

  <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702155913088.png" alt="image-20210702155913088" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-1-Customizing-Table-Calculations/image-20210702160315005.png" alt="image-20210702160315005" style="zoom:50%;" />

<br />

<br />

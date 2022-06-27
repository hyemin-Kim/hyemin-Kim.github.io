---
title: Tableau >> Advanced (4) Customer Behavior Analyze Survey Data
date: 2022-06-27 15:39:13
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 4. Advanced
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
---

# Customer Behavior: Analyze Survey Data

<br />

Surveys are a useful way to collect data from the people your organization serves, but the results can be challenging to visualize. 

However, in Tableau Desktop, we can make survey data easier to consume by restructuring our data and visualizing it in a bar chart as follows.

<img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706105022838.png" alt="image-20210706105022838" style="zoom:67%;" />

<br />

#### \>> Practice

**<font color = 'navy'><< Goal >></font>**

A survey about college campus security has done in a local university, the students were asked to answer each question with one of five responses, ranging from Strongly Agree to Strongly Disagree. 

We would like to know 

* how the responses were distributed by the two campuses surveyed,

* the average response to each question, 
* and to see what areas of security need attention. 

<br />

**<font color = 'navy'><< Process >></font>**

**[STEP 1] Pivot the five questions: transpose data from columns to rows**

* Select the five questions fields --> Right-click --> Pivot

  <img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706124325253.png" alt="image-20210706124325253" style="zoom:40%;" /> 

  <br />

* Rename the new fields "Question" and "Responses"

  <img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706124455189.png" alt="image-20210706124455189" style="zoom:40%;" /> 

<br />

**[STEP 2] First looking at the data as a whole**

Show the total percentage of responses:

* Drag Responses to Columns  --> Change the aggregation to Count  --> Add a [Percent of Total] Quick Table Calculation

* Change the axis title and format the label so it does not display decimal places

  <img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706125857806.png" alt="image-20210706125857806" style="zoom:40%;" />

  <br />

**[STEP 3] Break down the responses by Campus and Questions** 

<img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706130527510.png" alt="image-20210706130527510" style="zoom:50%;" />

<br />

**[STEP 4] Color the bars by Responses**

* Make a copy of the [Responses] field, convert it to a dimension, and rename it [Responses (dimensions)]

  <img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706131323482.png" alt="image-20210706131323482" style="zoom:50%;" />

  <br />

* Color the view by [Responses (dimension)] and rename the aliases to match the survey

  <img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706131814108.png" alt="image-20210706131814108" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706131939248.png" alt="image-20210706131939248" style="zoom:50%;" />

<br />

* Edit legend colors and change the title to Responses

  <img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706132303482.png" alt="image-20210706132303482" style="zoom:50%;" />

<br />

**[STEP 5] Calculate the average response to each question** 

* Create a calculated field, fixed on Campus and Question, to determine the average response

  [Average Response] :

  `{ FIXED [Campus], [Question] : AVG([Responses]) }`

<br />

* Add [Average Response] to rows, make it discrete, and format it so it has one decimal place

  <img src="/images/S-Tableau-Advanced-4-Customer-Behavior-Analyze-Survey-Data/image-20210706133302359.png" alt="image-20210706133302359" style="zoom:50%;" />

<br />

<br />

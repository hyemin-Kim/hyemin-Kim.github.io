---
title: Tableau >> Intermediate (15) Comparing Measures Against a Goal
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 48610
date: 2022-06-27 15:07:46
---

# Comparing Measures Against a Goal

@[toc]

<br />

## **1. Building Bar-in-Bar Charts**

Bar-in-bar charts are useful for comparing two measures as overlapping bars in the same space.

Making the bars different sizes can avoid that the bars bidden underneath the others

<br />

### Process to build a bar-in-bar chart

* Add <font color = 'blue'>[dimension]</font> to [Rows]

  Add the <font color = 'viridans'>1st [Measure]</font> to [Columns]

  <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614110224399.png" alt="image-20210614110224399" style="zoom:67%;" />

  <br />

* Drag the <font color = 'viridans'>2nd [Measure]</font> to the view, dropping it on the x-axis when two green bars appear.

  <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614110405228.png" alt="image-20210614110405228" style="zoom:67%;" />

  <br />

* Side-by-side bars for two [Measures]

  <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614110512156.png" alt="image-20210614110512156" style="zoom:67%;" />

  <br />

* Move the [Measure Names] from [Rows] to [Color] mark

  <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614110845733.png" alt="image-20210614110845733" style="zoom:67%;" />

  <br />

* Unstack bars

  [Analysis] menu --> [Stack Marks] --> [Off]

  <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614111240025.png" alt="image-20210614111240025" style="zoom:80%;" />	<img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614111307271-16563136198991.png" alt="image-20210614111307271" style="zoom:60%;" />

<br />

* Make the bars different size

  * Hold [Ctrl] and drag [Measure Name] to [Size]

  * Edit size:

    * Smallest : controls the size for the thinner bars
    * Largest :   controls the size for the thicker bars

    ![image-20210614111715412](/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614111715412.png)	![image-20210614111734298](/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614111734298.png)	<img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614111758855-16563136537213.png" alt="image-20210614111758855" style="zoom: 67%;" />

    <br />

  <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614111931130.png" alt="image-20210614111931130" style="zoom: 67%;" />

<br />

<br />

## **2. Building Bullet Graphs**

Bullet graphs can be useful when you want to see how far a measure has progressed toward a goal. (i.e. comparing a measure against another measure)

<br />

### \>> Methods to create a bullet graph

#### [Method 1] In the Data Pane

[Question] How far enrollment has progressed towards the maximum enrollment that would be allowed

* Build a view that shows current enrollment by department

  <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614125445025.png" alt="image-20210614125445025" style="zoom:80%;" />

  <br />

* Use Maximum Enrollment as a reference line

  * Add [Maximum Enrollment] to [Detail]

  * Right-click the x-axis (Students Enrolled axis), and choose [Add Reference Line]

  * Edit the reference line with [Scope], [Line] and [Formatting]

    <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614125641240.png" alt="image-20210614125641240" style="zoom: 50%;" />         <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614125736991-16563136858875.png" alt="image-20210614125736991" style="zoom:67%;" />

    <br />

    <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614125952753.png" alt="image-20210614125952753" style="zoom:80%;" /> 

  <br />

* Add distribution areas to show stages of process

  * Right-click the x-axis (Student Enrolled axis), and choose [Add Reference Line]

    <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614130221752.png" alt="image-20210614130221752" style="zoom:80%;" />

  * Edit the distribution

    \- Scope: [Per Cell]

    \- Computation: [Percentages] 25, 50, 75  ---  [Percent of]  Sum(Maximum Enrolled) / Sum

    \- Label : [None]

    \- Formatting : check [Fill Below]

    <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614130533550.png" alt="image-20210614130533550" style="zoom: 67%;" />					<img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614130351229-16563137195357.png" alt="image-20210614130351229" style="zoom: 67%;" />

    <br />

    <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614130758991.png" alt="image-20210614130758991" style="zoom:80%;" /> 

  <br />

* Use color to distinguish whether a department has reached its maximum enrollment

  * Create a calculated field "Max Enrolled?"

    `SUM([Students Enrolled]) >= SUM([Maximum Enrollment])`

  * Drag [Max Enrolled?] to [Color]

  <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614131317367.png" alt="image-20210614131317367" style="zoom:80%;" />

<br />

#### [Method 2] Use the *Show Me*

* Select two measures we want to compare, and any dimensions we want to include

* Click [Show Me] and select the bullet graph icon

  * Here, Tableau uses 

    \- the *Maximum Enrollment* for the bars and 

    \- *current enrollment* for the reference lines and distribution

  <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614132009819.png" alt="image-20210614132009819" style="zoom:85%;" /> 	<img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614132031246-165631376553311.png" alt="image-20210614132031246" style="zoom:80%;" />    <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614132150639-165631379546813.png" alt="image-20210614132150639" style="zoom:60%;" />

  <br />

* Swap how the two measures are used

  * Right-click the x-axis (Maximum Enrollment axis)  --> [Swap Reference Line Fields]

    <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614132818737.png" alt="image-20210614132818737" style="zoom:80%;" />    <img src="/images/S-Tableau-Intermediate-15-Comparing-Measures-Against-a-Goal/image-20210614132853178-165631381365915.png" alt="image-20210614132853178" style="zoom:60%;" />

<br />

<br />

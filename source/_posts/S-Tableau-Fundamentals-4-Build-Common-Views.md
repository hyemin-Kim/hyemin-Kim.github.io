---
title: Tableau >> Fundamentals (4) Build Common Views
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 2. Fundamentals
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 17023
date: 2021-06-28 10:58:53
---

# Build Common Views

@[toc]

<br />

## **1. Working with Dates to Visualize Time-Based Data**

\>> Change date field and calender defaults

* [Data] --> Data Source Name --> [Date Properties]

  ​			<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210521145523588-16298809215928.png" alt="image-20210521145523588" style="zoom:50%;" />					<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210521145648241.png" alt="image-20210521145648241" style="zoom:80%;" />

<br />

<br />

## **2. Create Custom Date Fields and Hierarchies**

### \>> Create a custom continuous date value

1. [Data] Pane --> [Order Date] --> click the down-arrow

2. [Create] --> [Custom date]

3. [Name] :  "Continuous Date (Months)"

   [Detail] : "Months"

   [Date Value]

4. Click [OK]

   ​					<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210521161538861-16298808457426.png" alt="image-20210521161538861" style="zoom:50%;" />					<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210521161650010.png" alt="image-20210521161650010" style="zoom: 80%;" />

<br />

### \>> Create a custom discrete date part

1. [Data] Pane --> [Order Date] --> click the down-arrow

2. [Create] --> [Custom date]

3. [Name] :  "Discrete Date (Months)"

   [Detail] : "Months"

   [Date Part]

4. Click [OK]

   ​				<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210521161538861-16298808772617.png" alt="image-20210521161538861" style="zoom:50%;" />						<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210521162304726.png" alt="image-20210521162304726" style="zoom:80%;" />

<br />

### \>> Create a custom date hierarchy

1. Create a custom discrete date part field, "Discrete Date (Years)"
2. Create another custom discrete date part field, "Discrete Date (Months)"
3. In the [Data] pane, drag [Discrete Date (Months)] on top of [Discrete Date (Years)]
4. In the dialog box, change the name of the hierarchy to "Custom Dates"
5. Click [OK]

<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210521163445426.png" alt="image-20210521163445426" style="zoom:80%;" />

<br />

<br />

## **3. Comparing Multiple Measures in Views**

**[Measure Values]** (<font color = 'viridis'>측정값</font>) and **[Measure Names]** (<font color = 'blue'>측정값 이름</font>) fields are automatically created by Tableau.

They serve as containers for the measures in the [Data] Pane:

* <font color = 'viridis'>[Measure Values]</font> field:  a measure that contains the values of the measures
* <font color = 'blue'>[Measure Names]</font> field: a dimension that contains the names of the measures
  * Note: it does not include measures, such as [Latitude], that do not aggregate the same way as other measures

With  **Measure Values** and **Measure Names** fields, you can build certain types of views that involve multiple measures, enabling you to compare them.

<br />

### \>> Create text tables with multiple measures

**[개요]**

* Text tables can contain up to **fifty measures on Rows** and **sixteen on Columns**
* Measures in text tables **can have different units**



<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210521170225404.png" alt="image-20210521170225404" style="zoom:67%;" />

<br />

<br />

### \>> Make views with multiple measures on the same axis

**[개요]**

* You can add **fifty measures** to the same axis
* Measures that share an axis should have the **same unit of measurement**
* Measures that share the same axis use the **same type of mark**, such as bar

<br />

**[실습]**

1. Add [Category] to [Columns]
2. Add [Sales] to [Rows]
3. Drag [Profit] from the [Data] pane to the [Sales] axis
   * [Measure Values] and [Measure Names] will be added to the view automatically
4. Drag [Measure Name] from the [Data] pane, to color on the [Marks] card.

<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526084305992.png" alt="image-20210526084305992" style="zoom:60%;" />

<br />

<br />

### \>> Build dual and combined axis charts

**[개요]**

* **Dual axis charts** have <font color = 'viridis'>two axes for the measures</font> and <font color = 'blue'>one for the dimensions</font>
* **Dual axis charts** use <font color = 'viridis'>two measures</font> and <font color = 'blue'>one or more dimensions</font>

* Measures can have **different units**
* Measures can use the **same or different mark types**

<br />

**[실습]**

* **Measures with same number format**  [Sales & Profit]

  1. **<font color = 'darkblue'>Set the dimension and the first measure in the view</font>**

     [Columns] : <font color = 'viridis'>Month(Order Date)</font>  (*dimension*)

     [Rows] : <font color = 'viridis'>SUM(Sales)</font>  (*first measure*)

     <br />

  2. **<font color = 'darkblue'>Make a dual axis chart:</font>**

     Drag <font color = 'viridis'>[Profit]</font> (*second measure*) from Data pane to the right edge of the view 

     until you see *< a light green ruler icon >* and *< a black dotted line >*

     and drop the measure.

     <img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526095349671.png" alt="image-20210526095349671" style="zoom: 50%;" />

     <img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526100126518.png" alt="image-20210526100126518" style="zoom:50%;" />

     <br />

  3. **<font color = 'darkblue'>Change the mark type for each measure</font>**

     <img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526094017490.png" alt="image-20210526094017490" style="zoom:50%;" />

     <br />

  4. **<font color = 'darkblue'>Set the scales same</font>**

     Right-click the axis want to change --> Synchronize Axis

     <img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526101345020.png" alt="image-20210526101345020" style="zoom:50%;" />

<br />

* **Measures with different number formats**  [Sales & Discount]

  \> Without [Synchronize Axis] (축 동기화)

  <img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526102648297.png" alt="image-20210526102648297" style="zoom:50%;" />

<br />

<br />

### \>> Using Scatter Plots To Show Relationships Between Measures

> [E-Learning Link](https://elearning.tableau.com/tableau-fundamentals/786137/scorm/3htuzbdo9a99x)

**[What can we do with scatter plots?]**

* Evaluate data clusters

* Identify correlations and trends

  \- Use correlations and trends to analyze data

* Identify outliers

  \- Manage outliers

  \- Exclude an outlier from a view

  \- Add an annotation to an outlier

<br />

**[Details]**

* **Build a scatter plot**

<img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526110123760.png" alt="image-20210526110123760" style="zoom: 67%;" />

<br />

* **Evaluate data clusters**

  \- Two clusters divided by the eruption duration classes, [long] and [short]

  <img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526110409805.png" alt="image-20210526110409805" style="zoom: 67%;" />

  <br />

* **Identify correlations and trends**

  \- Positive Correlation

  \- Negative Correlation

  \- No Correlation

<br />

* **Use correlations and trends to analyze data**

  <img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526111021545.png" alt="image-20210526111021545" style="zoom: 67%;" />

  \- Positive relationship between [wait time between eruptions] and [eruption duration]

  \- the longer the wait time between eruptions, the longer the eruption duration

<br />

* **Identify outliers**

  <img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526111537532.png" alt="image-20210526111537532" style="zoom:67%;" />

  * Exclude an outlier

    1. Press [Ctrl] and select the outlier

    2. On the tooltip that appers, click [Exclude]

       <br />

  * Add an annotation to an outlier

    1. Right-click the outlier
    2. Point to [Annotate] (주석 추가)
    3. Click [Mark]
    4. Use the [Edit Annotation] dialog box to create annotation
    5. click [OK]

    <img src="/images/S-Tableau-Fundamentals-4-Build-Common-Views/image-20210526123454393.png" alt="image-20210526123454393" style="zoom: 67%;" />

    <br />

  <br />








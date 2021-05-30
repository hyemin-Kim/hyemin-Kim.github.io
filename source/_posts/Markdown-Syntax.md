---
uuid: bb1ba431-d26c-e1a0-9dd0-3d09f764fb47
title: Markdown 常用语法（持续更新）
tags:
 - Markdown
categories: 【USAGE】
cover: https://s1.ax1x.com/2020/05/23/YjmlFg.png
comments: true
abbrlink: 14404
typora-root-url: ..
date: 2020-05-10 02:16:53
---

<font face="Microsoft YaHei">

## **Markdown 常用语法**

<br />

### **标题** 

一级标题： "#" + 空格 + "一级标题"  
二级标题： "##" + 空格 + "二级标题"  
三级标题： "###" + 空格 + "三级标题"  
……  
以此类推 【最多到6级】
<br />

### **换行**

“内容” 末尾 + 2个空格 + Enter

<br />

### **斜体**

- 方法一：“内容”前后加1个 * 号（无空格）

- 方法二：“内容”前后加1个下划线（无空格）

> *“内容” *    ——>  *"内容"*  
>
> _ “内容” _   ——>  _内容_

<br />

### **加粗**

- 方法一：“内容”前后加2个 * 号（无空格）

- 方法二：“内容”前后加2个下划线（无空格）

> ** “内容” **   ——>  **"内容"**  
>
> __ “内容” __   ——>  __“内容”__

<br />

###  **斜体加粗**

“内容”前后加 3 个 * 号 （无空格）

> ***“内容”***

<br />

### **删除线**

”内容”前后加 2 个波浪线（~）

> ~~ “内容” ~~   ——>  ~~“内容”~~

<br />

### **高亮**

“内容”前后加 2 个 = 号

> == "内容" ==   ——>  =="内容"==

<br />

### **字体，颜色，字号**

使用 font 标签

 ```html
 <font  face='Microsift Yahei'  color='red'  size='6'> 字体，颜色和字号 </font>
 ```
<font color='red'  size='6'> 字体，颜色和字号 </font>

<br />

### **上标 & 下标**

  + 上标：“内容”前后加 1 个 ^ 号

  + 下标：“内容”前后加 1 个 ~ 号

> 我是 ^ 上标 ^  ——>  我是^上标^  
>
> 我是 ~ 下标 ~  ——> 我是~下标~

<br />

### **引用**

“内容”前加 > 号

> “内容”

引用号可叠用，>号越多，级数越低  
例如：可以使用>, >>, >>> 的形式

> 一级引用
> > 二级引用
> >
> > > 三级引用

<br />

### **文字内容对齐设置**

**1. 使用div标签：**
	

	```html
	<div style="text-align: right">your-text-here</div>
	```

> <div style="text-align: left">居左</div>
> <div style="text-align: center">居中</div>
> <div style="text-align: right">居右</div>

<br />

**2. 使用p标签：(在Jupyter Notebook中不适用)**

   居中：```<center> 内容 </center> ```

   居左/居右：```<p align='left'> 内容 </p>```

> <p align='left'> 居左 </p>
> <center> 居中 </center>
> <p align='right'> 居右 </p>

<br />

### **插入链接**

​     中括号内输入“显示的文字”，紧接着小括号内输入“网址链接”  
​    【注意：网站地址需要 http 开头，最好直接复制】

> [点我进入百度](http://www.baidu.com/)

<br />

### **插入图片**

​     感叹号 + 中括号内输入“显示的文字”，紧接着小括号内输入“图片链接”  
​    【注意：图片链接非网页的网址栏链接，而是右键“复制图片地址”得到的链接 (Chrome)】

> ![图片](http://t9.baidu.com/it/u=1307125826,3433407105&fm=79&app=86&f=JPEG?w=5760&h=3240)

<br />

* **调整图片大小：**

  ```html
  <img src="链接" width="宽度(数字or百分比)" height="高度" alt="图片名称" align=center/left/right>
  ```


<br />

### **列表**

#### **（1） 有序列表**

​      （序号1+点+空格）+内容+回车  
​      （序号2+点+空格）+内容+回车  
​      （序号3+点+空格）+内容+回车

> 1. 第一行
> 2. 第二行
> 3. 第三行

​      【注意】：系统会默认调整有序列表的序列数。即，即使你误输入成了1.，2.，4.，系统也会自动更正为 1.，2.，3.  

> 1. 第一点
> 2. 第二点
> 4. 第四点

<br />

#### **（2）无序列表**

​        使用“ + ”+空格+内容  
​       ​ 或者“ - ”+空格+内容  
​       ​ 或者“ * ”+空格+内容  
​       下一级：前面加 tab

> + 第一章
>
> + 第二章
>
> + 第三章
>
> 	+ 第一节

<br />

#### **（3）任务列表**

​       短横线 + 1 个空格 + 中括号（括号中间带 1 个空格） + 1 个空格 + “内容”

> - [x] 学习python
> - [ ] 学习SQL

<br />

### **表格**

* 添加表格
  竖线作为列分界线，换行竖线中间输入短横线作为行分界线
  
  <img src="/images/Markdown-Syntax/image-20201110155108847-1604994124837.png" alt="image-20201110155108847" style="zoom:80%;" />

<br />

* 表格内容对齐

  | 左对齐 | 居中 | 右对齐 |
  | :----: | :---: | :----: |
  | :----- | :-----: | -----: |
  |<img src="/images/Markdown-Syntax/image-20201110155454459-1604994136986.png" alt="image-20201110155454459" style="zoom:80%;" />|<img src="/images/Markdown-Syntax/image-20201110155540639-1604994144047.png" alt="image-20201110155540639" style="zoom:80%;" />|<img src="/images/Markdown-Syntax/image-20201110155606006-1604994150443.png" alt="image-20201110155606006" style="zoom:80%;" />|



<br />

* 表格内容换行

  插入 \<br\>

  <img src="/images/Markdown-Syntax/image-20201110160141094-1604994157283.png" alt="image-20201110160141094" style="zoom:80%;" />

<br />

### **代码**

三个 ` 号，再输入所使用的编程语言

 ``` python
print("Python")  # python
 ```
 ```R
install.packages("ggplot2")  # R语言
 ```

<br />

### **插入目录 [Only for Typora]**

- 中括号内输入toc
- In Hexo: @[toc] (在使用hexo-renderer-markdown-it-plus插件时)

<br />
<br />

</font>
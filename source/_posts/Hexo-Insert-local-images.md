---
uuid: e8dffd4a-1715-5aa7-9cff-a6c8c7b9dae5
title: 在Hexo博文中添加本地图片的方法（基于Typora编辑器）
tags: 
- Hexo
- Typora
- Markdown
categories: 【USAGE】
description: 当我们想在markdown文档中添加网络图片时，可以使用命令```!['图片名称'](图片网络地址)```进行实现，然而这条命令却不适用于添加本地图片。本文将介绍在使用Typora编辑器编辑Hexo博文时，向markdown文档中添加本地图片的方法。快来看看吧
cover: https://lh4.googleusercontent.com/proxy/9EC0bxXmSPU8lCpM59sJo-H8ohlFDIDMpsemcAPPNNhak2m4jFKOG_tKCk8e1NemgjaICnYX5lgyE7SHOD6T11AuYTN6nWsJzESiibeKdHCiY7TA5A
comments: true
typora-root-url: ..
abbrlink: 5572
date: 2020-05-12 21:20:48
---

<font face="Microsoft YaHei">

当我们想在markdown文档中添加网络图片时，可以使用命令```!['图片名称'](图片网络地址)```进行实现，然而这条命令却不适用于添加本地图片。本文将介绍在使用Typora编辑器编辑Hexo博文时，向markdown文档中添加本地图片的方法。快来看看吧
<!-- more -->

<br />

@[toc]

<br />


### **【编写博客前】— 进行配置**

<br />

1. **建立 [资源文件夹(Asset Floder)](https://hexo.io/zh-cn/docs/asset-folders)，用来保存添加到博文中的本地图片**

   - 在本地Hexo根目录下的```source```文件夹中创建一个名为 ```images``` 的文件夹 


2. **在Typora中设置图片的相对路径**
  
   - 打开Typora的``文件 > 偏好设置 > 图像``，进行如下设置：  
   <center><img src="/images/Hexo-Local-Pictures/image-20200506223313787.png" alt="image-20200506223313787" style="zoom:50%;" /></center>
   
   - 此设置会使``source/images``文件夹下新增一个与所编辑的markdown文档同名的文件夹，文档中所添加的 *本地图片* 都将存档于此（即拥有了如下路径：```'hexo根目录'/source/images/'md文档名'/'图片名称'）```)。
     <br />
  
3. **撰写markdown文档时配置 *图片根目录* ，使其能够同步到hexo博客中去**

   - 撰写博文时，先点击Typora菜单栏中的```格式 > 图像 > 设置图片根目录``` , 将根目录配置为``'hexo根目录'/source``。然后再撰写博文。【注：每篇需要添加本地图片的博文都要先进行此步骤】  
   <center><img src="/images/Hexo-Local-Pictures/1.png" alt="1" style="zoom:50%;" /></center>


<br />

### **【编写博客时】— 图片导入方法**
 <br />

1. **直接拖拽**
   - 将原本存放于其他本地文件夹中的图片直接拖拽到文档中的相应位置中去
   - 此时图片会被自动存档至生成的同名文件夹```'hexo根目录'/source/images/'md文档名'```中
   - 文档中图片地址的代码会显示成 *自动生成的相对路径*，即``/images/'md文档名'/'图片名称'`` 
     <br />
2. **利用相对路径调取**
   - 当利用 *方法1* 插入了至少一张图片时（即已生成同名文件夹时），便可以把接下来要插入的图片复制到此同名文件夹中，在文档中*利用相对路径* 调取图片：
   - 所使用的命令是：```![图片显示名称](/images/'md文档名'/'图片名称')``` 
   - 这里的``图片显示名称``不必与文件夹中保存的``图片名称``保持一致，```'图片名称'```中要记得包含图片格式（例如：tupian.jpg 或 picture.png 等）  
     <br />


  【注意】当还没有利用 *方法1* 插入过图片时（即同名文件夹尚未生成时），**不可以自己创建同名文件夹**保存图片。亲测不好使！！（.md文档中可以显示，但是hexo博文中无法显示）

<br />

### **【编写博客后】— 图片存档结果**

在利用上述方法完成了含有本地图片的markdown博文后，我们的资源文件夹```'hexo根目录'/source/images/```内最终会显示成什么样子呢？

- 每一篇配置了图片根目录的博文（即【编写博客前】的第3步），都会在```'hexo根目录'/source/images/```文件夹中有一个与文档名称同名的文件夹```'hexo根目录'/source/images/'md文档名'```

- 该文件夹中会保存博文编写中曾经添加的**所有本地图片**
  - **所有**的含义是：即使编辑过程中某些本地图片在添加后又被删除了，它们也仍然会保留在文件夹中，即该文件夹会备份你在博文中添加的 *所有本地图片历史*
  - **本地图片**的含义是：这里只会保存插入的本地图片，而不会保存插入的网络图片。尽管在【编写博客前】的第2步配置中，我们也同样勾选了``对网络位置的图片应用上述规则``。（请原谅我并不知道其中的缘由。。）  

  

就此，在Typora编辑器中编写Hexo博文时，向markdown文档中添加本地图片的方法就介绍完毕啦！快去应用到你的博文中去吧~

 <br />  
 <br />  
 <br /> 
 <hr />

本文参考了[yinyoupoet](https://yinyoupoet.github.io/)的[typora + hexo博客中插入图片](https://yinyoupoet.github.io/2019/09/03/hexo博客中插入图片/)  
更多关于Typora中插入图片的内容可以参考[Typora的官方说明](https://support.typora.io/Images/#when-insert-images)

 <hr />  
 <br />  
 <br />  


</font>
---
title: 什么是FreeMarker？
layout: post
tags: FreeMarker
date: 2019-08-30 10:14:56
---
>**1、什么是FreeMarker？**

FreeMarker是一个用Java语言编写的模板引擎，它基于模板来生成文本输出。其原理如下图所示：
![原理图](https://img-blog.csdnimg.cn/20190830104112439.png)
FreeMarker的模板文件并不比HTML页面复杂多少，FreeMarker模板文件主要由如下4个部分组成:

（1）文本：直接输出的部分 
（2）注释：使用<#-- ... -->格式做注释，里面内容不会输出 
（3）插值：即${...}或#{...}格式的部分，类似于占位符，将使用数据模型中的部分替代输出 
（4）FTL指令：即FreeMarker指令，全称是：FreeMarker Template Language，和HTML标记类似，但名字前加#予以区分，不会输出

下面是一个FreeMarker模板的例子，包含了以上所说的4个部分：
```FreeMark
<html>
<head>
<title>Welcome to FreeMarker 中文官网</title><br> 
</head> 
<body>
<#-- 注释部分 --> 
<#-- 下面使用插值 --> 
<h1>Welcome ${user} !</h1><br> 
<p>We have these animals:<br> 
<u1>
<#-- 使用FTL指令 --> 
<#list animals as being><br> 
  <li>${being.name} for ${being.price} Euros<br> 
<#list>
<u1>
</body> 
</html> 
```
FreeMarker与Web容器无关，即在Web运行时，它并不知道Servlet或HTTP，故此FreeMarker不仅可以用作表现层的实现技术，而且还可以用于生成XML，JSP或Java等各种文本文件。

在Java Web领域，Freemarker是应用广泛的模板引擎，主要用于MVC中的view层，生成html展示数据给客户端，可以完全替代JSP。

总之，FreeMarker是一个模板引擎，一个基于模板生成文本输出的通用工具，使用纯Java编写，模板中没有业务逻辑，外部Java程序通过数据库操作等生成数据传入模板（template）中，然后输出页面。它能够生成各种文本：HTML、XML、RTF、Java源代码等等，而且不需要Servlet环境，并且可以从任何源载入模板，如本地文件、数据库等等。

>**2、FreeMarker有什么优点？**

FreeMarker的诞生是为了取代JSP。虽然JSP功能强大，可以写Java代码实现复杂的逻辑处理，但是页面会有大量业务逻辑，不利于维护和阅读，更不利于前后台分工，容易破坏MVC结构，所以舍弃JSP，选择使用FreeMarker是大势所趋。当前很多企业使用FreeMarker取代JSP，FreeMarker有众多的优点，如下所示：

（1）很好地分离表现层和业务逻辑。

JSP功能很强大，它可以在前台编写业务逻辑代码，但这也带来了一个很大的弊端——页面内容杂乱，可读性差，这将会大大增加后期的维护难度。而FreeMarker职责明确，功能专注，仅仅负责页面的展示，从而去掉了繁琐的逻辑代码。FreeMarker的原理就是：模板+数据模型=输出，模板只负责数据在页面中的表现，不涉及任何的逻辑代码，而所有的逻辑都是由数据模型来处理的。用户最终看到的输出是模板和数据模型合并后创建的。

（2）提高开发效率。

众所周知，JSP在第一次执行的时候需要转换成Servlet类，之后的每次修改都要编译和转换。这样就造成了每次修改都需要等待编译的时间，效率低下。而FreeMarker模板技术并不存在编译和转换的问题，所以就不会存在上述问题。相比而言，使用FreeMarker可以提高一定的开发效率。

（3）明确分工。
JSP页面前后端的代码写到了一起，耦合度很高，前端开发需要熟悉后台环境，需要去调试，而后台开发人员需要去做不熟悉的前端界面设计。对两者而言，交替性的工作需要花费一定的学习成本，效率低下。而使用FreeMarker后，前后端完全分离，大家各干各的，互不影响。

（4）简单易用，功能强大
FreeMarker支持JSP标签，宏定义比JSP Tag方便，同时内置了大量常用功能，比如html过滤，日期金额格式化等等。FreeMarker代码十分简洁，上手快，使用非常方便。

>**3、Freemarker的使用方法**

freemarker没有其他的任何依赖，仅仅依赖Java自身。

3.1、freemarker最新版本
最新版本是：freemarker 2.3.28，发布于：2018-04-04。需要：J2SE 1.5 或更高版本

3.2、freemarker maven仓库管理
把freemarker的jar包添加到工程中，Maven工程添加依赖
```java
<dependency>
  <groupId>org.freemarker</groupId>
  <artifactId>freemarker</artifactId>
  <version>2.3.28</version>
</dependency>
```

>**4 参考**

[freemarker中文官网](http://www.freemarker.cn/)
，它基于模板来生成文本输出。其原理如下图所示：

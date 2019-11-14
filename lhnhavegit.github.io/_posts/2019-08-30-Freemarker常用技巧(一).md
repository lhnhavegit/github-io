---
title: Freemarker常用技巧(一)
layout: post
tags: FreeMarker
date: 2019-08-30 14:17:30
---

>**1 截取字符串**

有的时候我们在页面中不需要显示那么长的字符串，比如新闻标题，这样用下面的例子就可以自定义显示的长度
```freemarker
<#if title.content?length lt 8>
           <a href>${title.content?default("")}</a>
      <#else>
           <a href title="${title.content}">${title.content[0..3]?default("")}...</a>
</#if>
```
意思就是如果这个字符串的长度小于8，那么就正常显示，反之则取4位
注意：常用的比较运算符
=(==):判断两个值是否相等
!=:不相等
```freemark
>(gt):判断左边是否大于右边
>=(gte):大于等于
<(lt):小于
<=(lte):小于等于
```
>**2 连接字符串**
```freemark
${"Hello," + user + "!"} //输出结果为:hello,swiftlet.net!
```

>**3 日期格式和boolean类型，转化为string类型**
```freemark
${lastUpdate?string("yyyy-MM-dd HH:mm:ss")}      
```
输出结果如下:
```freemark
2003-04-08 21:24:44
<#assign foo=true/>
${foo?string("yes","no")} //输出结果:yes
```
>**4 排序**

升序用sort_by()
```freemark
<#list list?sort_by("字段") as x>
</#list>
```
降序用sort_by()?reverse
```freemark
<#list list?sort_by("字段")?reverse as x>
</#list>
```
>**5 去空格**
```freemarker
${xx?trim}
```
>**6 数值精度控制**
```freemarker
mX:小数部分最小X位。
MX:小数部分最大X位。
<#assign x=2.582/>
<#assign y=4/>
#{x; M2}//2.58
#{y; M2}//4
#{x; m1M2}//2.58
#{y; m1M2}//4.0
```

>**7 内置函数**
```freemarker
html:字符串中所有的特殊HTML字符都需要用实体引用来代替（比如<代替&lt;）
cap_first:字符串的第一个字母变为大写形式
lower_case:字符串的小写形式
upper_case:字符串的大写形式
trim:去掉字符串首尾的空格

序列使用的内建函数：
size：序列中元素的个数

数字使用的内建函数：
int:数字的整数部分（比如-1.9?int就是-1）9>.空值运算符

length:字符串的长度
string :把其他格式的数据，转化为string类型
${test?html}
${test?upper_case?html}

假设字符串test存储”Tom & Jerry”，那么输出为：

Tom &amp; Jerry
TOM &amp; JERRY

${seasons?size}
${seasons[1]?cap_first}

${"horse"?cap_first}
假设seasons存储了序列"winter", "spring", "summer", "autumn"，那么上面的输出将会是：
4
Spring
Horse
```
> **8 顶层变量**

所谓顶层变量就是直接放在数据模型中的值。
```FREEMARKER
Map root = new HashMap();
root.put("name","admin");//name是一个顶层对象
对于顶层变量,直接使用${variableName}来输出变量值
```
       
>**9 集合连接运算符**

集合连接运算是将两个集合连接成一个新的集合,连接集合的运算符是'+'.
```FREEMARKER
<#list ["一","二","三"] + ["四","五","六"] as x>
    ${x}
</#list>
//输出结果如下:
一二三四五六
```

>**10 算术运算符**

取整运算
```FREEMARKER
<#assign x=5>
${(x/2)?>int}//2
${1.1?int}//1
${1.999?int} //1
${-1.1?int}//-1
```

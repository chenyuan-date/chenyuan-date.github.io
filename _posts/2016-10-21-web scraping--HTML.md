---
layout: post            
title: web scraping -- HTML                         
author: CY                            
tags: [Website]                                      
categories: [R]                           
share: false                              
image:                                      
  background: triangular.png 
---



### HTML introduction

作为网络前端技术最核心三大技术之一（HTML、CSS和JavaScript），HTML的重要性不言而喻。如果说前端开发过程是一个造房子的过程，那么HTML就是这所房子的骨架结构，从地基到天花板要结构明晰，而房子造好后的装修则是CSS，比如说给地板贴瓷砖，给墙壁贴墙纸这样。最后房子建好，晚上我们要开灯不是？这就是JavaScript。

HTML的全称叫做超文本标记语言（Hyper Text Markup Language），是一种用于在网页上展示内容的语言。HTML并不是一种编程语言，而是一种描述内容并定义其表征的标记语言。说白了就是，HTML只规定了网页的结构，让网页在哪里显示标题和内容，显示什么内容，至于怎么个显示法，HTML管不着。

### HTML语法规则

随手打开一个网页，单击右键查看源文件，当前网页的HTML代码就展示在你眼前了。相较于编程语言的语法，HTML的语法堪称简单易懂又好学。从结构上看，HTML是一个树形结构，从内容上来看，HTML也就是标签、元素和属性这些内容，再稍微注意一下HTML的注释方式、保留字符和文档定义，一个简单的HTML知识概览你就了解了。



**标签、元素和属性**

HTML中标签指的是会指定其中包装的文本作为在浏览器分页的标题栏显示的标题，在实际语法中标签通常以一个< >符号包括起来，起始标签、内容和终止标签组合起来则成为元素，如下代码所示：

    <title> Chinars | 统计之都 </title>

起始标签和终止标签都用< > 符号包裹，以便和内容进行区分，不同的是终止标签会有一个/符号以示区别。一般而言，每个元素都有一个起始标签和终止标签，但也不是全部。比如说<br>标签表示换行，它就不需要一个</br>标签来表示终止。

常用的HTML标签如下表所示, 更多标签请参考[HTML手册](http://www.w3school.com.cn/tags/)：

| 标签         | 描述             |
| ---------- | -------------- |
| <a>        | 定义锚            |
| <!DOCTYPE> | 定义文档类型         |
| <meta>     | 定义关于HTML文档的元信息 |
| <link>     | 定义文档与外部资源的关系   |
| <code>     | 定义计算机代码文本      |
| <p>        | 定义段落           |
| <br>       | 换行             |
| <h1>-<h6>  | 定义HTML标题       |
| <div>      | 定义文档中的节        |
| <span>     | 定义文档中的节        |
| <form>     | 定义供用户输入的HTML表单 |
| <script>   | 定义客户端脚本        |
| <tr>       | 定义表格中的行        |
| <td>       | 定义表格中的单元       |



标签最重要的一个特性是属性。例如：

	<a href="/chinar/chinar-2013/">第六届中国R语言会议</a>

锚标签<a>能够把相关的文本（这里是“第六届中国R语言会议”）和一个指向另一个地址的超链接关联起来。href="/chinar/chinar-2013/"这个属性指定锚链接，浏览器会自动把这类元素转化为带有下划线并且可以点击的样式。总而言之，属性就是让标签能够描述其内容处理方式的选项。具体属性的作用则根据相应的标签来定。

属性总是处于起始标签的内部，标签名的右侧，一个标签拥有多个属性也是常见操作，多个属性之间用空格分开。就像下面这样：

	<div><img src="https://uploads.cosx.org/2010/10/SHUFE_map.jpg" alt="Thumbnail" /></div>


**树形结构**

就像文档结构图一样，HTML最大的一个特点就是它呈现出树形结构的样子。先看一个简单的HTML结构示例：
```
<!DOCTYPE html>                        
    <html>         
       <head>             
          <title> Chinars | 统计之都 </title>              
      </head>               
        <body>             
           第10届中国R会议简介            
        </body>                  
    </html>                   
```

<!DOCTYPE html>是文档定义类型标签，忽略这个的话这个例子的第一个元素是<html>元素，在这个元素的起始和终止标签内，又有几个标签分别起始和终止：<head><title>和<body>。<head>和<body>标签是直接被<html>元素包含的，<title>标签则包含在<head>标签内。一个典型的树形结构就这样被描述出来了。

在结构良好并且合法的HTML文件中，所有元素相互之间必须是严格嵌套的。一对起始标签和终止标签必须完全包含在另一对起始和终止标签内。


### HTML的R语言解析

所谓解析，是为了获得有用的HTML文件表征，运用一个能够理解标记结构特殊含义的程序、并在某个R的专用数据结构内部重建HTML文件隐含的层次结构，而不是仅仅读取。在R语言中，我们通常使用XML包中的`htmlParse()`函数来解析一个HTML文件，XML有着与以C语言为基础的libxml2库的接口，功能十分强大。且看简单的R代码示例：

```
library(XML)
url <- "http://www.r-datacollection.com/materials/html/JavaScript.html"
exmaple1 <- htmlParse(file = url)
print(example1)
```

解析出来的结果什么呢？就是你打开该网页，右击查看源代码后出来的内容呀。为啥要解析HTML网页？为了方便下步的数据提取呀，傻狍子～


### References    

[R语言爬虫系列1|HTML基础与R语言解析](https://ask.hellobi.com/blog/louwill12/9672)
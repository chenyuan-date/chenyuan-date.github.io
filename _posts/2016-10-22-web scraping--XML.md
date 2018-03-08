---
layout: post            
title: web scraping -- XML                         
author: CY                            
tags: [R]                                      
categories: [R]                           
share: false                              
image:                                      
  background: triangular.png 
---



### XML introduction 

XML（eXtensible Markup Language）又称可扩展标记语言。XML的共性为：和HTML一样，它是一门标记语言，有标记语言的全部特征。XML的特性为：XML是被设计用来传输和存储数据的，而HTML是用来显示数据的，所以XML又有网络数据交换最流行格式的美誉。先看一段XML代码：


```   
<?xml version="1.0" encoding="ISO-8859-1"?>
<nbaplayer>
		<team>
			<city name="houston"> rockets</city>
			<player> james harden</player>
		</team>
		<team>
			<city name="boston"> celtics</city>
			<player> kyrie irving</player>
		</team>
		<team>
			<city name="goldenstates"> worriors</city>
			<player> stephen curry</player>
		</team>
</nbaplayer>		
```

上面的XML代码提供了三名NBA球员的一些基本信息，还是非常容易理解的。正如之前所提到的，XML首先是一门标记语言，它的语法特性和HTML别无二致，XML里的值和名字都被包裹在有含义的标签里，这三名球员都带有主队、姓名和所在城市信息，这种缩进的框架结构能够让我们轻易地看懂XML文档的架构。文档以根元素<nbaplayer>开始，也以它结束。

所以综上我们就了解了，XML是一种类似于HTML的标记语言，它的设计宗旨是传输数据，而非显示数据，在编写XML文档时，我们需要自行定义标签。作为一种纯文本格式，任何有处理纯文本能力的软件都可以拿来处理XML。



### XML语法规则

1.  一个XML文档永远以声明该文档的一行代码来开头：

  `<?xml version=”1.0” encoding=”ISO-8859-1”?>`

version="1.0"用来声明该XML文档的版本号，目前就两个版本：1.0和1.1。encoding="ISO-8859-1"表明声明编码格式。一提到编码，相信有着各种乱码经验的R使用者都应该有体会。



2. XML文档必须要有一个根元素，这个根元素包裹了整个文档，在上面的例子里，根元素是：

  ```
  <nbaplayer>
  ...
  <\nbaplayer>
  ```

XML是用来传输数据的，而这个数据通常是放在具体的XML元素中的。



3. 一个XML元素由起始标签和具体内容来定义，一个元素可以用一个闭合标签来结束，也可以在起始标签里用一个斜杠（/）来闭合。元素里可以包含其他元素、属性、具体数据等其他内容。我们来看上述例子中<city>元素：

  `<city name=”houston”> rockets </city>`

它的组成部分有：元素标题  city ;  起始标签  <city> ; 终止标签  </city>; 数据值    <rockets>         




### R语言解析XML

在R语言中解析XML和解析HTML 是一样的道理，就是对XML原件产生一个能保留住原始文档结构的表征，然后据此从这些文件中提取想要的信息。在R语言中解析XML的过程实际上包括两个步骤，首先XML文件的符号序列会被读取并从元素中创建层次化的C语言树形数据结构，然后这个数据结构会通过使用处理器翻译为R语言的数据结构。

R中导入和解析XML文档的包就叫XML包，我们可以使用`xmlParse( )`函数来解析XML。和htmlParse( )函数较为类似，且看例子：
```
library(XML)
nbadata <- xmlParse(file="D:/Rdata/nbadata.xml")
nbadata 
```

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<nbaplayer>
  <team>
    <city name="houston"> rockets</city>
    <player> james harden</player>
  </team>
  <team>
    <city name="boston"> celtics</city>
    <player> kyrie irving</player>
  </team>
  <team>
    <city name="goldenstates"> worriors</city>
    <player> stephen curry</player>
  </team>
</nbaplayer>
```

简单的一个函数就可以使得一个完整的XML文档被解析到R里面去了。至于如何提取HTML和XML中我们想要的数据信息，方式有多种，但最方便快捷的还是XPath表达式。

### XPath表达式

XPath表达式就是一种可以查询标记语言的方法，可以理解为SQL一样的东西，但是比正则表达式要容易。简单来说，XPath表达式就是选取XML或者HTML文件中节点（元素）的方法。

XPath通过路径表达式（Path Expression）来选择节点信息，跟文件系统路径一样使用“/”符号来分割路径。XPath表达式选择节点的基本规则：
nodename：选择该节点的所有子节点
“/”：选择根节点
“//”：选择任意节点
“@”：选择属性

以前面的XML文档作为例子：
nbaplayer：选取nbaplayer元素所有的子节点
/nbaplayer：选取根节点nbaplayer
//team：选择所有的team子元素
//@name：选择所有的name属性值

除此之外，我们还可以通过给表达式附加一些条件来选择指定的数据，所有的筛选条件都可以附在一个[ ]符号中：
/nbaplayer/team[1]：选择nbaplayer下第一个team子元素
//city[@name]：选择带有name属性的team节点


### SelectorGadget自动生成XPath表达式

一款 Chrome插件: [SelectorGadget](http://selectorgadget.com/)，是可以快速定位节点信息的CSS选择器插件，可以方便快捷的生成网页中想要提取的信息的XPath表示，然后可以直接复制拿来放到R爬虫代码中去。      
按照说明书操作即可，简直是神器！


### references 
[XML website](https://www.xml.com/)      
[[R语言爬虫系列2|XML&XPath表达式与R爬虫应用](https://ask.hellobi.com/blog/louwill12/9807)       

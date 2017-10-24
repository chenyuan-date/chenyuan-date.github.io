---
layout: post            
title: web scraping -- XPath                        
author: CY                            
tags: [Website]                                      
categories: [R]                           
share: false                              
image:                                      
  background: triangular.png 
---



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

安装：别人都可以拖拽安装，我不行，我是[在网站](https://chrome.google.com/webstore/category/extensions?hl=zh-CN)添加的扩展程序          

使用方法：点击这个小工具的拓展程序或者收藏，就可以启动。然后点击要提取的信息，在右下角选择XPath表达式后，网页会自动跳出一个框框，里面的代码就是XPath表达式，把它复制到代码函数里就可以了。      

用户体验：特别棒，不过等成为老司机后，有了火眼金睛，就没必要用这个了。





### References

[R语言爬虫系列2|XML&XPath表达式与R爬虫应用](https://ask.hellobi.com/blog/louwill12/9807)
[extracting data using XPathSApply conditioning on more than one attribute](https://stackoverflow.com/questions/27028100/extracting-data-using-xpathsapply-conditioning-on-more-than-one-attribute)        
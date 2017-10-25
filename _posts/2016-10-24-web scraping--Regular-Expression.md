---
layout: post            
title: web scraping -- Regular Expression                        
author: CY                            
tags: [Website]                                      
categories: [R]                           
share: false                              
image:                                      
  background: triangular.png 
---



HTML/XML网页解析后提取数据一般用专用工具XPath表达式，而更为通用、更加底层的文本信息提取工具非正则表达式莫属。



### 正则表达式 introduction

正则表达式就是`使用一个字符串来描述、匹配一系列某个语法规则的字符串`。通过特定的字母、数字以及特殊符号的灵活组合即可完成对任意字符串的匹配，从而达到提取相应文本信息的目的。在R语言中，有两种风格的正则表达式可以实现，一种就是在基本的正则表达式基础上进行扩展，这和相应的R字符串处理函数相关，另一种就是Perl正则表达式，这种风格的正则我们在R中一般不常用，本文主要还是针对R默认的基础的正则表达式风格进行讲解。

R默认的正则表达式风格包括基础文本处理函数和stringr包中的文本处理函数。在R中二者都支持正则表达式，也都具备基本的文本处理能力，但基础函数的一致性要弱很多，在函数命名和参数定义上很难让人印象深刻。stringr包是Hadley Wickham开发了一款专门进行文本处理的R包，它对基础的文本处理函数进行了扩展和整合，在一致性和易于理解性上都要优于基础函数。本文在介绍基本的正则表达式语法的基础上，通过R中这两种文本处理函数进行实例说明，也好让大家对R语言中正则表达式的基本用法有个大致了解，在后续的爬虫演练中更容易理解一些信息提取的细节知识。



### 正则表达式基本语法

[正则表达式速查表](http://www.jb51.net/shouce/jquery1.82/regexp.html)             

[在线测试正则表达式的网页](https://www.regexpal.com/)         

R中基础文本处理函数和stringr包文本处理函数对于正则表达式的支持情况：

![](https://mmbiz.qpic.cn/mmbiz_png/4lN1XOZshfcib80FWibia4AG7hzk7svc3DsyJSJcJ8DOQmfLauXBJ7B504uV1dq8JvJGUwC36OzzmAI65bPC7zKCQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)



以识别电子邮箱地址为例进行解析。一个正常的电子邮箱账户应该由下面几部分构成：任意字符、数字和符号组成的用户名+@+.+com/net等域名。根据正则表达式的语法规则，我们就可以由这几部分写出邮箱账户的正则表达式：

```
[A-Za-z0-9\._+]+@[A-Za-z0-9]+\.(com|org|edu|net) 
```

其中：

[A-Za-z0-9\\._+]+：A-Z表示匹配任意的A-Z大写字母，所有可能的组合放在中括号里表示可以匹配其中的任一个，加号表示任意字符可以出现1次或者多次，\表示转义，因为.在正则表达式中有特殊含义，想要正常的表达.号必须使用转义符。   

@：邮箱必须的一个符号。       

[A-Za-z0-9]：同前面一样，@符号后面必须有一个包含运营商信息的字符串。

\.：邮箱地址中必须要有的一个点号。

(com|org|edu|net)：列出邮箱地址可能的域名系统，括号内表示分组处理，|符号表示或的含义。



### 基础文本处理

R中常用的支持正则表达式的基础文本处理函数包括grep/grepl、sub/gsub、regexpr/gregexpr等。



### stringr包文本处理



### References

[正则表达式速查表](https://edonymu.com/2017/01/05/reg/)


---
layout: post
title: Unfinished work
author: CY
tags: [R]
categories: [Websites]
share: false
image:
  background: triangular.png 
---



```r
library(XML);
url1<-"http://www.genetics.ac.cn/rcjy/"
url <- htmlParse(url1,encoding="UTF-8")  #把html文件读入R语言中并解析

# 找结点，提出来所有的链接
links <- xpathSApply(url, path = "//a/@href")
# 通过正则提取出来每个导师的链接
supervisor <- grep(pattern="http://sourcedb.genetics.cas.cn/zw/zjrck/", x=links, value=TRUE)
# 去掉冗余，共有89个导师的item
Supervisor <- as.data.frame(unique(supervisor))
```

提取单个网页的信息，以李振声老师的为例：

```r
library(XML);
url2 <-"http://sourcedb.genetics.cas.cn/zw/zjrck/200907/t20090721_2130994.html"
url3 <- htmlParse(url2,encoding="UTF-8")  #把html文件读入R语言中并解析

# 找结点，提出来所有的链接
name <- getNodeSet(url3, path = "//h1//text()")[[1]]
dh <- xpathSApply(url3, path = "//div[@id='dh']//text()")[[2]]
dzyj <- xpathSApply(url3, path = '//div[@id="dzyj"]/script/text()', function(x) { stringr::str_extract(xmlValue(x), '[0-9a-zA-Z\\._]+@[0-9a-zA-Z\\._]+')})
qtbz <- xpathSApply(url3, path = "//div[@id='qtbz']//text()")[[2]]

# 把以上信息整理成表格形式
Li <- c(name, dh, dzyj, qtbz)

Li
```

```
## [[1]]
## 李振声 
## 
## [[2]]
## 86-10-64806605 
## 
## [[3]]
## [1] "zsli@genetics.ac.cn"
## 
## [[4]]
## 小麦远缘杂交研究
```
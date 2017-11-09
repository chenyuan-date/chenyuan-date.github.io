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



### 提取单个网页的信息，以李振声老师的为例：

```r
library(XML)

Li_url <- "http://sourcedb.genetics.cas.cn/zw/zjrck/200907/t20090721_2130994.html"
Li_info <- function(URL) {
  Li_parse <- htmlParse(URL,encoding="UTF-8")  #把html文件读入R语言中并解析
  name <- xpathSApply(Li_parse, path = "//h1//text()", xmlValue)[[1]]  
  # xmlValue是取该标签值得函数
  dh <- xpathSApply(Li_parse, path = "//div[@id='dh']//text()", xmlValue)[[2]]    
  dzyj <- xpathSApply(Li_parse, path = '//div[@id="dzyj"]/script/text()', function(x) { stringr::str_extract(xmlValue(x), '[0-9a-zA-Z\\._]+@[0-9a-zA-Z\\._]+')})    
  qtbz <- xpathSApply(Li_parse, path = "//div[@id='qtbz']//text()", xmlValue)[[2]]    
  data.frame(name, dh, dzyj, qtbz)
}

Li <- Li_info(Li_url)
```


### 依次读出所有PI的网址

```r
PI_url <- "http://www.genetics.ac.cn/rcjy/"
PI_URL <- htmlParse(PI_url,encoding="UTF-8")  #把html文件读入R语言中并解析

# 找结点，提出来所有的链接
links <- xpathSApply(PI_URL, path = "//a/@href")

# 通过正则提取出来每个导师的链接
Supervisor <- grep(pattern="http://sourcedb.genetics.cas.cn/zw/zjrck/", x=links, value=TRUE)

# 去掉冗余，共有89个导师的item
Supervisor <- unique(Supervisor)
length(Supervisor)
```

```
## [1] 89
```


```r
test <- Supervisor[1:4]
df <- data.frame()  # set empty data frame
PI_INFO = function(URL){
  for (i in 1:4) {
    data <- Li_info(test[i])
    df <- rbind(df, data)
  }
  #return(df)
}
df
```

```
## data frame with 0 columns and 0 rows
```

```r
#results <- PI_INFO(test)
#write.table(results,"results.txt",row.names=FALSE)
```



### References      
[R的两个爬虫实例](http://fentwer.leanote.com/post/fentwer-R_web-crawler-example)


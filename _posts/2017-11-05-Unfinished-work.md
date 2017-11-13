---
layout: post
title: Extract webpage -- Example Two
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
  name <- xpathSApply(Li_parse, path = "//h1//text()", xmlValue) 
  # xmlValue是取该标签值的函数
  dh <- xpathSApply(Li_parse, path = "//div[@id='dh']//text()", xmlValue)  
  # dh <- xpathSApply(Li_parse, path = "//div[@id='dh']//text()", function(x) {stringr::str_extract(xmlValue(x), '[0-9]+-[0-9]+-[0-9]+')})
  dzyj <- xpathSApply(Li_parse, path = '//div[@id="dzyj"]/script/text()', function(x) { stringr::str_extract(xmlValue(x), '[0-9a-zA-Z\\._]+@[0-9a-zA-Z\\._]+')})    
  qtbz <- xpathSApply(Li_parse, path = "//div[@id='qtbz']//text()", xmlValue)    
  data.frame(name, dh, dzyj, qtbz)
}

Li <- Li_info(Li_url)
Li
```

```
##     name             dh                dzyj             qtbz
## 1 李振声     联系电话： zsli@genetics.ac.cn       研究方向：
## 2 李振声 86-10-64806605 zsli@genetics.ac.cn 小麦远缘杂交研究

Note: 此处出现这个结果是为了避开个别PI信息不全的情况，后边只要去冗余即可
```

### 依次读出所有PI的网址

```r
PI_url <- "http://www.genetics.ac.cn/rcjy/"
PI_URL <- htmlParse(PI_url,encoding="UTF-8")  #把html文件读入R语言中并解析

# 找结点，提出来所有的链接
links <- xpathSApply(PI_URL, path = "//a/@href")

# 通过正则提取出来每个导师的链接
PI <- grep(pattern="http://sourcedb.genetics.cas.cn/zw/zjrck/", x=links, value=TRUE)

# 去掉冗余，共有89个导师的item
PI <- unique(PI)
length(PI)
```

```
## [1] 89
```

### Extract all information and output

```r
df <- data.frame()  # set empty data frame
PI_INFO <- function(URL_total){
  for (i in 1:length(URL_total)) {
    data <- Li_info(URL_total[i])
    df <- rbind(df, data)
  }
  return(df)
}

IGDB <- PI_INFO(PI)
names(IGDB) <- c("姓名", "电话号码", "电子邮件", "研究方向")

## Remove redundant rows
IGDB <- data[duplicated(IGDB[c('姓名')]),]  # extract duplicated rows

## Output results into file
suppressPackageStartupMessages(library(xlsx))
write.xlsx2(IGDB,"PI_Info.xlsx", sheetName = "IGDB", row.names = F, col.names = T)
```


### References     
[R的两个爬虫实例](http://fentwer.leanote.com/post/fentwer-R_web-crawler-example)



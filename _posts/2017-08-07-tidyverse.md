```
layout: post
title: tidyverse
author: CY
tags: [R]
categories: [tidyverse]
share: false
image:
  background: triangular.png 
```



### `tidyverse` introduction

The tidyverse is an opinionated [collection of R packages](https://www.tidyverse.org/packages)designed for data science. All packages share an underlying philosophy and common APIs. 

大部分数据分析任务，通常有一些固定的操作，操作对应的命令和library也是相对固定的：

![](/images/Tidyverse.png)

首先，导入数据→整理数据，然后进入：转换数据→数据图像化→建立模型这三者的循环中，同时需要一些操作让我们的代码更简洁。在这个过程中，我们经常会用到相应的很多library，悲剧的是我们经常会因为忘记载入相应的包而出现一系列的报错。是时候拿出大杀器`tidyverse`了。

tidyverse包一言以蔽之就是：Tidyverse是一个集成的系统包，里面包含了众多用作数据处理分析的library，并且持续更新中。载入这个包，你就可以高枕无忧了，以上所有命令随意用。哈哈哈哈

### `tidyverse` usage

```
install.packages("tidyverse")
library(tidyverse)
```



### `tidyverse` including packages: 

+ Load the core tidyverse packages:
  + [ggplot2](http://ggplot2.tidyverse.org/), for data visualisation.
  + [dplyr](http://dplyr.tidyverse.org/), for data manipulation.
  + [tidyr](http://tidyr.tidyverse.org/), for data tidying.
  + [readr](http://readr.tidyverse.org/), for data import.
  + [purrr](http://purrr.tidyverse.org/), for functional programming.
  + [tibble](http://tibble.tidyverse.org/), for tibbles, a modern re-imagining of data frames.

- Working with specific types of vectors:
  - [hms](https://github.com/rstats-db/hms), for times.
  - [stringr](https://github.com/tidyverse/stringr), for strings.
  - [lubridate](https://github.com/hadley/lubridate), for date/times.
  - [forcats](https://github.com/hadley/forcats), for factors.
- Importing other types of data:
  - [feather](http://github.com/wesm/feather), for sharing with Python and other languages.
  - [haven](https://github.com/hadley/haven), for SPSS, SAS and Stata files.
  - [httr](https://github.com/hadley/httr), for web apis.
  - [jsonlite](https://github.com/jeroenooms/jsonlite) for JSON.
  - [readxl](https://github.com/hadley/readxl), for `.xls` and `.xlsx` files.
  - [rvest](https://github.com/hadley/rvest), for web scraping.
  - [xml2](https://github.com/hadley/xml2), for XML.
- Modelling
  - [modelr](https://github.com/hadley/modelr), for modelling within a pipeline
  - [broom](https://github.com/dgrtwo/broom), for turning models into tidy data



### References

[tidyverse website]()   

[[为”Tidyverse” 疯狂打call!](https://ask.hellobi.com/blog/mqzhang/9884)]
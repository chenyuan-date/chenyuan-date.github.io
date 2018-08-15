---
layout: post
title: Presentation, Report, Python in Rstudio 
author: CY
description: "R studio"
tags: [Study]
categories: [Study]
share: false
image:
  background: triangular.png
---



### `installr` package

The *installr* package offers a set of R functions for the installation and updating of software (currently, only on Windows OS), with a special focus on R itself. This package has two main goals:

1. To make updating R (on windows) as easy as running a function.
2. To make it as easy as possible to install all of the needed software for R development (such as git, RTools, etc), as well as for reproducible research using R (such as MikTeX, pandoc, etc).

#### Installation

To install the stable version on CRAN:

```
install.packages('installr')
```

To install the latest installr version from GitHub use:

```
if (!require('devtools')) install.packages('devtools'); 
# make sure you have Rtools installed first! if not, then run:
#install.packages('installr')
#install.Rtools()
devtools::install_github('talgalili/installr')
```
#### Usage

If you are using the `Rgui`, you will see a new menu added on your top right (just by "help"), giving you the option to update R, or install new software.

For command line use you can **update R** by running:

```
if(!require("installr")) install.packages('installr')
library("installr")
updateR() 
# this will open dialog boxes to take you through the steps.
# OR use:
# updateR(TRUE) 
# this will use common defaults and will be the safest/fastest option
```

Or **install a new software** simply by running:

```
library("installr")
installr() 
# user can easily select (via a GUI interface) a software to install.
```



### R markdown生成中文自动化报告



#### R Markdown 工作流程：   

1.  打开：打开扩展名为.Rmd的文件。     
2.  编写：利用简易的R Markdown语法编写内容。    
3.  嵌入：嵌入R代码，生成报告所需的输出结果。    
4.  提交：用输出结果代替R代码，把报告转换为幻灯片、pdf、html或者微软Word文件。     

#### 软件安装与配置

```
# 安装rmarkdown包
install.packages("rmarkdown")

# 安装pandoc软件和tinytex软件，现已取代MikTex软件
if(!require("installr"))
{
  install.packages("installr")
  require("installr")
}
if(!require("tinytex"))
{
  install.packages("tinytex")
  require("tinytex")
}

# 安装pandoc
install.pandoc()

# 安装tinytex
install_tinytex() # 超级长的等待时间，差点放弃

# 安装PDF模板
install.packages("rticles")
```

安装完tinytex后，重启一下Rstudio，然后运行 `tinytex:::is_tinytex()`，看结果是不是TRUE，检测是否成功安装。如果不是，换一下安装tinytex的方法：`tinytex::install_tinytex()`

```
# 不断测试找问题
sessionInfo()
Sys.getenv("RSTUDIO_PANDOC")
Sys.which("xelatex")
Sys.which("pdflatex")
```



#### 利用PDF模板生成中文PDF报告步骤：        

1. 选择File - New File - R Markdown - From Template - CTeX Documents          
2. 点击OK，生成PDF模版，保存为xx.Rmd。         
3. 执行xx.Rmd文件 (也就是点击knit)，快捷键：`Ctrl+Shift+K`，生成PDF文档。    
4. 在这个PDF模板，基于自己的主题和内容进行修改，然后重新执行，生成自己所需要的PDF报告文件。    



### 在R studio中运行Python脚本

最新版本的R studio增加了terminal，也就是终端。点击一下左下方 ”Terminal“ ，立马就可以切换Python代码的编写（在上方空白处编写Python代码，下方直接运行，类似于编写R代码）。真正实现左手R，右手Python。 且可支持开多个终端。 如果安装了[`reticulate`](https://github.com/rstudio/reticulate)， 则可以使R 和Python代码同时在R Markdown中运行，且相互继承运算结果。      

```
install.python()
install.package("reticulate") # R Interface to Python
```



### 用R project来管理你的项目

File - New Project - New Directory - Empty Project然后再命名一个新的项目名称就好了。

用project的优点在于易于代码和结果的管理和重新运行。当你把整个project给你的合作者的时候，他们只需要直接运行你的脚本就可以重复你的结果，因为所有数据的相对路径没有改变。



### 运行R bookdown去写书

根据已有模板去写不同部分的代码，然后Build这本书。可以根据自己的需要去生成不同格式的book。模板已存储在自己的邮箱。
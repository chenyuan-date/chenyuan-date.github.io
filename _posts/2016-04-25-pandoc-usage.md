---
layout: post
title: Pandoc usage
author: CY
description: "Introduction of pandoc (a universal document converter) usage"
tags: [pandoc]
categories: [web]
share: false
image:
  background: triangular.png
  feature: 55.png
---

## 1.install pandoc
[pandoc官网](http://pandoc.org/)下载安装window版pandoc   
 
linux 下的安装教程参考[阳志平的博文](http://www.yangzhiping.com/tech/pandoc.html)

## 2. 安装 MiKTeX
pandoc 被称为[格式转换的瑞士军刀](http://yanping.me/cn/blog/2012/03/13/pandoc/)。执行程序文件只有 20 M 左右大小，但是能够在几十种文件格式之间自如的转换，那当然是得依赖各种格式文件所需要库。转换为 pdf 就要用到 MiKTeX，Windows 下推荐使用 CTeX 完整版，对<mark>中文</mark>的支持很好，可以从[CTeX官网](http://www.ctex.org/HomePage)下载完整套件。 
其中：     
- CTeX_2.9.\*.exe (~200 M) 包含 Basic 版 MiKTeX，占用空间小，会根据需要的宏包自动升级。     
- CTeX_2.9.\*_Full.exe (~1.3 G) 包含完整版 MiKTeX。   
- CTeX_2.9.\*_Update.exe (~20 M) 支持从之前版本升级。     

一般 CTeX 要装在 C 盘，CTEX 强制安装在 C 盘是为了避免出现 DLL 动态库调用等错误，增强稳定性。

## 3 将 markdown 文件转换为 pdf
首先win+R，打开运行工具；输入框输入`CMD`命令，之后单击“确定”进入提示符界面。

![pandoc snapshot](https://github.com/chenyuan-date/chenyuan-date.github.io/blob/master/images/pandoc.png "pandoc snapshot")

如果markdown文件中不包含中文字符，那么直接使用下面的命令就可以将markdown文件无缝转换为Latex支持的pdf文件。    
`pandoc infile.md -o outfile.pdf`

如果markdown文件中包含中文字字符，那么上段命令就无法直接转换，可能会报以下错误：  
! Package inputenc Error: Unicode char \u8:鍒?not set up for use with LaTex. pandoc: Error producing PDF from Tex source. See the inputsnc package documentation for explanation. ...

同时产生中间文件：*.tex

为了解决中文编译的问题，需要做以下的工作：     
1.将markdown文档的编码方式改为utf-8。比较简单的办法就是用记事本打开该文档，然后另存为时选择编码方式为utf-8。有可能当你改变编码方式后，文档中的中文全变成乱码了。为避免这种情况，可以在改变编码方式之前先复制文档的全部内容，然后在改变编码方式之后粘贴替换文档中的全部内容，这样就不会出现乱码了。       

2.编译pandoc默认的latex引擎是pdflatex，是不支持中文的，需要手动设置编译时所用的引擎为xelatex，编译命令改为：        
`pandoc infile.md -o outfile.pdf --latex-engine=xelatex`     

3.这时编译可能没有错误了，但是得到的pdf文档中可能所有的中文都没有了。这是字体的问题，因为编译时默认的字体时不支持中文的，所以我们得手动设置中文字体。显然，所设的字体应该为系统中已装的字体，且字体的名字不能写错。有一个办法可以的到系统中所安装的所有字体名，即在控制台中输入命令：fc-list >> C:\fonts.txt。这样，扫到的字体信息就全部被导入到C盘根目录下的fonts.txt文件中了。这里我们选择宋体，字体名称为“SimSun”，于是编译命令改为：      
`pandoc infile.md -o outfile.pdf --latex-engine=xelatex -V mainfont="SimSun" `    
*注意：命令中的`V`是大写*    
*这里字体名也可以不加双引号，但是如果字体名比较复杂（如包含空格）时，不加双引号就可能出错。*    

4.中文字符应该能够显示了，但是可能很多文字已经超出了文档的边界无法显示，这是因为pandoc对中文的支持不太好，不能自动换行。因此选择用另外一种方法：使用编辑好的latex模板来生成pdf。模板的字体得是系统中安装有的字体，然后编译命令改为：      
`pandoc infile.md -o outfile.pdf --latex-engine=xelatex --template=template.latex`      
*注意：如果安装的MiKTeX宏包不全，编译可能会出问题，如找不到exp13.sty等，因此推荐安装完整版的MiKTex。*    
*当然，也可以使用自定义的模板来生成tex和pdf文件。首先使用命令 pandoc -D latex > my.latex 生成一个默认的模板，在对这个模板进行修改，如字体、自动换行等。* 


References:    
[利用Pandoc将markdown文件转化为pdf](http://blog.sina.com.cn/s/blog_5ee56d450101dah2.html)    
[黑魔法利器pandoc](http://yanping.me/cn/blog/2012/03/13/pandoc/)  
[Markdown写作进阶：Pandoc入门浅谈](http://www.yangzhiping.com/tech/pandoc.html)    
[latex template](https://github.com/tzengyuxio/pages/tree/gh-pages/pandoc)    
---
layout: post
title: markdown简明语法
author: CY
description: "test"
tags: [markdown]
categories: [markdown]
share: false
image:
  background: triangular.png
---

This is markdown rules, the name is **markdown**, this is the *rules*, ~~rules~~ 

```
This is markdown rules, the name is **markdown**, this is the *rules*, ~~rules~~ 
```
看到了

## 1. 标题设置（让字体变大，和word的标题意思一样）
在Markdown当中设置标题，有两种方式：

	第一种：通过在文字下方添加“=”和“-”，他们分别表示一级标题和二级标题。(任何数量的 = 和 - 都可以有效果)
	第二种：在文字开头加上 “#”，通过“#”数量表示几级标题。(一共只有1~6级标题，1级标题字体最大)

## 2.强调

斜体             
  
    将需要设置为斜体的文字两端使用1个“*”或者“_”夹起来(符号可跨行，符号可加空格)

粗体

	将需要设置为斜体的文字两端使用2个“*”或者“_”夹起来(符号可跨行，符号可加空格)

删除线

	将需要加删除线的文字两端使用2个“~~”夹起来

高亮
	
	将需要高亮的文字两端使用2个“==”夹起来


## 3.分割线

	单一段落用一个空白行
	连续两个空格，会换行
	三个或更多“-”(空行下方)、“_”、“*”，必须单独一行，可含空格

## 4.区块引用 (Blockquotes)

	翻译成html就是<blockquote></blockquote>，符号后的空格可不要
	通过在文字开头添加“>”表示块注释
	内层引用(嵌套)，符号“>”前的空格必须要
	当>和文字之间添加五个blank时，块注释的文字会有变化(被块包围)

## 5.列表

无序列表

	(“+”、“-”、“*”)+空格+文字。-+*效果一样，但不能混合使用，因为混合是嵌套列表
	列表内容可以很长，不需要手工输入换行符，css控制段落的宽度，会自动的缩放内容

有序列表

	数字(有序或无序)+英文点(.)+空格+文字

嵌套列表

	“-”、“+”、“*”可循环使用，但符号之后的空格不能少，符号之前的空格也不能少

## 6.代码
行内代码块

	简单文字出现一个代码框。使用`<blockquote>`。（`不是单引号而是左上角的ESC下面~中的`）

代码块

	大片文字需要实现代码框。使用空行+Tab或四个空格(默认一个tab占四个空格)。

## 7.链接（Links）

	使用 [描述](链接地址) 为文字增加外链接	
	直接写 [描述](url "可选的title")
    引用方式：
		先定义 [ref_name]:url，然后在需要写入url的地方，这样使用[锚文本][ref_name]，通常的ref_name一般用数字表示，这样显得专业
    简写url：用尖括号包裹url，这样生成的url锚文本就是url本身

## 8.images

	其实和链接一样，只是前面多了个“！”	
	一行表示: ![alt_text](url "可选的title")
    引用表示法: ![alt_text][id],预先定义 [id]:url "可选title"
    直接使用<img>标签，这样可以指定图片的大小尺寸

## 9.脚注（footnote）

脚注[^1]和脚注[^2]
[^1]:脚注1
[^2]:脚注2
	
## 10.表格

	这个必须使用增强版的功能。tools->markdown-->processor(extra)
	key(网上搜的）
	- Email address
	Soar360@live.com
	- License key
	GBPduHjWfJU1mZqcPM3BikjYKF6xKhlKIys3i1MU2eJHqWGImDHzWdD6xhMNLGVp
	bP2M5SN6bnxn2kSE8qHqNY5QaaRxmO3YSMHxlv2EYpjdwLcPwfeTG7kUdnhKE0vV
	y4RidP6Y2wZ0q74f47fzsZo45JE2hfQBFi2O9Jldjp1mW8HUpTtLA2a5/sQytXJU
	Ql/QKO0jUQY4pa5CCx20sV1ClOTZtAGngSOJtIOFXK599sBr5aIEFyH0K7H4BoNM
	iiDMnxt1rD8Vb/ikJdhGMMQr0R4B+L3nWU97eaVPTRKfWGDE8/eAgKzpGwrQQoD+
	nzX1xoVQ8NAuH+s4UcSeQ==


| *Year* | *Temperature (low)* | *Temperature (high)* |
|------|-----|----|
| 1900 | -10 | 25 |
| 1910 | -15 | 30 |
| 1920 | -10 | 32 |

-----

Example
===============
一级标题
=
二级标题
-
# Header 1   
## Header 2   
### Header 3    
#### Header 4   
##### Header 5   
###### Header 6 (末尾为了美观也可以加#，但是标题的大小只取决于行首#的数量）   

--------------------------------------------------------------------
*斜体(Italics)*

*斜体
(Italics)*

_斜体(Italics)_

_斜体
(Italics)_

**粗体(bold)**

**粗体
(bold)**

__粗体(bold)__

__粗体
(bold)__

~~text~~

==text==
*******************************************************************
---
***
___
-------------------------------------------------------------------
>引用
 >>引用中的引用
 >>>第三层引用

>     (>和文字之间超过5个空格之后，会有块出现)
******************************************************************
- 无序列表
+ 无序列表
* 无序列表
___

1. 有序列表
3. 有序列表
5. 有序列表
___

- 嵌套列表
 + 嵌套列表
     - 嵌套列表
 + 嵌套列表
     * 嵌套列表
- 嵌套列表
___
学习使用 `markdown`

<!--lang:python-->
    import numpy as np
	import theano.tensor as T
	from theano import function
	rng = np.random

```
python code
```

---
[不如](http://bruce-sha.github.io "不如的博客")

I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].  

[1]: http://google.com/        "Google" 
[2]: http://search.yahoo.com/  "Yahoo Search" 
[3]: http://search.msn.com/    "MSN Search"

<http://ibruce.info>

------
	| Tables        | Are           | Cool  |
	| ------------- |:-------------:| -----:|
	| col 3 is      | right-aligned | $1600 |
	| col 2 is      | centered      |   $12 |
	| zebra stripes | are neat      |    $1 |
----------------

reference  
http://ibruce.info/2013/11/26/markdown/ 






	
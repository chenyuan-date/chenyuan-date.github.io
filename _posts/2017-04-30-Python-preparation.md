---
layout: post
title: Python Preparation
author: CY
tags: [Python]
categories: [Python]
share: false
image:
  background: triangular.png
---



记得前几年在北京奥运村就看到少儿编程班，那个时候我对编程还一无所知，所以人和人之间的差别。。。哎，不说了，说多了都是泪。
俗话说，工欲善其事，必先利其器。在写这个Python教程之前，我们先来认识一下Python及其相关资源，对Python的整体布局先有一个大概的了解，做到心中有数才好。

首先说明一点，以下关于Python的内容都是基于Python3的。



##  Python特点 

```
Python 是一款易于学习且功能强大的编程语言。 它具有高效率的数据结构，能够简单又有效地实现面向对象编程。Python 简洁的语法与动态输入之特性，加之其解释性语言的本质，使得它成为一种在多种领域与绝大多数平台都能进行脚本编写与应用快速开发工作的理想语言。
```

-  语法简单,易于学习                    
-  自由且开放                       

Python 是 FLOSS （自由/开放源代码软件）的成员之一。简单来说，你可以自由地分发这一软件的拷贝，阅读它的源代码，并对其作出改动，或是将其的一部分运用于一款新的自由程序中。

- 高级语言                
- 跨平台性                  
- 解释性               
- 面向对象                    

Python 同时支持面向过程编程与面向对象编程。在 *面向过程* 的编程语言中，程序是由仅仅带有可重用特性的子程序与函数所构建起来的。在 *面向对象* 的编程语言中，程序是由结合了数据与功能的对象所构建起来的。

- 可扩展性                 
- 可嵌入性                    
- 丰富的库              

Python 标准库的规模非常庞大。它能够帮助你完成诸多事情，包括正则表达式、文档生成、单元测试、多线程、数据库、网页浏览器、CGI、FTP、邮件、XML、XML-RPC、HTML、WAV 文件、密码系统、GUI（图形用户界面），以及其它系统依赖型的活动。



##  Python编辑器的选择

1. 如果是Web开发工程师                                       
  `pycharm`，是一个很好的Python集成开发环境（IDE），针对大型的web框架修改调试，还是需要个大型IDE。据说界面非常友好，但是也据说特别占用内存，一般电脑承受不了，会特别慢。                              

2. 如果是数据处理工程师                      
  spyder或者anaconda。安装后就处理好集成环境。不用再处理环境依赖关系，也包含了numpy，matplotlib和pandas，可以做些数据处理。                    
  `spyder`是个IDE，类似Rstudio。轻便，打开快，但调试不方便，调试时容易卡住。                                     
  `Jupyter notebook` (ipython notebook 最新整合为Jupyter notebook)是集代码、结果、文档三位一体的文学化可重复程序文档。支持40多种程序语言，Python为原生语言。它是Ipython的升级版，而Ipython可以说是一个加强版的交互式 Shell，也就是说，它比在terminal里运行python会更方便，界面更友好，功能也更强大。                                              

3. 如果是初学者                           
  用`python+vscode`，可以智能提示，语法检查，逐行调试等                      

4. 如果是黑客hacker                           
  用`vim`，或者bpython等REPL工具。            




## Python包总览

1. Scientific computing: `Numpy`, `SciPy` (也是安装python包的拦路虎直到有了[conda](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484424&idx=1&sn=05e64a2cb989b458c4fdb4c88d3af24d&scene=21#wechat_redirect))
2. Data analysis:  `Pandas`, 类比于R的数据框操作包
3. 可视化工具 `Seaborn` (配合pandas), `matplotlib` (类比MATLAB), `plotly` (交互式绘图), `ggplot` (类比ggplot2)
4. 网站开发 `web.py`, `Django`, `Flask`
5. 任务调度和流程管理 `Airflow` (pipeline首选)
6. Machine learning: `scikit-learn` (经典), `PyML`, `Tensorflow` (谷歌开发), `pylearn2`, `Orange` (带有图形界面的机器学习包)
7. 网页抓取 `Beautiful Soup`，`requests`,
8. 可重复编程 `Jupyter`
9. 正则表达式 `re`



## Online tools

有这两个工具，你可以不用安装，直接在网页上coding。我觉得对于初学者还是有帮助的，特别是对我这种不想在电脑上安装太多软件的人来说，好处大大滴。                                  

[Jupyter](https://hub.mybinder.org/user/ipython-ipython-in-depth-ezdqr7df/notebooks/binder/Index.ipynb#)                                                                     

[Colaboratory](https://colab.research.google.com/notebooks/welcome.ipynb#scrollTo=8iU2gnJFItM1) 这个是chrome的一个插件，安装了之后就可以双击666了                                                         



##  Python学习资源

[简明 Python 教程](https://bop.mol.uno/)                             

[python3-cookbook](http://python3-cookbook.readthedocs.io/zh_CN/latest/index.html)              

[Python tutorial ](http://www.pythondoc.com/pythontutorial3/index.html#)   

[Python教程 - 廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)                   

[像计算机科学家一样思考Python](https://www.ctolib.com/docs/sfile/think-python-2e/0.html)                          

[Python Tutor](http://www.pythontutor.com/)是`Philip Guo`开发的，通过把计算机运行程序代码的过程可视化的展示来帮助克服程序学习最初的障碍。                   

[Biopython (用到了查查就好)](http://biopython.org/DIST/docs/tutorial/Tutorial.pdf) (PDF)                                                             



cheatsheets                             

[python cheatsheets  ](https://www.datacamp.com/community/data-science-cheatsheets)                                                       

[python for beginners  ](http://www.pythonforbeginners.com/cheatsheet/)                    

[Cheat Sheets for Machine Learning, Data Science, Probability, SQL & Big Data  ](https://www.analyticsvidhya.com/blog/2017/02/top-28-cheat-sheets-for-machine-learning-data-science-probability-sql-big-data/)                             

[Python & R codes for common Machine Learning Algorithms](https://www.analyticsvidhya.com/blog/2015/09/full-cheatsheet-machine-learning-algorithms/)    

[python 3 cheatsheet](https://perso.limsi.fr/pointal/_media/python:cours:mementopython3-english.pdf)                      

http://sixthresearcher.com/wp-content/uploads/2016/12/Python3_reference_cheat_sheet.pdf

http://www.cs.put.poznan.pl/csobaniec/software/python/py-qrc.html

​      


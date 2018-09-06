---
layout: post
title: Determine the optimal cut-point for continuous variables in survival analysis 
author: CY
tags: [Biostatistics]
categories: [Biostatistics]
share: false
image:
  background: triangular.png
---



临床研究中，多数情况下，连续指标与结局的关联不是线性关系，比如血压与心血管疾病发生的关系，可能在血压在升高到一定值后心血管事件发生突然升高，另外连续指标在临床应用时不如分类指标方便，因此临床应用相关指标时总会想办法找到一个正常范围或截断值。对于一般的二分类结局指标，可以用ROC曲线去实现([Youden Index/Cut-Off determination](http://chenyuan.date/2017/06/Youden_index/))，但对于生存类型的数据，寻找截断值比较困难。下面介绍几种方法。



### X-Tile method 

#### x-tile 基本信息

一款[为连续变量找cut-off的小软件x-tile，是耶鲁大学开发的单一功能小软件](https://medicine.yale.edu/lab/rimm/research/software.aspx)，并且于2004发在了clinical cancer research上。下载安装且不需要特殊设置。                                   

软件打开后界面是很简单：左上角是官网，中间的声明中提示不要用于商业用途。可以操作的只有左下角 `Analyze` 和右下角 `Exit`。点击 `Analyze`后，界面同样极简，此时只能点击左上角 `file`  -- `open`，弹出对话框。 导入数据 `.txt` 或是 `.xpf` 格式。                      

x-tile的使用说明书可以通过 `file` - `Users Manual` 路径找到，或者在文件夹 `c:\program files\x-tile\` 中也可以找到。                  

x-tile的示例数据在文件夹：`c:\program files\x-tile\X-tile Sample Data`。     

一旦导入数据，便会在数据所在目录产生一个以 x-tile 开始命名的文件夹，里边包含两个文件：                                  

- `.xpf`: 包含xml格式的数据，也就是该软件将你的数据转化成了 xml 格式。在重新分析该数据时，可以直接输入该文件。                       
- `.set`: 包含如何使 x-tile 产生plot的信息。                 



#### x-tile 分析属性设置

将文件导入x-tile后，就可以开始对后续的分析属性进行设置了。   

- Min Pop Size: 可作为临床亚群最小的病人数目。     

- Min Event No: 可视为有统计意义的亚群中所需的最小事件数目(如死亡)。    

- Min. Pop. Pct: 总人数中可视为临床有效亚人群的比例。

- Min Middle Pop Pct: 总人数中可视为临床有效中间亚人群的比例。   

- Random Pop No: 用来做蒙特卡洛p值模拟的随机人群数目。   

- Alpha: 统计显著的临界值。默认0.05。    

- Training to Validation Set Size Ratio: 训练集和验证集的比例。默认1:1。  

- Display Uncorrected P-values: 显示未经矫正的P值。   

- Monte Carlo Simulations：为了避免多个截断值选择问题，x-tile用蒙特卡洛模拟来矫正p值。     

  - 交叉验证   

  - p值矫正：找到合适的截断值，然后和成千上百的随机人群比较生存差异。      


    

#### x-tile 分析参数设置   

点击 `Show X-tile Setup`，然后出现一个数据界面。界面最左侧显示列名，选中列名，将在中间显示每列的具体内容。点击右侧的 `load` 按钮，则选择选中的列作为参数。

更多的详细内容，参见user manual



#### x-tile 分析结果

x-tile产生的结果包括好几部分，如果在热图中点击左键，则会显示最适合的截断值。注意，x-tile只会对 marker 1 产生plot。 



### Maxstat





Another method to determine the cut-offs in survival analysis 

http://r-addict.com/2016/11/21/Optimal-Cutpoint-maxstat.html

https://github.com/kassambara/survminer/issues/41
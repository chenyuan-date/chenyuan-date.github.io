---
layout: post
title: MetaboAnalyst       
author: CY
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---



[`MetaboAnalyst`](https://www.metaboanalyst.ca/) 是一个在线的用于代谢组学数据分析、可视化和注释，并整合其他组学数据的综合性工具套件。从2009年的 MetaboAnalyst 1.0 采用单一模块实现了代谢组学数据处理和统计分析起，MetaboAnalyst不断更新，分别在2012年和2015年发布了2.0和3.0版本，以满足代谢组学研究不断发展的需要。而且为了更好地应对不断增长的用户需求，MetaboAnalyst 已经迁移到 [Google云服务器](https://cloud.google.com/)。2017年，至少四分之一的代谢组学研究都使用了MetaboAnalyst，说明其已经成为代谢组学数据分析的首选工具之一。2018年发布的4.0版本更新改善了用户界面、提高了可重复性/透明度，实现了支持批量处理、提供改进的来自非靶向质谱(MS)数据的通路注释、支持代谢组学生物标志物meta分析的新模块和多组学分析等功能，并扩展了代谢组和代谢通路数据库，且发布了R软件包 (MetaboAnalystR) 支持本地安装使用，在线分析添加了R 命令的历史面板以实现更透明及可重复的分析。   



## 1 MetaboAnalyst 4.0 框架概述**

MetaboAnalyst 用户界面既提供了现代的“外观和感觉”，也有易于操作的模块化分析途径。所有功能被分为[4类12个模块](https://www.metaboanalyst.ca/faces/docs/Overview.xhtml)：

- **探索性统计分析**: 一般统计、生物标志物分析、双因素/时间序列分析和功效分析。可以接受来自靶向或非靶向的代谢组学数据集的数据。                               
- **功能分析**：代谢物组富集分析、靶向代谢通路分析和根据非靶向代谢组学MS数据预测通路活性 (基于mummichog算法)。                      
- **数据整合和系统生物学**：生物标志物meta分析、联合通路分析和network浏览器。      
- **数据处理和通用功能**：包含通用数据处理工具，如化合物ID转换，批处理效应校正，脂质组学，以及与三个基于网络的实用工具的关联，包含支持NMR的Bayesil, 支持GC-MS的GC-AutoFit以及支持LC-MS的XCMS Online。       

![](../images/MetaboAnalyst1.png) 



![](../images/MetaboAnalyst2.png)


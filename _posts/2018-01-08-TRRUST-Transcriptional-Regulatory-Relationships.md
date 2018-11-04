---
layout: post
title: TRRUST： Transcriptional Regulatory Relationships    
author: CY
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---





[TRRUST(Transcriptional Regulatory Relationships Unraveled by Sentence-based Text mining)数据库](http://www.grnpedia.org/trrust/) 是一个记录转录因子调控关系的数据库，不仅包含转录因子对应的靶基因，也包含了转录因子间的调控关系。目前该数据库只存储了人和小鼠相关的调控信息，而且这些调控关系是通过文本挖掘的方法从文献中整理得到的。                   

对于human而言，包含了800种转录因子，8444个调控关系对；对于mouse而言，包含了828种转录因子，6552个调控关系对。                                        

该数据库提供了人和小鼠的转录因子基因的列表。



1. 以`human`为例，点击[转录因子基因列表](http://www.grnpedia.org/trrust/data/search_list.human.htm), 可以观察到每个转录因子对应的gene  symbol, Entrez ID等信息，可以用于检索。                       

2. 数据库的查询功能 “Search"，不仅可以查询到转录因子的靶基因targets, 也可以查询到调控该转录因子的其他转录因子，即regulators。如果在检索框中输入的基因为一个转录因子对应的基因（如BRCA1），会同时输出该转录因子的靶基因，调控该转录因子的其他转录因子以及和该转录因子具有相同靶基因的其他转录因子，也会输出该基因相关的疾病，GO，KEGG等功能注释。如果输入的基因不是一个转录因子（如CDKN1A），则只会输出调控该基因的转录因子。                                         
3. 除了查询单个基因，还可以通过输入一系列的基因（如差异分析得到的差异基因），通过费舍尔精确检验，分析在哪个转录因子中富集。                     
4. 该数据库还提供了人和小鼠转录因子基因及其调控关系的表格供下载 ('Download')。                  
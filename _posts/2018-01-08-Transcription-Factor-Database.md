---
layout: post
title: Transcription Factor Database 
author: CY
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---



转录因子相关的信息有以下几种：                

1. transcription factors :  转录因子的名称，对应的基因，家族，序列等基本信息            
2. DNA motifs: 转录因子结合区域的保守模式                                 
3. DNA binding sites: 转录因子实际的结合区域              
4. target genes: 转录因子调控的靶基因                            



##footprintDB:综合性的转录因子数据库

[footprintDB](http://floresta.eead.csic.es/footprintdb/index.php) 是一个综合性的转录因子数据库，通过整合 [19个转录因子相关数据库的信息](http://floresta.eead.csic.es/footprintdb/index.php?databases) (点击可查看每个数据库的版本，转录因子数量等统计信息)，构建了一个非冗余的数据集。footprintDB数据库中存储了transcription factors， DNA motifs 和 DNA binding sites 3种信息。                                      

通过点击主页左侧"Search"目录下的"Keywords"。                          

- 检索 Transcription Factor                                                            

  在输入框里输入转录因子的名字，点击即可搜索。搜索结果包括转录因子对应的基因，物种，蛋白编号，蛋白序列， 序列, motif， binding sites 等信息。                       

- 搜索 DNA Binding Motif                                                         

  包含了motif的编号，对应的物种，一致性序列，sequence logo, PSSM矩阵，binding  sites 等信息。                           

- DNA binding Sites                            

  包含了结合位点的编号，序列，对应的motif和转录因子等信息。                      

- Motif compare                              

  点击主页左侧"Search"目录下的"Sequences"，输入一个motif的PSSM矩阵或者binding区域的序列，可以将该motif与数据库中已有的motif比对，确定是否为已知的motif。                   

  这个功能运行时间会很久，建议提供邮箱，运行完毕后会将结果发送到与邮箱里。             




## TRRUST: 转录因子调控关系数据库                    

[TRRUST(Transcriptional Regulatory Relationships Unraveled by Sentence-based Text mining)数据库](http://www.grnpedia.org/trrust/) 是一个记录转录因子调控关系的数据库，不仅包含转录因子对应的靶基因，也包含了转录因子间的调控关系。目前该数据库只存储了人和小鼠相关的调控信息，而且这些调控关系是通过文本挖掘的方法从文献中整理得到的。                                     

对于human而言，包含了800种转录因子，8444个调控关系对；对于mouse而言，包含了828种转录因子，6552个调控关系对。                                                                  

该数据库提供了人和小鼠的转录因子基因的列表。                                                 

1. 以`human`为例，点击[转录因子基因列表](http://www.grnpedia.org/trrust/data/search_list.human.htm), 可以观察到每个转录因子对应的gene  symbol, Entrez ID等信息，可以用于检索。                                                                     
2. 数据库的查询功能 “Search"，不仅可以查询到转录因子的靶基因targets, 也可以查询到调控该转录因子的其他转录因子，即regulators。如果在检索框中输入的基因为一个转录因子对应的基因（如BRCA1），会同时输出该转录因子的靶基因，调控该转录因子的其他转录因子以及和该转录因子具有相同靶基因的其他转录因子，也会输出该基因相关的疾病，GO，KEGG等功能注释。如果输入的基因不是一个转录因子（如CDKN1A），则只会输出调控该基因的转录因子。                                                                     
3. 除了查询单个基因，还可以通过输入一系列的基因（如差异分析得到的差异基因），通过费舍尔精确检验，分析在哪个转录因子中富集。                                                 
4. 该数据库还提供了人和小鼠转录因子基因及其调控关系的表格供下载 ('Download')。                   



## Harmonizonme: 转录因子靶基因数据库

[Harmonizonme数据库](http://amp.pharm.mssm.edu/Harmonizome/) 将各个`Resource`来源数据库中的原始信息加以整理，得到更加直观，方便使用的数据集`Datasets`，然后将所有的整理好的信息存储在同一个数据库中。         

目前该数据库包含来自66个[Resources数据库](http://amp.pharm.mssm.edu/Harmonizome/about#resources)，114个数据集datasets, 共有57620个基因，295496个属性，71927784个相互作用关系。       

找转录因子靶基因，在首页输入 "transcription factor targets", 然后可以看到有6个靶基因数据库。选择其中的一个打开，会显示该数据库包括的所有转录因子的靶基因信息，点击每个转录因子，可以看到相关的靶基因。          

除了在线浏览特定转录因子的靶基因外，还可以方便的下载该数据库中的数据集。在"Data Access" 项目下的“Downloads"，链接即可下载。通过该数据库可以方便的得到转录因子和靶基因之间的调控关系。                                          

 


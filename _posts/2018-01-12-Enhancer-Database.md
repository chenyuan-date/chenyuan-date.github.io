---
layout: post
title: Enhancer Database   
author: CY
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---



**增强子 (Enhancer)**: 基因组上的一段DNA序列，可与转录因子配合调控基因的表达。人体所有细胞基因组相同，但是细胞的形态和功能各不相同，这很大程度上是由增强子决定的。              

**超级增强子较普通增强子表现出更高的转录因子密度，并且经常与控制体细胞中细胞状态和分化的关键谱系特异性的基因相关，它促进基因表达的能力更强，主要负责调控决定细胞身份的基因的表达**。大部分超级增强子在细胞内处于抑制状态，一般只有少量决定细胞身份的超级增强子被打开，一旦细胞内超级增强子打开错误，或靶向的基因错误，就导致肿瘤的发生。很多关键致癌基因都是超级增强子驱动的。肿瘤发生过程中，肿瘤细胞还会在致癌基因处构建超级增强子，用于驱动致癌基因的表达。相比单个基因，肿瘤细胞更依赖超级增强子。这意味着超级增强子或许是不错的抗肿瘤靶点，表明了超级增强子在生物学和医学研究中具有重要的作用和广泛的应用。



### [SEdb (**S**uper-**E**nhancer **d**ata**b**ase)](http://www.licpathway.net/sedb/)                     

现有的两个超级增强子的数据库 [dbSUPER](http://asntech.org/dbsuper/) 和 [SEA (Super-Enhancer Archive)](https://sea.nebulagene.com/SEA/) 仅提供了关于超增强子的基本信息，例如其基因组位置，细胞或组织类型和相关基因。数据库 [SEdb](http://www.licpathway.net/sedb/) 则提供了有关超级增强子的详细遗传和表观遗传注释信息，有助于阐明超级增强子相关功能并发现潜在的生物学效应。           

在`Data-Browser`，可以通过“数据来源”，“生物样本类型”，“组织类型”和“生物样本名称” 进行浏览。比如我们选择组织类型中lung进行浏览，结果显示肺组织中所有样本的超级增强子，还包括基本信息，比如样本ID号，数据来源，样本类型以及样本名字等。  

在 `Search`，数据库提供了三种查询方法，包括 `Tissue category-based`，`gene-based`，`sample-based` 的查询。  组织查询：选择 `Tissue` -- `Lung`, 点击 “SE ID“ 可以更详细的查看该增强子的信息，包括：      

- 超级增强子的一般信息        

- 超级增强子区域中常见的SNP，eQTL，风险SNP，TFBS，CRISPR / Cas9靶位点，DHS和增强子        

- 通过不同的鉴定策略提供可能与超级增强子相关的基因                 

- 超级增强子元件的详细信息和分析                        

- 与此超级增强子重叠的样本中标识的其他超级增强子的链接，相当于区域富集分析                                     

其他的搜索方法大致相同，只是需要自己多点点熟悉一下界面。                    

在 `Analysis`，数据库提供了三个在线分析工具：**Gene-SE Analysis**，**SNP-SE Analysis** 和 **Overlap Analysis**。                            

在`Genome-Browser`，数据库提供了数据可视化工具，可以查看超级增强子的临近信息。                 

在`Download`，数据库为每个样本提供超级增强子和超级增强子元件的下载。用户可以选择bed格式或者是csv的格式进行下载，还支持所有超级增强子的打包下载。                                    



### [dbSUPER](http://asntech.org/dbsuper/)           






### [SEA (Super-Enhancer Archive)](https://sea.nebulagene.com/SEA/)
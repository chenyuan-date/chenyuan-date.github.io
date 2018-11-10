---
layout: post
title: Cancer Database 
author: CY
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---



## **综合性肿瘤数据库**

### [**TCGA**](https://cancergenome.nih.gov/)       

[The Cancer Genome Atlas (TCGA)](https://cancergenome.nih.gov/)  是综合性肿瘤数据库，关注与癌症的发生和发展相关的分子突变图谱。              

由于TCGA是一个庞大的，使用最为广泛的数据库，所以详细介绍在[另一个专题](http://chenyuan.date/2018/01/TCGA-Database/)。                              



### [**ICGC**](https://icgc.org/)              

International Cancer Genome Consortium (ICGC，国际癌症基因组联盟) 由[亚洲、澳大利亚、欧洲、北美和南美17个行政区的89个项目](https://icgc.org/icgc/cgp)，包括25,000个肿瘤基因组。目的是 `To obtain a comprehensive description of genomic, transcriptomic and epigenomic changes in 50 different tumor types and/or subtypes which are of clinical and societal importance across the globe`.

在[ICGC Data Portal](https://dcc.icgc.org/) 输入想要查询的内容即可在线使用。    

点击 [ICGC Data Portal - Cancer Projects](https://dcc.icgc.org/projects) 可以看出TP53依然是突变频率最高的基因。通过左侧的选择栏，还可以看不同肿瘤类型和很多不同国家人群的情况。在该页面下方还有突变整体比较的图，每个点表示每个个体外显子区每MB区域体细胞突变的数目，不同区域的不同癌症归为一组展示。澳大利亚的皮肤癌(MELA-AU)整体突变率最高，英国的慢性骨髓病（CMDI-UK）突变频率最低。这里面有地域差异，也有疾病差别。          

点击 [ICGC Data Portal - Data Analysis](https://dcc.icgc.org/analysis) 可以做在线富集分析，队列比较分析，集合分析和利用OncoGrid展示数据。        

点击 [ICGC Data Portal - DCC Data Releases](https://dcc.icgc.org/releases)，可以下载所有的突变数据的summary。                     

点击 [ICGC Data Portal - Data Repositories](https://dcc.icgc.org/repositories)，可以下载来自WGS，RNA-seq等的fasta/bam格式数据，但是需要先申请下载权限才可以。[具体的要求在此](https://docs.icgc.org/portal/access/)。           



如何使用搜索：   

比如输入一个基因 (BRCA1)，`Summary` 有关于基因的详细信息。`Mutations` 有基因突变频率分布以及突变位点分布，所在基因组区域的展示，该基因最频繁突变位点，突变位点影响注释等。`Targeting Compounds` 有靶向突变位点的小分子化合物，对于药物设计有重要意义。以及小分子药物的属性、其它靶点、正在开展的临床试验等。             

还可以搜索某一癌症类型(breast cancer)，会显示不同亚型和不同国家的该癌症的详细信息。               



### [**UCSC XENA**](https://xena.ucsc.edu/)                    

`UCSC Xena`功能基因组浏览器是集分析、可视化、Galaxy与一体的新一代在线数据分析和可视化平台。现有91个队列的1098个公共数据集包括 TCGA, ICGC, TARGET, GTEx, CCLE等都进行了标准化处理。因此不同的数据集之间可以组合比较。

1. 热图的方式可以进行单基因和多基因的表达、突变、拷贝数变异、样品属性的关联展示。
2. 对任何展示的变量(不同表型病人的比较，不同基因表达的比较，突变有无的比较，甲基化水平的变化)都可以进行生存分析，绘制KM-plot，计算其对病人生存率的影响。
3. 热图可以根据任一变量排序，然后查看其它变量的变化。如根据药物处理状态排序，查看基因的表达或修饰的变化。

此外 Xena 提供了`ICGC Data Portal`的`Chrome`扩展，可以在`ICGC`的界面加入XENA的`Heatmap`展示  (好用不好用还没有有待进一步探索)。该数据库的网站提供了[使用视频](https://xena.ucsc.edu/getting-started/)，可以参考一下。               



### [**COSMIC**](https://cancer.sanger.ac.uk/cosmic/)             

Catalogue Of Somatic Mutations In Cancer (COSMIC) 是世界上最大最全面的有关肿瘤的体细胞突变以及其影响的资源。主要提供多种肿瘤细胞基因组中的CNA、甲基化、基因融合、SNP及基因表达信息等。主页面分为项目、数据管理、工具、帮助、搜索框等几大块，简洁清晰。   



### [**UCSC Cancer Genomics Browser**](http://genome.ucsc.edu/index.html)     

UCSC Cancer Genomics Browser是一个整合、可视化、分析癌症基因组学和临床数据的网络分析工具。该平台目前共有355个数据集，包括了来自71870例样本的全基因组数据。

用户可以通过它浏览基因组的任何一部分，并且同时可以得到与该部分有关的基因组注释信息，如已知基因、预测基因、表达序列标签、mRNA、CpG岛，克隆组装间隙和重叠、染色体带型、小鼠同源性等。



### [**Tumor Portal**](http://www.tumorportal.org/)

Tumor Portal 可以通过三种方式来探索肿瘤相关数据。即肿瘤类型，基因和图表。      



## **肿瘤基因数据库**

### [**ArrayMap**](https://arraymap.org/)    

ArrayMap是由苏黎世大学分子生命科学研究所构建的，提供预处理过的肿瘤基因组芯片数据以及CNA 图谱。arrayMap数据库为高分辨率致癌基因组CNA数据的meta分析和系统级数据集成提供了切入点。

用户可通过关键字搜索自己感兴趣的样本或者搜索特定文献中的样本，并在此基础上分析感兴趣的基因或基因组片段上的CNA 。用户还可以选择两个样本来比较二者的CNA 的差异。

收录内容：

- ![img](https://mmbiz.qpic.cn/mmbiz_png/EuxW25oibqb2QMsCiamuDZYibhFIJIbo7KQOanibaqTr9oG7LJAicLsQDpOkuP0VTPzQvmWg6G1VLl3DVqzCdw9FKLA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)62032 genomic array profiles
- ![img](https://mmbiz.qpic.cn/mmbiz_png/EuxW25oibqb2QMsCiamuDZYibhFIJIbo7KQfpzezLshvdicjcq6LvPA0iaicqDTWQ9PlF5DhzKxG2H0wZwia4YXUEicweg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)901 experimental series
- ![img](https://mmbiz.qpic.cn/mmbiz_png/EuxW25oibqb2QMsCiamuDZYibhFIJIbo7KQ1ic97SiawNIDT7MZkibGWicTNgiaCsQh6uHtMDGUricnCoccVmq9qgiaQGChw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)267 array platforms
- ![img](https://mmbiz.qpic.cn/mmbiz_png/EuxW25oibqb2QMsCiamuDZYibhFIJIbo7KQz2ydiaymSmjYXJZPEibdWoPeEMCm0Sm9cRclicFQCaueZ1SAUx1enibUVQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)251 ICD-O cancer entities
- ![img](https://mmbiz.qpic.cn/mmbiz_png/EuxW25oibqb2QMsCiamuDZYibhFIJIbo7KQHee25sTBqecjfCK3icPHoicJQ8NibW1DJeCRHAYhE7y03eqnYVQoqwC7w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)709 publications (Pubmed entries)



### [**Cancer Hotspots**](https://www.cancerhotspots.org/#/home)      

Cancer Hotspots数据库由Memorial Sloan Kettering癌症中心的Kravis分子肿瘤学中心维护，提供大规模癌症基因组学数据中发现的在统计学上有显著复发突变的信息。

目前，Cancer Hotspots里面包含有24592个肿瘤样品中鉴定的单残基和框内indel突变热点。用户还可按照gene、residue、type、variants等对其内容进行排列查看。



### [**OncoKB**](http://oncokb.org/#/)     

OncoKB是由Memorial Sloan Kettering癌症中心（MSK）维护的全面的精准肿瘤学知识库，包含来自FDA，NCCN或ASCO，ClinicalTrials.gov和科学文献的专业指导方针和建议，治疗策略，肿瘤专家或肿瘤协会共识，参考文献等信息。

OncoKB目前包含有关554种癌症基因特定改变的详细信息，还有1级（FDA批准）、2级（标准护理）的治疗信息，3级临床证据和生物学证据。  



## **肿瘤转录组数据库**

### [**ArrayExpress**](https://www.ebi.ac.uk/arrayexpress/)   

ArrayExpress是欧洲生物信息协会（EMBL-EBI）下属的功能基因组数据库，收集整理基于芯片和测序的基因组学实验的数据，以支持可重复的研究。数据库目前已收集了71416次实验的46.89TB存档数据。

在帮助页面有详细的在线教程，供用户学习如何搜索、提交数据。



### [**Oncomine**](https://www.oncomine.org/)    

Oncomine是大型的肿瘤基因芯片数据库，致力于收集、标准化并分析肿瘤样本的基因表达谱芯片数据。目前，Oncomine 已经收集了来自715 个数据集的86 733 个样本的基因表达数据，可用于分析基因表达差异、预测共表达基因等，并可根据肿瘤分期、分级、组织类型等临床信息进行分类。
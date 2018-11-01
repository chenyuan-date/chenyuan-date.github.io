---
layout: post
title: 	SNP Genotyping  
author: CY
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---



## 遗传变异的种类

**单核苷酸多态性(SNP)**，**小片段的插入缺失(Indel)**，**结构变异(SV)**，**拷贝数变异(CNV)**等等。区分这些变异简单的方法就是变了几个，其中SNP是单个核苷酸的改变，indel通常是50bp以下的变异，SV和CNV则要更长。      

**SNP** 和 **SNV** 都是单碱基的突变，但是SNP 是多了一个**频率属性**的SNV，比如在群体中1%以上。     

**SNP**（single nucleotide polymorphism，单核苷酸多态性）：个体间基因组DNA序列同一位置单个核苷酸变异(替代、插入或缺失)所引起的多态性；不同物种个体基因组 DNA 序列同一位置上的单个核苷酸存在差别的现象。SNP 在CG序列上出现最为频繁，而且多是C转换为T ，因为CG中的C 常为甲基化的，自发地脱氨后即成为胸腺嘧啶。一般而言，SNP 是指变异频率大于1%的单核苷酸变异，主要用于高危群体的发现、疾病相关基因的鉴定、药物的设计和测试以及生物学的基础研究等。而在研究癌症基因组变异时，相对于正常组织，癌症中特异的单核苷酸变异是一种somatic mutation，称为**SNV**（single nucleotide variants, 单核苷酸位点变异）。      

一般来说，SNP、SNV 的应用场景不同。其中，SNP 一般指健康人群中的无害突变，比如不同种族来源的人群中存在的不同的SNP, 可以参照千人基因组计划的研究结果。而SNV 一般指一些明确有害的或者有潜在有害的单核苷酸突变，比如某些遗传疾病或者肿瘤的一些突变。       

全基因组SNP突变可以分成**6类（C>A, C>G, C>T, A>C, A>G, A>T）**。以A:T>C:G为例，此种类型SNP突变包括A>C和T>G。由于测序数据既可比对到参考基因组的正链，也可比对到参考基因组的负链，当T>C类型突变出现在参考基因组正链上，A>G类型突变即在参考基因组负链的相同位置，所以通常也会将T>C和A>G划分成一类。



## Biallelic and Multiallelic

 **Biallelic** 表示在基因组的某个位点上有两个等位基因，即可以有一个突变等位基因。也就是说这个位置上可能存在一个和参考基因组相同的碱基和一个和参考基因组不同的碱基或者是一个deletion。**Multiallelic** 多等位基因表示在基因组的某个位点可以观测到三个或者多个等位基因，在vcf文件中可以看到两个或者三个非参考基因组的突变。多等位基因并不常见，在各种vcf文件相关工具中，都可以统计这两种信息。

More alleles, larger diversity （等位基因越多，多样性越大）



## Minor allele frequency (MAF) 

All the MAF can be found here https://www.ncbi.nlm.nih.gov/projects/SNP/docs/rs_attributes.html     

**MAF** refers to the frequency at which the *second most common* allele occurs in a given population.                     

SNPs with a MAF of 0.05 (5%) or greater were targeted by the [HapMap project](https://www.ncbi.nlm.nih.gov/variation/news/NCBI_retiring_HapMap/).               

MAF is widely used in population genetics studies because it provides information to differentiate between common (MAF > 5%) and rare (MAF < 5%) variants in the population.     

Mutation: MAF ≤1%
Polymorphism: MAF >1%



## Genotyping 基因分型

Genotyping 是通过检测个体DNA序列来确定个体基因组成（基因型）差异的实验过程。   
---
layout: post
title: Breast cancer PAM50 subtypes
author: CY
tags: [Biology]
categories: [Biology]
share: false
image:
  background: triangular.png 
---



### PAM50

PAM50 stands for `Prediction Analysis of Microarray 50`. It tests a sample of the tumor (removed during a biopsy or surgery) for a group of 50 genes. Along with other factors, the results of the PAM50 test help predict the chance of metastasis (when cancer spreads to other organs). It was proposed by [Parker et al.](http://ascopubs.org/doi/abs/10.1200/JCO.2008.18.1370) in 2009. 

The PAM50 is a RT-qPCR assay that measures the expression of 50 classifier genes and five control genes to identify the intrinsic subtypes known as Luminal A, Luminal B, HER2-enriched and Basal-like. Along with a categorical classification of breast cancer subtype, it also provides quantitative values for proliferation, luminal gene expression, *ESR1*, *PGR* and *ERBB2*.

Gene expression profiling by microarray has given us insight into the complexity of breast tumors and can be used to provide prognostic information beyond standard clinical assessment. 

For example:

 - the 21-gene OncotypeDx assay (Genome Health Inc, Redwood City, CA) can be used to risk stratify early-stage estrogen receptor (ER) –positive breast cancer.
 - Another strong predictor of outcome in ER-positive disease is proliferation or genomic grade.
 - the 70-gene MammaPrint (Agendia, Huntington Beach, CA) microarray assay has shown prognostic significance in ER-positive and ER-negative early-stage node-negative breast cancer.

Parker *et al* (2009) published microarray data (GEO data set **GSE10886**)，数据可以比较方便的下载重现整个思路，只需要测定50个基因的表达量即可。



### PAM50 classifier usage 

The centroids, gene lists, and R code to produce the classification are all available along with the clinical information for the **training set** on this page: https://genome.unc.edu/pubsup/breastGEO/

Specifically, the **R code and supporting data** files are here: https://genome.unc.edu/pubsup/breastGEO/PAM50.zip

And the **centroids** alone are here: https://genome.unc.edu/pubsup/breastGEO/pam50_centroids.txt

In addition, this document provides additional information regarding classification of the PAM50 plus Claudin-low calls https://genome.unc.edu/pubsup/breastGEO/Guide%20to%20Intrinsic%20Subtyping%209-6-10.pdf

Anyone **running PAM50** (or any classifier based on relative measurements such as expression) should understand the concepts in this paper: http://www.breast-cancer-research.com/content/pdf/s13058-015-0520-4.pdf



### 30个基因的分类效果

[2011年一篇文章](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3242517/) 提出了Montreal cohort of 87 patients的30个基因，也可以比较好的区分这些亚型：

![](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3242517/bin/bjc2011355f3.jpg)

这两个基因集的交叉，Of these 30 genes, **only 7 of the 30 genes** overlapped with the PAM50 (*FOXA1*, *MLPH*, *ESR1*, *SLC39A6*, *NAT1*, *GRB7 and ERBB2*) (Parker *et al*, 2009)


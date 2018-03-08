---
layout: post
title: Multi-Omics Factor Analysis (MOFA)
author: CY
tags: [Study]
categories: [Study]
share: false
image:
  background: triangular.png 
---



记录一下今天下午EMBL组的Britta Velten下山来给我们讲多组学因子分析的工具（MOFA）。此人是EMBL Huber组的博后，他们实验室主要进行多组学分析和统计计算。今天她讲的这个工具是他们实验室开发的，综合多组学数据进行分析，致力于找到因子的最优组合，以表征疾病。



### Integration of data from different omics is challenging

**Challenges:** 

1. Heterogeneous data sets have to be modeled under different statistical assumptions
2. Appropriate regularization strategies are required to avoid over-fitting
3. Approaches based on marginal correlations suffer from spurious associations and a high multiple testing burden
4. Missing data is commonly encountered, both in terms of single values as well as individual samples that miss a certain assay.



### Exploratory analysis: From single- to multi-omics

Principle component analysis (PCA) decomposes high-dimensional data Y into a low-dimensional representation by uncorrelated factors.

**An extension to multi-omic data requires:**

1. Disentangling variation between different data sets:
   1. Which axes of variation are unique to a single data set?
   2. Which capture co-variation between different biological layers?
2. Accounting for heterogeneity of different data sets
3. Characterization and annotation of the major axes of variation



### Multi-Omics Factor Analysis (MOFA)

**MOFA** is a computational method for `discovering the principal sources of variation` in a multi-omics dataset. MOFA infers a set of (hidden) factors that capture biological and technical sources of variability across a joint low-dimensional representation of multiple data sets, thereby enabling a variety of downstream analyses, including factor annotation, data imputation and the detection of outlier samples. 



Important properties of **MOFA** for multi-omic applications:

1. Interpretability by two-level sparsity                    
   1. factor- and view-wise sparsity by an ARD prior                       
   2. factor- and feature-wise sparsity by a spike and slab prior            
2. Scalable inference using a variational framework                     
3. Handling of missing values                          
4. Modeling non-Gaussian views                     



###  References

[PMBio/MOFA](https://github.com/PMBio/MOFA)

[Multi-Omics factor analysis disentangles heterogeneity in blood cancer](https://www.biorxiv.org/content/early/2017/11/10/217554.full.pdf+html)
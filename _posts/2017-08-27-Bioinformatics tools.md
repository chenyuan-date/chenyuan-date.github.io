---
layout: post
title: Tools for Bioinformatics analysis
author: CY
description: "A comprehensive summary of tools for bioinformatics analysis"
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---



# fastq格式相关

## SRAtoolkit 

SRA数据库下载公用数据时的工具   

网址 https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=toolkit_doc    


## fastx toolkit

a collection of command line tools for Short-Reads FASTA/FASTQ files preprocessing   
有各种各样的小功能，比如提取反向互补序列等等。   
网址 http://hannonlab.cshl.edu/fastx_toolkit/     

## fastqc

A quality control tool for high throughput sequence data   
评估测序数据质量  
网址 https://www.bioinformatics.babraham.ac.uk/projects/fastqc/  

## MultQC

Aggregate results from bioinformatics analyses across many samples into a single  report  
一次同时生成多个数据质量报告，省时省力方便对比，支持fastqc  
网址 https://github.com/ewels/MultiQC  
网址 http://multiqc.info/docs/  

## Trim Galore

around Cutadapt and FastQC to consistently apply quality and adapter trimming to FastQ files, with some extra functionality for MspI-digested RRBS-type (Reduced Representation Bisufite-Seq) libraries   
和fastqc出自一家，可以和fastqc结合使用，用来清洗原始数据。  
网址 https://www.bioinformatics.babraham.ac.uk/projects/trim_galore/

## Trimmomatic

A flexible read trimming tool for Illumina NGS data  
专门清洗illumina测序数据的工具  
网址 http://www.usadellab.org/cms/index.php?page=trimmomatic

## khmer

working with DNA shotgun sequencing data from genomes, transcriptomes, metagenomes, and single cells.  
可以对原始测序数据进行过滤等  
网址 http://khmer.readthedocs.io/en/v2.1.1/user/scripts.htm

# BED格式相关

## bedops

the fast, highly scalable and easily-parallelizable genome analysis toolkit  
网址 https://bedops.readthedocs.io/en/latest/index.html   
玩转bed格式文件，速度比bedtools快  

## bedtools

a powerful toolset for genome arithmetic   
网址 http://bedtools.readthedocs.io/en/latest/index.html   
最知名的bed文件相关工具，但是和samtools并非出自一家

# SAM/BAM格式相关

## samtools

Utilities for the Sequence Alignment/Map (SAM) format  
网址 http://www.htslib.org/doc/samtools.html  
有这一个就够了

# SNP（VCF/BCF）相关

## GATK

网址 https://software.broadinstitute.org/gatk/documentation/  
使用率最高的软件

## bcftools

utilities for variant calling and manipulating VCFs and BCFs  
网址 http://www.htslib.org/doc/bcftools.html  
对vcf格式的文件进行各种操作

## vcftools

网址 https://vcftools.github.io/man_latest.html  
和bcftools类似

## snpEFF

Genetic variant annotation and effect prediction toolbox  
适合用来进行snp注释  
用法 http://snpeff.sourceforge.net/SnpEff_manual.html  
网址 http://snpeff.sourceforge.net/  
也可以注释ChIP-seq  
支持非编码注释，如组蛋白修饰  

## samtools mpileup

Utilities for the Sequence Alignment/Map (SAM) format  
网址 http://www.htslib.org/doc/samtools.html  

# ChIP-seq/motif

## MACS

Model-based Analysis of ChIP-Seq  
主要用于组蛋白修饰产生的narrow peaks(H3K4me3 and H3K9/27ac)  
transcription factors which are usually associated with sharp and solated peaks  
网址 http://liulab.dfci.harvard.edu/MACS/README.html  

## MACS2

网址 https://github.com/taoliu/MACS  
MACS的升级版本，也可以用来找broad peak  

## SICER

highly recommended for a practical ChIP-seq experiment design and can be used to account for local biases resulting from read mappability, DNA repeats, local GC content  
网址https://www.genomatix.de/online_help/help_regionminer/sicer.html  
出来怼MACS，主要用来找一些比较宽的peak,类似于H3K9me3 和 H3K36me3。

# large sequences alignment

长序列比对常用的几个软件  

## MUMer

rapid alignment of very large DNA and amino acid sequences  
网址 http://mummer.sourceforge.net/examples/  
网址 http://mummer.sourceforge.net/manual/   

## GMAP

GMAP: A Genomic Mapping and Alignment Program for mRNA and EST Sequences  
网址 http://research-pub.gene.com/gmap/  

## BLAT

Blat produces two major classes of alignments:at the DNA level between two sequences that are of 95% or greater identity, but which may include large inserts；at the protein or translated DNA level between sequences that are of 80% or greater identity and may also include large inserts.  
网址 https://genome.ucsc.edu/goldenpath/help/blatSpec.html  

# short reads alignment

短序列比对，二代测序数据比对

## BWA

Burrows-Wheeler Alignment Tool  
mapping low-divergent sequences against a large reference genome  
It consists of three algorithms: BWA-backtrack, BWA-SW and BWA-MEM.  
网址 http://bio-bwa.sourceforge.net/bwa.shtml  
网址 https://github.com/lh3/bwa

## GSNAP

Genomic Short-read Nucleotide Alignment Program  
网址 http://research-pub.gene.com/gmap/

## Bowtie

works best when aligning short reads to large genomes  
not yet report gapped alignments  
网址 http://bowtie-bio.sourceforge.net/manual.shtml

## Bowtie2

ultrafast and memory-efficient tool for aligning sequencing reads to long reference sequences  
supports gapped, local, and paired-end alignment modes  
网址 http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#reporting  
和上一代的区别在于支持gapped alignments

## HISAT2

Tophat的继任者，基于HISAT和Bowtie2  
HISAT2的速度比STAR快一些  
网址 http://ccb.jhu.edu/software/hisat2/manual.shtml

## STAR

Spliced Transcripts Alignment to a Reference  
网址 https://github.com/alexdobin/STAR  
网址 https://github.com/alexdobin/STAR/blob/master/doc/STARmanual.pdf

# genome guide assemble

## stringtie

highly efficient assembler of RNA-Seq alignments into potential transcripts  
对于可变剪切的发现相对准确  
网址 https://ccb.jhu.edu/software/stringtie/

## Cufflinks

基本不用了。。。  

## IDP

Isoform Detection and Prediction tool   
gmap+hisat2,也就是长短序列比对相结合，效果不错  
网址 https://www.healthcare.uiowa.edu/labs/au/IDP/IDP_manual.asp

# de novo assemble/gene prediction

下面几个软件结合起来就是一个从组装到注释到计算效率的过程

## trintiy

倾向于预测长的可变剪接  
新版本从之前的过度预测越来越倾向于有所保留  
比较耗资源，一般1个CPU最好分配6G-10G  
可以有参或者无参转录组拼接  
网址 https://github.com/trinityrnaseq/trinityrnaseq/wiki

## oases

通常得到的N50比较高  
检测低表达的基因有一定优势  
De novo transcriptome assembler for very short reads  
网址 https://github.com/dzerbino/oases

## PASA（内包括BLAT和GMAP）

得到拼接好的fasta文件后可以用pasa进行基因结构预测  
Gene Structure Annotation and Analysis Using PASA  
网址 http://pasapipeline.github.io/  

## Maker

基因预测  
can be used for de novo annotation of newly sequenced genomes, for updating existing annotations to reflect new evidence, or just to combine annotations, evidence, and quality control statistics  
网址 http://www.yandell-lab.org/software/maker.html

## TransRate

reference free quality assessment of de novo transcriptome assemblies   
网址 http://hibberdlab.com/transrate/  
专业的拼接质量评估软件，有三种评估模式。

## DETONATE

DE novo TranscriptOme rNa-seq Assembly with or without the Truth Evaluation  
网址 https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0553-5

## BUSCO

它的评估模式和上面两个不太一样  
based on evolutionarily-informed expectations of gene content from near-universal single-copy orthologs

# Estimating transcript abundance

可以分为基于比对和不基于比对两种，其中RSEM和eXpress是基于比对的，另外两种是基于比对的。 

## RSEM

RNA-Seq by Expectation-Maximization  
网址 https://deweylab.github.io/RSEM/README.html

## eXpress

quantifying the abundances of a set of target sequences from sampled subsequences  
网址 https://pachterlab.github.io/eXpress/overview.html

## kallisto

快到飞起
丰度估计中样本特异性和读长偏好性低  
quantifying abundances of transcripts from RNA-Seq data  
网址 https://pachterlab.github.io/kallisto/

## salmon

quantifying the expression of transcripts using RNA-seq data  
网址 https://combine-lab.github.io/salmon/  
也是很快

# Read count

## htseq-count

网址 http://htseq.readthedocs.io/en/release_0.9.1/  
数read, 有它就够了

# Difference expression

和之前的步骤对应，这里也可以分为基于read和基于组装以及不基于比对三类工具。

## limma

Linear Models for Microarray Data  
网址 http://bioconductor.org/packages/release/bioc/html/limma.html  
用于分析芯片数据

## DEseq

网址 http://bioconductor.org/packages/release/bioc/html/DESeq.html

## DEseq2

效果在几个工具中相对好  
网址 http://bioconductor.org/packages/release/bioc/html/DESeq2.html

## DEGseq

Identify Differentially Expressed Genes from RNA-seq data  
网址 http://www.bioconductor.org/packages/2.6/bioc/html/DEGseq.html

## edgeR

Empirical Analysis of Digital Gene Expression Data in R  
网址 http://www.bioconductor.org/packages/release/bioc/html/edgeR.html

## Ballgown

准确度有时不是很好  
facilitate flexible differential expression analysis of RNA-Seq data  
organize, visualize, and analyze the expression measurements for your transcriptome assembly.  
网址 https://github.com/alyssafrazee/ballgown

## sleuth

用来配合kallisto使用  
网址 https://pachterlab.github.io/sleuth/about

# Data visualization

数据可视化的工具可以分为本地版本和在线版本

## IGV

Integrative Genomics Viewer  
网址 http://software.broadinstitute.org/software/igv/  
本地展示分析结果的不二选择

## jbrowse

公开展示数据或者给合作者分享时的不二选择，快且好看。  
网址 http://jbrowse.org/code/JBrowse-1.10.2/docs/tutorial/

## DEIVA

Interactive Visual Analysis of differential gene expression test results  
网址 http://hypercubed.github.io/DEIVA/  
差异表达的可视化在线工具

## Heatmapper

expression-based heat maps  
pairwise distance maps  
correlation maps  
网址 http://www.heatmapper.ca/  
用来话各种热图的在线工具

## START

visualize RNA-seq data starting with count data  
网址 https://kcvi.shinyapps.io/START/  
基于shinny的一套RNA-seq数据可视化工具

# 几个神奇的网站

## biostars

网址 https://www.biostars.org

## R book

网址 http://r4ds.had.co.nz/

## python guide

网址 http://docs.python-guide.org/en/latest/

## bioptyhon

网址 http://biopython.org/DIST/docs/tutorial/Tutorial.html

## Rosalind

网址 http://rosalind.info/problems/list-view/

## bioinformatics tools

网址 https://omictools.com/  
网址 https://bioinformatics.ca/links_directory/

## data visualistion catalogue

网址 http://datavizcatalogue.com/index.html

# References

生信技能树2017年8月27日公号`师妹 你要的都在这里了`






---
layout: post
title: Download reference genome and annotation
author: CY
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---



通常测序生成的reads要与参考基因组或参考转录组进行比对，所以首先需要获取参考基因组和参考转录组信息。



## 基因组各种版本对应关系

| NCBI   | UCSC | ENSEMBL                             |
| ------ | ---- | ----------------------------------- |
| GRCh36 | hg18 | ENSEMBL release_52.                 |
| GRCh37 | hg19 | ENSEMBL release_59/61/64/68/69/75.  |
| GRCh38 | hg38 | ENSEMBL  release_76/77/78/80/81/82. |

打开NCBI的，也可以看到里边很复杂，比如GRCh37.1, 37.2, 37.3 等等，不过这种版本一般指的是注释在更新，基因组序列一般不会更新。



## **下载参考基因组**

### UCSC下载

UCSC(http://genome.ucsc.edu/index.html) --> `Downloads` --> `Genome Data` --> `Human` --> `hg19 (Full data set)` --> ` chromFa.tar.gz  `

http://hgdownload.soe.ucsc.edu/goldenPath/hg19/bigZips/chromFa.tar.gz

**chromFa.tar.gz** - The assembly sequence in one file per chromosome. Repeats from RepeatMasker and Tandem Repeats Finder (with period of 12 or less) are shown in lower case; non-repeating sequence is shown in upper case.

```
mkdir reference && cd reference
mkdir -p genome/hg19 && cd genome/hg19
nohup wget http://hgdownload.soe.ucsc.edu/goldenPath/hg19/bigZips/chromFa.tar.gz &
tar -zvf chromFa.tar.gz
cat *.fa > hg19.fa
rm chr*
```



### Ensembl 下载

[Ensembl](http://www.ensembl.org/info/data/ftp/index.html) 是常用的信息齐全的参考基因组和GTF文件下载网站。打开链接即可看到几个常用动物物种的DNA序列和GTF格式的基因组注释。点击相应物种后边的 `DNA(FASTA)` 栏目下的 `FASTA` 即可进入基因组序列下载目录。                                

Ensembl 提供的参考基因组有2种组装形式 (`primary`，和 `toplevel`) 和3种重复序列处理方式 (`unmasked(dna)`、`soft-masked(dna_sm)` 和 `masked(dna_rm)`)。一般选择`dna.primary`或`dna_sm.primary`。                                     

- 为什么选择Primary                            

  Primary assembly contains all top level sequence regions excluding haplotypes and patches. This file is best used for performing sequence similarity searches where patch and haplotype sequences would confuse analysis.                              

- 为什么不选择masked                       
  Masked基因组是指所有重复区和低复杂区被N代替的基因组序列，比对时就不会有reads比对到这些区域。一般不推荐用masked的基因组，因为它造成了信息的丢失，由此带来的一个问题是uniquely比对到masked基因组上的reads实际上可能不是unique的。而且masked基因组还会带来比对错误，使得在允许错配的情况下，本来来自重复区的reads比对到基因组的其它位置。 另外检测重复区和低复杂区的软件不可能是完美的，这就造成遮盖住的重复序列和低复杂区并不一定是100%准确和敏感的                                      

- soft-masked基因组                                      

  是指把所有重复区和低复杂区的序列用小写字母标出的基因组，由于主要的比对软件，比如BWA、bowtie2等都忽略这些soft-mask，直接把小写字母当做大写字母比对，所以使用soft-masked基因组的比对效果和使用unmasked基因组的比对效果是相同的。                           



### NCBI下载

```
for i in $(seq 1 22) X Y M;
do wget ftp://ftp.ncbi.nlm.nih.gov/genomes/Homo_sapiens/ARCHIVE/BUILD.37.3/Assembled_chromosomes/seq/hs_ref_GRCh37.p5_chr${i}.fa.gz; 
gzip -d hs_ref_GRCh37.p5_chr${i}.fa.gz;
cat hs_ref_GRCh37.p5_chr${i}.fa.gz >>hg19.fa;
sleep 10s;
done;
```



## 下载基因组注释文件

基因注释`GTF`文件在分析转录组数据时会用到，下载GTF注释文件，基因组版本尤为重要。            

### Ensembl 下载

#### [**FTP下载**](http://www.ensembl.org/info/data/ftp/index.html)       

点击该链接中对应物种后边 `Gene Sets` 目录下的 `GTF` 文件。        

```
wget ftp://ftp.ensembl.org/pub/release-75/gtf/homo_sapiens/Homo_sapiens.GRCh38.94.gtf.gz
```

变幻中间的release就可以拿到所有版本信息：<ftp://ftp.ensembl.org/pub/>

Ensembl 中基因组和GTF文件中染色体的名字都没有添加`chr`，最好手动添加，以保持与`UCSC`或下游操作一致。                     

#### [**BioMart下载**](http://www.ensembl.org/biomart/martview)

ENSEMBL数据库的BioMart 工具为下载基因的功能信息、序列信息、结构信息、ID的转换等提供了很大的便利。       

**注意在BioMart的Attribute选项里如果选择了蛋白相关的选项，得到的结果中只有蛋白编码基因的信息。如果要下载所有基因信息，请不要选择蛋白相关的选项。**      

下载基因相关信息，可以选择 `Ensembl Genes 94` 数据集 --> `Human genes (GRCh38.p12)(下拉框中最先出现的关于人的)` 。

如果下载全部的基因信息，左侧 `Filters` 部分可以略过不填。如果只想下载比如说某个GO通路的基因或给定列表的基因信息，可以在`Filters`中指定对应的`GO ID`。                            

左侧 `Attribute` 中包含基因的名字、位置、注释、在不同数据库中的名字、GO注释、KEGG注释、功能域信息等，按需选择下载。选择好后，点击`Results`，获取结果。                          

`Export al results to`选择存储到文件中。如果特别大，而自己网速又比较慢，可以选择通过`邮件发送下载链接`。                                          

也可以通过Biomart提取基因结构 (点击`Structures`) 信息，比如5’ UTR、3’ UTR、外显子、内含子的坐标等。             

Biomart下载很方便，但是一个个点击非常麻烦。在页面选项上边有 `XML` 按钮，点击打开看到选择的下载信息都记录在了这个文件中。使用`wget -O result.txt 'http://www.ensembl.org/biomart/martservice?query=` `+` `XML中的内容` (调整为一行，并且行尾加一个单引号) 即可反复使用。如果想换一个物种，只需修改对应的`Dataset name`即可。



### NCBI下载 

```
# hg38
wget ftp://ftp.ncbi.nlm.nih.gov/genomes/Homo_sapiens/GFF/ref_GRCh38.p7_top_level.gff3.gz 
# hg19
wget ftp://ftp.ncbi.nlm.nih.gov/genomes/Homo_sapiens/ARCHIVE/BUILD.37.3/GFF/ref_GRCh37.p5_top_level.gff3.gz
```



### UCSC

方法一：用Table Browser下载

需要在[Table Browser](http://genome.ucsc.edu/cgi-bin/hgTables)里选择一系列参数：

> clade: Mammal
> genome: Human
> assembly: Feb. 2009 (GRCh37/hg19)
> group: Genes and Gene Predictions
> track: UCSC Genes
> table: knownGene
> region: Select "genome" for the entire genome.
> output format: GTF - gene transfer format
> output file: enter a file name to save your results to a file, or leave blank to display results in the browser
>
> Then click 'get output'.

但是这种方式下载的GTF文件是有限制的，只包含了转录本ID。转录本对应的基因名称是非常重要的信息，如果要解决这个问题，可以通过FTP服务器进行下载。



方法二：用FTP下载

UCSC的FTP服务提供了物种的注释文件供下载，但是FTP中并没有直接提供bed, gtf 格式的文件，因为这些格式存在冗余信息，文件大小会比较大。为例节省磁盘空间，UCSC提出来`genePred`这种格式。这种格式每一行代表一个转录本信息，冗余信息较少。

UCSC RefSeq这种信息对应的文件为`refGene.txt.gz`, 需要借助UCSC官网提供的[格式转换工具](http://hgdownload.soe.ucsc.edu/admin/exe/)`genePredToGtf` 将该文件转换为gtf格式。


```
wget ://hgdownload.soe.ucsc.edu/goldenPath/hg38/database/refGene.txt.gz
gunzip refGene.txt.gz
cut -f 2- refGene.txt | genePredToGtf file stdin -source=hg38_Ref  hg38.gtf
```

refGene.txt的第一列信息是多余的，删除之后，整个文件就是`genePred`格式了。生成的gtf文件中有gene_id的信息。但是相比NCBI和Ensembl，UCSC提供的GTF文件中共缺少了gene_biotype的信息，因此无法确定基因类型。




### GENCODE下载

GENCODE (http://www.gencodegenes.org/) --> `Human` --> `Current Release/Release history` --> 下载所需要的版本注释文件(GTF/GFF3) 



## 下载外显子坐标 (CCDS) 文件

[NCBI](https://www.ncbi.nlm.nih.gov/) --> `DNA & RNA` --> `Consensus CDS (CCDS)` --> `Announcements下的FTP site` --> `current human` --> `CCDS.current.txt`     

```
# 下载CCDS文件
wget ftp://ftp.ncbi.nlm.nih.gov/pub/CCDS/current_human/CCDS.current.txt
# 把CCDS转成bed
cat CCDS.current.txt| grep -v "Withdrawn"|perl -alne '{/\[(.*?)\]/;next unless $1;$gene=$F[2];$exons=$1;$exons=~s/\s//g;$exons=~s/-/\t/g;print "$F[0]\t$_\t$gene" foreach split/,/,$exons;}'|sort -u |bedtools sort -i |awk '{print "chr"$0"\t0\t+"}'  > hg38.exon.bed
```


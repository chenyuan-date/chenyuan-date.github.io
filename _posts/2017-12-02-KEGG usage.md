---
layout: post
title: KEGG usage
author: CY
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---



### Definations

[**GO**](http://www.geneontology.org/)  是Gene ontology的缩写，GO数据库分别从`分子功能`、`参与的生物途径`及`细胞中的定位`对基因产物进行了标准化描述，即对基因产物进行了简单注释。

通过GO富集分析可以粗略了解差异基因富集在哪些生物学功能、途径或者细胞定位。

**Pathway** 指代谢通路，对差异基因进行pathway分析，可以了解实验条件下显著改变的代谢通路，在机制研究中显得尤为重要。 

GO分析好比是将基因分门别类放入一个个功能类群，而pathway则是将基因一个个具体放到代谢网络中的指定位置。

[**KO**](http://www.genome.jp/kegg/ko.html) 是KEGG Orthology的缩写。它是蛋白质（酶）的一个分类体系，序列高度相似，并且在同一条通路上有相似功能的蛋白质被归为一组，然后打上KO（或K）标签。



### KEGG introduction

[KEGG](http://www.genome.jp/kegg/) (Kyoto encyclopedia of Genes and Genomes) 京都基因和基因组百科全书，是系统分析基因功能，联系基因信息和功能信息的知识库。它可以达到以下两个层面的信息：一，如果从功能出发，可以由功能到通路再到基因，迅速锁定某一功能的关键基因；二，从基因出发，可以获得某个基因在信号通路中的角色（上下游关系）和生物学功能，深入理解基因与功能的关系。从信号通路出发，找到关键基因，论证一系列基因和表型的关系，最后重新归结于信号通路是一个很主流的研究思路。



### Disease related pathways

例如我是研究乳腺癌的，我想看一下乳腺癌相关信号通路。

`首页` --> `Data-oriented entry points下面的KEGG PATHWAY` --> `选择organism前缀为hsa, 后边框内输入breast cancer`  --> `名为hsa05224的信号通路即为乳腺癌相关信号通路`

[Breast cancer - Homo sapiens (human)](http://www.kegg.jp/kegg-bin/highlight_pathway?scale=1.0&map=hsa05224&keyword=breast%20cancer)



### How to interpret KEGG results

以[糖酵解通路图](http://www.kegg.jp/kegg-bin/highlight_pathway?scale=1.0&map=hsa00010&keyword=Glycolysis)为例，方框一般就是酶，方框里面的5.1.3.3不是IP，而是EC编号；小圆圈代表代谢物，你点上去，会出现C00267的东西，C代表compound，00267是葡萄糖这种化合物在KEGG中的编号，一般在KEGG中数据条目都是这样的，前面一个标志，后面一个五位数编号；大的圆方块，就表示是另一个代谢图了，所以就不展开了。因为这是一张特定物种(human)的代谢图，绿色的框框表示专属于这个物种。

**在KEGG中有两种代谢图**

**①**一种是**参考代谢通路图reference pathway**，是根据已有的知识绘制的概括的、详尽的具有一般参考意义的代谢图，这种图上就不会有绿色的小框，而都是无色的，所有的框都可以点击查看更详细的信息；

**②**一种就是像上面这样的**属于特定物种的代谢图species-specific pathway**，会用绿色来标出这个物种特有的基因或酶，只有这些绿色的框点击以后才会给出更详细的信息。

这两种图很好区分，reference pathway 在KEGG中的名字是以map开头的，比如map00010，就是糖酵解途径的参考图；而特定物种的代谢通路图开头三个字符不是map而是种属英文单词的缩写（应该就是一个属的首字母+2个种的首字母）比如人类的糖酵解通路图，就是hsa00010， 酵母的糖酵解通路图，就是sce00010。

**如何寻找KEGG中的两种代谢图**

1. 有下拉列表的时候，在列表选择reference 或者是特定物种即可。
2. 在[pathway检索页面](http://www.genome.jp/kegg/pathway.html) ，默认的就是map，也就是参考图，你想要什么物中的代谢图写上它的名称就好了（种属缩写），如果不知道是哪3个字母，点击organism 选择即可。不过你点进去也是一片空白，需要你提示两个字母才会给出下拉条目。（其实就是上边写的乳腺癌相关信号通路的寻找过程）



### Search customed pathways

基因表达分析以后，会进行组间差异筛选以及差异基因的KEGG（pathway）富集分析，有时会对感兴趣基因进行富集分析和标记pathway图中关注基因。如何对KEGG数据库进行关注基因的DIY标记呢？

1. 整理关注基因的信息文本。整理方法如下：如果是芯片数据，又需要将上调基因和下调基因用不同颜色区分，在excel表格中整理两列，第一列是Entrez geneID，第二列附上表示不同颜色的英文单词，例如上调基因用red标记，下调基因用green标记（这个是中国传统的惯性，但是我的德国老板说，红色代表赤字，所以在他们的规则里，红色要代表下调的基因，绿色代表上调基因，在quora上一查还真是这样）。如果不是芯片数据，也可以根据自己的需求将不同ID号后面附上不同颜色单词，用以在通路图中不同基因标记不同颜色。然后另存为“文本文件（制表符分隔）”格式文件(.txt)。



| EntrezGeneID | color |
| ------------ | ----- |
| 3101         | red   |
| 3098         | red   |
| 3099         | red   |
| 80201        | green |
| 2645         | green |
| 83440        | green |



2. 找到输入以上信息的页面流程如下：`[KEGG数据库首页](http://www.genome.jp/kegg/)`  --> `点击页面尾部Analysis tools中KEGG Mapper` -->  `点击侧边工具栏的Search&Color Pathway`  

3. 在“Search against”选项中选择您需要标记基因的物种，点击“org”，输入物种的英文名字，会出现相应物种对应的3个字母缩写名称，选择即可。例如“Humansapiens（human）”，对应3个字母名称为hsa，在“Primary ID”选项中选择“NCBIGeneID”，之后点击“选择文件”这项，输入整理好的.txt文件 (或者直接输入到文本框中也是一样的)，完成后，点击“Exec”选项提交即可，之后会出现关注基因都被富集到哪个通路的信息。

4. 红色标注下面所列基因名字是没有在数据库中搜索到相应信息的基因，说明对于这些基因在数据库中没有收入。将此页面下拉，会看到感兴趣基因富集到的通路。点击感兴趣的pathway，例如“pathway in cancer”即可出现想要的结果。其中，红色为上调基因，绿色为下调基因，绿色为该物种所有基因。鼠标滑到有颜色标记的方框后会出现该基因的信息。

   ​

   ​

### References

[如何在KEGG数据库中DIY标记感兴趣基因](http://www.oebiotech.com/Article/rhzkeggsjkz.html)
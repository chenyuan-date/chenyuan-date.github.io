---
layout: post
title: Metabolomics Database and Tools  
author: CY
tags: [Bioinformatics]
categories: [Bioinformatics]
share: false
image:
  background: triangular.png 
---



## Database   

[Human Metabolome Database (HMDB)](http://www.hmdb.ca/)          

[Reactome](http://www.reactome.org)                                         

[PubChem]()         

[KEGG]()                         

[Human metabolic atlas: A dedicate online resource for Human Metabolism](http://www.metabolicatlas.org/)            

[Metabolomics -- The human protein atlas](https://www.proteinatlas.org/news/tag/metabolomics)                

[核姆霍兹慕尼黑研究中心Metabolomics](https://www.helmholtz-muenchen.de/ibis/institute/groups/metabolomics/about-us/index.html)              

​                       

## Analyzing tools 

- **Mass Profiler Professional (MPP)  **                 
  - 安捷伦公司代谢组学数据预处理，数据分析软件，功能强大，常规的数据分析都可以实现。用于MPP软件分析的数据格式为.cef格式，该格式的文件需要使用MassHunter软件生成。使用MassHunter软件对安捷伦公司质谱所采集的原始数据进行色谱峰提取，解卷积，积分，缺失值过滤等操作，之后将生成的列表直接导出为.cef文件进行后续分析。                  
  - 常见的统计分析，该软件都可以完成，包括主成分分析，偏最小二乘判别分析，聚类分析，方差分析，代谢通路分析等。                             
- **MarkerLynx  **                                 
  - 沃特世公司生产，作为MassLynx软件等一个模块，可以对沃特世公司仪器采集的数据进行数据预处理（色谱峰提取，排列，解卷积）生成供接下来统计分析的数据集。生成的数据集可以导入EZinfor软件进行统计分析，该软件其实就是将Simca-p内嵌到了MassLynx 里。                   
- **Progenesis QI  **                              
  - 适用性较广的一个数据预处理软件，它可以处理市面上几乎所有常用高分辨质谱仪产生的数据，包括沃特世，安捷伦，热电等等，其中与沃特世仪器得到的原始数据兼容性最好，无需经过数据转换和加载插件。该软件可以识别由沃特世仪器在MSe状态下得到的数据。                    
  - 该软件也可以进行简单的统计分析，如方差分析，聚类分析，主成分分析等。但是如果实验室中使用了沃特世高分辨质谱仪，并且购买了EZinfo软件的话，由Progenesis QI产生的数据集可以直接导入进行分析。如果使用的是其他厂家的仪器，那么得到的数据集可以导入其他第三方软件进行后续的统计分析。此外，该软件可以联网进行代谢通路分析。                  
- **Sieve**                        
  - 热电公司生产的一款数据预处理软件，可以识别热电旗下所有高分辨质谱仪产生的数据。数据预处理之后，也可进行简单的统计分析，如主成分分析，方差分析，绘制火山图等。                     
  - 也可将该软件的产生的数据集导入其他统计软件进行更为深入的统计分析。              
- **SIMCA**                         
  - 代谢组学中最常用的统计分析软件。但是是商业软件，收费的，网上可以下到试用版。              
- [MetaboAnalyst](http://chenyuan.date/2018/01/MetaboAnalyst/)                
  - 一款免费使用的网络软件，功能强大，可以进行数据预处理和数据统计分析。该软件需要使用者自己准备符合要求的数据集，不能对仪器产生的原始数据进行识别，因此需要与仪器配套的软件对原始数据进行处理的到可供分析的数据集。                          
  - 该软件可对数据集进行缺失值过滤，归一化，数据转换等操作；同时该软件还包含几乎所有的常用的统计分析方法以及代谢通路分析。                   





## Companies    

[Metabolon](https://www.metabolon.com/)                 

[Biocrates](https://www.biocrates.com/)            
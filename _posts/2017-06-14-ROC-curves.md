---
layout: post
title: ROC curve calculation
author: CY
tags: [Biostatistics]
categories: [Biostatistics]
share: false
image:
  background: triangular.png
---




## ROC curves in usage     

一般在下面的三种情况用到ROC曲线：       
* 对一个连续性的指标进行cutoff分析的时候，如果结局变量是二分类的话，可以通过ROC曲线来计算最佳的cut-off值。        
* 构建模型的时候，可以通过ROC曲线来评价构建的模型的诊断效能。                                        
* 评价多个模型的同样的也是可以通过ROC曲线来比较。      

ROC曲线有一些特定的值，如：灵敏度；特异度；阈值；曲线下面积以及约登指数，需要在做ROC的时候给出。




## R for ROC curves  
Packages like `pROC`, `RROC`, `cutpointr` 都可以对一个变量进行ROC计算以及相关数据的统计。           
pROC包当中提供了一个函数叫roc，我们可以通过这个函数来计算两组之间的ROC结果：   
* `ci.auc` 函数计算ROC曲线的AUC以及95% CI。     
* `coords` 函数计算ROC曲线的相关信息。这个函数可以接受的参数包括：“threshold”, “specificity”, “sensitivity”, “accuracy”, “tn” (true negative count), “tp” (true positive count), “fn” (false negative count), “fp” (false positive count), “npv” (negative predictive value), “ppv” (positive predictive value), “precision”, “recall”. “1-specificity”, “1-sensitivity”, “1-accuracy”, “1-npv” and “1-ppv”`。可以选择不同的参数来返回不同的结果。
* 这个包没有约登指数的计算，不过约登指数就是灵敏度+特异度-1，可以自己计算。




## Function to calculate 

```r
# Load packages 
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(pROC))

ROCStatFunc <- function(dat, group, var, retype = c("threshold", "specificity", "sensitivity"),
                        auc = T, youden = T, digit = 3){
     subgroup <- levels(as.factor(dat[[group]]))
     subgroup1 <- paste0(subgroup[2], " vs ", subgroup[1])
     rocmodel <- roc(dat[[group]], dat[[var]])
     other <- coords(rocmodel, "b", ret = retype)
     other <- round(other, digit)
     if(auc == T){
         auc <- round(ci.auc(rocmodel),digit)
         auc <- paste0(auc[2],"(",auc[1],"-",auc[3],")")
         if(youden == T){
             abc <- coords(rocmodel, "b", ret = c("specificity", "sensitivity"))
             youdenres <- abc[1] + abc[2] - 1
             youdenres <- round(youdenres, digit)
             result <- c(group, subgroup1, auc, other, youdenres)
             names(result) <- c("group", "subgroup","auc(95%CI)", retype, "youden")
         }else{
             result <- c(group, subgroup1, auc, other)
             names(result) <- c("group", "subgroup", "auc(95%CI)", retype)
         }
     }else{
         if(youden == T){
             abc <- coords(rocmodel, "b", ret = c("specificity", "sensitivity"))
             youdenres <- abc[1] + abc[2] - 1
             youdenres <- round(youdenres, digit)
             result <- c(group, subgroup1, other, youdenres)
             names(result) <- c("group","subgroup", retype, "youden")
         }else{
             result <- c(group, subgroup1,other)
             names(result) <- c("group", "subgroup",retype)
         }
     }
     return(result)
}

#会返回很多信息，可以去掉这些结果
quiteROCFunc <- quietly(ROCStatFunc)
```

此函数一共包括7个参数。分别是：
dat: 我们需要输入我们的数据集。   
group: 想要进行ROC的结局变量。     
var： 需要分析的变量。       
retype: 想要计算的具体信息: 默认的返回的包括：阈值，灵敏度， 特异度。    
auc： 是否返回曲线下面积以及95%CI，逻辑值，默认为TRUE。      
youden: 是否返回约登指数，逻辑值，默认为TURE。        
digit: 结果保留几位小数点。  



## Calculate with example

```r
head(aSAH)
```

```
##    gos6 outcome gender age wfns s100b  ndka
## 29    5    Good Female  42    1  0.13  3.01
## 30    5    Good Female  37    1  0.14  8.54
## 31    5    Good Female  42    1  0.10  8.09
## 32    5    Good Female  27    1  0.04 10.42
## 33    1    Poor Female  42    3  0.13 17.40
## 34    1    Poor   Male  48    2  0.10 12.75
```

```r
quiteROCFunc(aSAH, group = "s100b", var = "age")$result
```

```
##          group       subgroup     auc(95%CI)      threshold    specificity 
##        "s100b" "0.04 vs 0.03"    "NA(NA-NA)"           "39"            "1" 
##    sensitivity         youden 
##          "0.6"          "0.6"
```

```r
multigroup <- c("age", "s100b", "ndka")
rocRes <- lapply(multigroup, function(x) quiteROCFunc(aSAH, "outcome", x)$result)
rocResDat <- do.call(rbind, rocRes)
rocResDat
```

```
##      group     subgroup       auc(95%CI)           threshold specificity
## [1,] "outcome" "Poor vs Good" "0.615(0.508-0.722)" "50.5"    "0.569"    
## [2,] "outcome" "Poor vs Good" "0.731(0.63-0.833)"  "0.205"   "0.806"    
## [3,] "outcome" "Poor vs Good" "0.612(0.501-0.723)" "11.08"   "0.514"    
##      sensitivity youden 
## [1,] "0.634"     "0.204"
## [2,] "0.634"     "0.44" 
## [3,] "0.707"     "0.221"
```

Note:   
* 这个函数依赖tidyververse和pROC包   
* 函数对于分组的话必须是两组     
* 结果当中的subgroup是case vs control


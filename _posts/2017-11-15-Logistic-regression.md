---
layout: post
title: Logistic regression 
author: CY
tags: [Machine Learning]
categories: [Machine Learning]
share: false
image:
  background: triangular.png
---



### Outliers, Leverage & Influential points 

**异常值点**: 异常值是指数据中有异常表现的数据点。在一个回归模型中，异常值点包括离群点，高杠杆值点和强影响点，这些点都可能对结果产生较大的负面影响，因此对异常值点的判断及修正对建立正确的回归模型非常重要。

**Outliers(离群点)**: 离群点通常指残差非常大的点，即模型预测的y值与真实的y值相差非常大。通常检测离群点的方法有：
方法1：用箱线图判断，如果图中的点出现在四个分位数外的一般都是离群点。
方法2：用QQ图检测，落在置信区间外的点通常被认为是离群点。
方法3：通常认为标准化残差的绝对值大于2的点可能是离群点，也有资料说是大于3，可视情况而定
方法4：用car包的outlierTest()函数求得最大标准化残差绝对值Bonferroni调整后的p值，从而作出判断。
对离群点，我们一般会选择删除，删除离群点还有利于提高数据集对于正态分布假设的拟合度。

**Leverage(高杠杆值点)**: 高杠杆值点指的是x值比较异常，通常与响应变量值y没有关系。
判断高杠杆值点的方法：
方法1： 杠杆点在简单线性回归中较容易辨别，一般找出预测值超出正常范围的观测点即杠杆点。
方法2： 计算点的帽子统计量，若该点的帽子统计量大于帽子统计量的均值的2或3倍，通常被认为是高杠杆值点。

**Influential(强影响点)**:  即对模型参数估计值影响有些比例失衡的点。例如，若移除模型的一个观测点时，模型会发生巨大的改变。一般来说，高杠杆值点，若是离群点，则是强影响点。当然强影响点也不局限于此，强影响点是指对统计推断有影响的点，一般用cook距离进行判断，若cook距离的值大于4/(n-k-1),则表明是强影响点

`influenceplot()`函数(car包中有)，可以把离群点，高杠杆值点，影响点都整合在一个图上，影响图横坐标为帽子值，纵坐标为学生化残差，因此纵坐标超过+2或者-2的点被认为是离群点，横坐标可以判断哪些点是高杠杆值点，图中越往右上角的点，越有可能是强影响点。



### Pre-request for logistic regression model

使用logistic regression model前，需判断是否满足以下7个研究假设：   
假设1：因变量即结局是二分类变量。      
假设2：有至少1个自变量，自变量可以是连续变量，也可以是分类变量。   
假设3：每条观测间相互独立。分类变量（包括自变量和因变量）的分类必须全面且每一个分类间互斥。   
假设4：最小样本量要求为自变量数目的15倍，但一些研究者认为样本量应达到自变量数目的50倍。   
假设5：连续的自变量与因变量的Logit转换值之间存在线性关系。   
假设6：自变量间不存在共线性。   
假设7：没有明显的离群点、杠杆点和强影响点。   











### References 

[Distinction Between Outliers & High Leverage Observations](https://onlinecourses.science.psu.edu/stat501/node/337)

[Outliers: discrepancy, leverage, and influence of the observations](https://learnche.org/pid/least-squares-modelling/outliers-discrepancy-leverage-and-influence-of-the-observations)
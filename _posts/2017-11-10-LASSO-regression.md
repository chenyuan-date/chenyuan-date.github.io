---
​---
layout: post
title: LASSO regression
author: CY
tags: [Biostatistics]
categories: [Biostatistics]
share: false
image:
  background: triangular.png 
​---
---



### LASSO Introduction
Tibshirani(1996)提出了Lasso(The Least Absolute Shrinkage and Selectionator operator)算法。这种算法通过构造一个惩罚函数获得一个精炼的模型；通过最终确定一些指标的系数为零，LASSO算法实现了指标集合精简的目的。这是一种处理具有复共线性数据的有偏估计。Lasso的基本思想是在回归系数的绝对值之和小于一个常数的约束条件下，使残差平方和最小化，从而能够产生某些严格等于0的回归系数，得到解释力较强的模型。

LASSO回归的特点是在拟合`广义线性模型`的同时进行变量筛选(Variable Selection)和复杂度调整(Regularization)。 因此，不论目标因变量(dependent/response varaible)是连续的(continuous)，还是二元或者多元离散的(discrete)， 都可以用LASSO回归建模然后预测。 这里的`变量筛选`是指不把所有的变量都放入模型中进行拟合，而是有选择的把变量放入模型从而得到更好的性能参数。 `复杂度调整`是指通过一系列参数控制模型的复杂度，从而避免Overfitting。 **对于线性模型来说，复杂度与模型的变量数有直接关系，变量数越多，模型复杂度就越高。 更多的变量在拟合时往往可以给出一个看似更好的模型，但是同时也面临过度拟合的危险。** 此时如果用全新的数据去验证模型(Validation)，通常效果很差。 *一般来说，变量数大于数据点数量很多，或者某一个离散变量有太多独特值时，都有可能过度拟合。*

LASSO回归复杂度调整的程度由参数`λ`来控制，λ越大对变量较多的线性模型的惩罚力度就越大，从而最终获得一个变量较少的模型。 LASSO回归与Ridge回归同属于一个被称为Elastic Net的广义线性模型家族。 这一家族的模型除了相同作用的参数λ之外，还有另一个参数α来控制应对高相关性(highly correlated)数据时模型的性状。 LASSO回归α=1，Ridge回归α=0，一般Elastic Net模型0<α<1。 这篇文章主要介绍LASSO回归，所以我们集中关注α=1的情况，对于另外两种模型的特点和如何选取最优α值，我会在第四节做一些简单阐述。

目前最好用的拟合广义线性模型的R package是glmnet，由LASSO回归的发明人，斯坦福统计学家Trevor Hastie领衔开发。 它的特点是对一系列不同λ值进行拟合，每次拟合都用到上一个λ值拟合的结果，从而大大提高了运算效率。 此外它还包括了并行计算的功能，这样就能调动一台计算机的多个核或者多个计算机的运算网络，进一步缩短运算时间。

下面我们就通过一个线性回归和一个Logistic回归的例子，了解如何使用glmnet拟合LASSO回归。 另外，之后的系列文章我打算重点介绍非参数模型(nonparametric model)中的一种，Gradient Boosting Machine。 然后通过一个保险行业的实例，分享一些实际建模过程中的经验，包括如何选取和预处理数据，如何直观得分析自变量与因变量之间的关系，如何避免过度拟合，以及如何衡量和选取最终模型等。




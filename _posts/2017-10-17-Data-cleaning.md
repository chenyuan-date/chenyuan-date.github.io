---
layout: post
title: Data cleaning 
author: CY
tags: [Study]
categories: [Study]
share: false
image:
  background: triangular.png
---



数据清洗可以从两个角度看：一是为了解决数据质量问题，二是让数据更适合做挖掘。不同的目的下分不同的情况，也都有相应的解决方式和方法。

### 解决数据质量问题

解决数据的各种问题，包括但不限于：

+ 数据的完整性----例如人的属性中缺少性别、籍贯、年龄等    

+ 数据的唯一性----例如不同来源的数据出现重复的情况      

+ 数据的权威性----例如同一个指标出现多个来源的数据，且数值不一样      

+ 数据的合法性----例如获取的数据与常识不符，年龄大于150岁      

+ 数据的一致性----例如不同来源的不同指标，实际内涵是一样的，或是同一指标内涵不一致 


数据清洗的结果是对各种脏数据进行对应方式的处理，得到标准的、干净的、连续的数据，提供给数据统计、数据挖掘等使用。 为了解决以上各种问题，需要不同的手段和方法来一一处理。 每种问题都有各种情况，每种情况适用不同的处理方法。

#### 解决数据的完整性问题

解题思路：数据缺失，补全数据。具体方法有：

	1. 通过其他信息补全，例如使用身份证件号码推算性别、籍贯、出生日期、年龄等
	2. 通过前后数据补全，例如时间序列缺数据了，可以使用前后的均值，缺的多了，可以使用平滑等处理。
	3. 实在补不全的，虽然很可惜，但也必须要剔除。但是不要删掉，没准以后可以用得上

#### 解决数据的唯一性问题

解题思路：去除重复记录，只保留一条。具体方法有：

	1. 按主键去重，用sql或者excel“去除重复记录”即可
	2. 按规则去重，编写一系列的规则，对重复情况复杂的数据进行去重。例如不同渠道来的客户数据，可以通过相同的关键信息进行匹配，合并去重。

#### 解决数据的权威性问题

解题思路：用最权威的那个渠道的数据。具体方法:

	对不同渠道设定权威级别，例如：在医院，首先得完全信任医生

#### 解决数据的合法性问题

解题思路：设定判定规则。具体方法:

	1. 设定强制合法规则，凡是不在此规则范围内的，强制设为最大值，或者判为无效，剔除
		字段类型合法规则：日期字段格式为“2010-10-10”
		字段内容合法规则：性别 in （男、女、未知）；出生日期<=今天
	2. 设定警告规则，凡是不在此规则范围内的，进行警告，然后人工处理
		警告规则：年龄》110
	3. 离群值人工特殊处理，使用分箱、聚类、回归等方式发现离群值

#### 解决数据的一致性问题

解题思路：建立数据体系，包含但不限于：

	1. 指标体系（度量）
	2. 维度（分组、统计口径）
	3. 单位
	4. 频度
	5. 数据

### 让数据更适合做挖掘或展示

目标包括但不限于：

+ 高维度----不适合挖掘

+ 维度太低----不适合挖掘

+ 无关信息----减少存储

+ 字段冗余----一个字段是其他字段计算出来的，会造成相关系数为1或者主成因分析异常）

+ 多指标数值、单位不同----如GDP与城镇居民人均收入数值相差过大

#### 解决高维度问题

解题思路：降维，方法包括但不限于：

	1. 主成分分析
	2. 随机森林

#### 解决维度低或缺少维度问题

解题思路：抽象，方法包括但不限于：
​	
	1. 各种汇总，平均、加总、最大、最小等
	2. 各种离散化，聚类、自定义分组等

#### 解决无关信息和字段冗余

解决方法：剔除字段

#### 解决多指标数值、单位不同问题

解决方法：归一化，方法包括但不限于：

	1. 最小-最大
	2. 零-均值
	3. 小数定标

### References 

[数据挖掘中常用的数据清洗方法有哪些？](https://www.zhihu.com/question/22077960)   

[机器学习基础与实践（一）--数据清洗](http://www.cnblogs.com/charlotte77/p/5606926.html)

[数据清洗的一些梳理](http://www.raincent.com/content-85-6046-1.html%E2%80%8B)
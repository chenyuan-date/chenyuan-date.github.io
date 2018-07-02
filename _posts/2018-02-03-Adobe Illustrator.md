---
layout: post
title: Adobe Illustrator
author: CY
tags: [Study]
categories: [Study]
share: false
image:
  background: triangular.png
---



`Adobe Illustrator`简称`AI`。

著名的`Adobe`公司出品，应该都不陌生，照片拍出来是不是好看，有他家`Photoshop`不少的功劳。试用后（买不起，也只能用试用版；如果有钱，还是推荐购买正版，维护原作者的权益），发现果然很强大。

矢量图的任何一个地方都可以挑出来修改，某个边框不好看，删掉；线条的粗细不统一，设置成一样的；某条线的颜色想重点突出下，单独修改 (这部分最好还是在画图时就修改好，会更协调，当然AI也没问题)；图中有了多余的元素，删掉；添加文字、设置成统一字体、统一大小更没问题；画个简单的模式图，没问题；不同的子图拼在一起，没问题；自此，再也不愁文章的拼图了。犯愁的是，没有好结果，无图可拼。

看看自己没戏了，还是把自己会的这点操作贡献出来，希望能给科研大牛们的工作尽一点绵薄之力。

第一个视频以[绘制的线图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247483947&idx=1&sn=7cf0252efff5433447507b977fcaff97&scene=21#wechat_redirect)为例，展示如果修改、调整矢量图的每个部分。`ggplot2`出品的矢量图整体逻辑比较清晰，一层层的叠加，修改起来也比较方便，没有太多难点；关键是熟悉用到的按钮的使用方式和快捷键的操作。



### 矢量图和标量图

**矢量图**是使用直线和曲线来描述图形, 这些图形的元素是一些点、线、矩形、多边形、圆和弧线等等, 它们都是通过数学公式计算获得的。矢量图形最大的优点是无论放大、缩小或旋转等不会失真；最大的缺点是难以表现色彩层次丰富的逼真图像效果。常见的矢量图有`PDF`, `SVG`, `EPS`等格式。如果图形中有文字, 并且文字可以复制, 则可初步判断为矢量图。

与矢量图相对应的就是**标量图**了, 常见的`png`, `jpg`, `gif`格式等, 是由像素点构成, 放大到一定程度会出现马赛克效果。图中的文字不可复制, 元素不可拆分。

### 矢量图的制作

- 常规图：

- - `Excel`, 生成的图可以直接拷贝到`AI`里面修改
  - `R`, `Perl`, `Python`等程序语言输出`pdf`, `eps`格式的图 (详见公众号中[R作图系列](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484250&idx=2&sn=1bad22e1e0018d9108ddafca561180b0&scene=21#wechat_redirect))

- 常用工具的出图

- - 二代测序出图  `UCSC` – `PDF`; `IGV` – `SVG`; `epigenomegateway` - `SVG`; 在高通量数据可视化文章中也有介绍
  - Motif   `Weblogo` - `eps`
  - 作图软件 Graphpad

### 矢量图编辑工具

主要有 `Gimp`, `Adobe illustrator`, `Inkscape`, `image magik`, `photoshop`, `latex`。适用之后, 从稳定性还是易用性来讲, `Adobe illustrator`是最好的一款。但是是收费软件, 在线会有一些试用版, 供测试时用。

### 作图基本原则

- 图形中文字的字体保持统一, 一般使用`Helevetica`或`Arial`
- 符号一般使用`Symbol`字体, 常见符号有 `′`, `β`等
- Panel的字号(A,B,C,D)一般比其余的文字大一号, 上下左右对齐
- 文字特别密集的地方字体可适当缩小, 原则是看着协调
- 图和图之间的距离在空间允许的情况下尽可能的大

















### `Adobe Illustrator`中的基本概念和操作描述

1. **编组**：性质相似或者需要同时修改的部分可以编为一组，方便处理。双击一组内容，就可以进入编组内部，对编组的每个元素修改；并且编组外的元素处屏蔽状态，操作起来不会受到干扰。
2. **剪切蒙版**：如果想剪切掉图中的某一部分，可以绘制一个矩形、圆形或任意不规则形状覆盖住**需要保留**的部分，然后同时选中这两个元素（绘制的形状框在被剪切的图之上），按右键，选择剪切蒙版，就可以完成剪切操作。而在修改图时，也可以不断的释放剪切蒙版，方便对不同图层的操作。
3. **直接选择工具**：可以无视编组和剪切蒙版，对选中并且只是选中的部分进行操作。这在删除多余的内容和边框时会经常用到。
4. **魔棒工具**： 选择类似属性的组分，统一操作。
5. **吸管工具**：给一个组分赋予另一个组分的属性。
6. **对齐工具**：用于组分的对齐和分布，在设置坐标轴的标记文字时很有用，省去了一个个手动对齐的操作。只要对齐两端，按一下按钮中间的内容就自动与刻度线对齐了。
7. 其它的就靠大家不断的尝试、体验、操作了。多选、多点、多查，慢慢就都熟练了。



https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484434&idx=1&sn=88b56a24270bd8ee34714f58bc0baa2c&chksm=ec0dc198db7a488e8818b5560a5547a4e574e2d16967953398acd3f38d90723bcbd713e0cbcc&mpshare=1&scene=1&srcid=0702Sozg83bekxYK0V8VI40j&pass_ticket=%2Fx%2F7g9x7T9Me2JipDkOD8agR6JgL25BaQUe3vymWvP%2B7%2BHhJGgE9tcfBD5qomh0Y#rd



https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484492&idx=1&sn=10c9b2308065b6260cfc69ea9e8d065f&chksm=ec0dc1c6db7a48d060007e9b325e09705d0d6321201099a7909878f3d213d01adddc96124c27&mpshare=1&scene=1&srcid=0702CFdW1aEDzlQGW0NcKBCD&pass_ticket=%2Fx%2F7g9x7T9Me2JipDkOD8agR6JgL25BaQUe3vymWvP%2B7%2BHhJGgE9tcfBD5qomh0Y#rd






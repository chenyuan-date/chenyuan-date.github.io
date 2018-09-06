---
layout: post
title: Python formatted output 
author: CY
tags: [Python]
categories: [Python]
share: false
image:
  background: triangular.png
---





经常会看到printf, sprintf等的格式化输出形式，但是别弄混了，它们是在 `bash`, `perl`, `c`等语言中起作用的函数，在Python中只有print函数。

传统的Python的格式化输出是通过 `%` 控制的。 所以会看到形如 `%d`, `%s`, `%f`等形式。



**使用 `format` 函数进行格式化输出**   

新版本的Python使用format函数进行格式化输出，通过 `{}` 和 ` : ` 来代替以前的 ` % `，增强了字符串格式化的功能。或许传统方法会在以后的版本中淘汰了，所以直接学习 format 函数就成。 

请注意，Python 从 0 开始计数，这意味着索引中的第一位是 0，第二位是 1，以此类推。



### 映射

#### 通过位置

字符串的format函数可以接受不限个参数，位置可以*不按顺序*，可以不用或者用*多次*。

```
"{} {}".format("hello", "world")    # 不设置指定位置，按默认顺序
'hello world'
 
"{0} {1}".format("hello", "world")  # 设置指定位置
'hello world'
 
"{1} {0} {1}".format("hello", "world")  # 设置指定位置
'world hello world'
```



#### 通过关键字参数

```
print("网站名：{name}, 地址 {url}".format(name="textbook", url="www.com"))
 
# 通过字典设置参数
site = {"name": "textbooktextbook", "url": "www.com"}
print("网站名：{name}, 地址 {url}".format(**site))
 
# 通过列表索引设置参数
my_list = ['textbook', 'www.com']
print("网站名：{0[0]}, 地址 {0[1]}".format(my_list))  # "0" 是必须的
```



#### 通过对象属性

```
class Person:  
    def __init__(self,name,age):  
        self.name, self.age = name,age  
        def __str__(self):  
            return 'This guy is {self.name},is {self.age} old'.format(self=self) 
            
str(Person('kzc',18))  
```



### 格式限定符

#### 填充与对齐

填充常跟对齐一起使用
`^`、`<`、`>` 分别是居中、左对齐、右对齐，后面带宽度
`:` 号后面带填充的字符，只能是一个字符，不指定的话默认是用空格填充

`d` ：默认是十进制，所以d经常省略

`s` : 输出字符串

```
'{:>8}'.format('189')  => '     189'
'{:0>8}'.format('189') => '00000189'
'{:a>8}'.format('189') => 'aaaaa189'
"{1:>10s}".format(8,"toto")  ==> '        toto'
print('{0:_^11}'.format('hello'))  ==> ___hello___
```



#### 精度与类型f
精度常跟类型f一起使用

`.数字` 表示输出小数点后几位小数

`f` 表示浮点数

```
'{:.2f}'.format(321.33345) => '321.33'
```



#### 正负号及空格

`+` 表示在正数前显示 `+`，负数前显示 `-`；  （空格）表示在正数前加空格

```
print("{0:+.2f},{0:-.2f},{0: .2f}".format(3.146567)) => +3.15,3.15, 3.15
print("{0:+.2f},{0:-.2f},{0: .2f}".format(-3.146567)) => -3.15,-3.15,-3.15
```



#### 指数、百分数

使用指数记法，将 `f` 改成 `e` 或者`E` (取决于指数输出的大小写形式)      

使用百分比格式，将 `f` 改成 `%`         

```
"{0:.2e},{0:.2E},{0:.2%}".format(3.14)
输出：'3.14e+00,3.14E+00,314.00%'
```



#### 其他类型

进制: b、d、o、x分别是二进制、十进制、八进制、十六进制。

```
'{:b}'.format(17)  => '10001'          
'{:d}'.format(17)  => '17' (默认)  
'{:o}'.format(17)  => '21'    
'{:x}'.format(17)  => '11'
```



用 `,` 号做金额的千位分隔符。

```
'{:,}'.format(1234567890)  => '1,234,567,890'
```



使用大括号 `{}` 来转义大括号   

```
print ("{} is {{0}}".format("runoob"))  => runoob is {0}
```


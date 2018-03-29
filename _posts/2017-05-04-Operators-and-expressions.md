---
layout: post
title: Python Operators and Expressions
author: CY
tags: [Python]
categories: [Python]
share: false
image:
  background: triangular.png
---



`表达式（Expressions` =  `运算符（Operators` + `操作数（Operands`



## Python 数据类型

- 数值

  - integer = 10
  - float = 10.01
- 字符串: string = “123abc”
- 逻辑: boolean = True / False
- 列表: list = [ value1, value2, … ]
- 字典: dictionary = { key1:value1, key2:value2, …}

### Cheatsheet

- `print(x, sep='y')`:  返回被 y 隔开的 x 
- `input()`: 交互式的输入输出。input函数从屏幕中录入的内容，属于字符串类型       
- `len(x)`:  返回 x 的长度 (x 可以为字符串、列表、字典)
- `type(x)`: 返回 x 的类型 (整数、浮点数、字符串、列表、字典…)




### 数值

数字主要分为两种类型:  整数（Integers）与浮点数（Floats）。

#### Cheatsheet

- `E/e` 表示 10 的幂。`5E-4` 表示 `5 * 10^-4`。

- `+`:  两个数字对象相加。

- `-`: 从一个数中减去另一个数，如果第一个操作数不存在，则假定为零。

- `*`: 给出两个数的乘积，或返回字符串重复指定次数后的结果。

- `**`: 返回 x 的 y 次方。

- `/`: x 除以 y 的商。

- `//`: x 除以 y 并对结果**向下**取整至最接近的整数。

  - `13 // 3` 输出 `4`; `-13 // 3` 输出 `-5`。

- `%` : 返回除法运算后的余数。

- `int()`: 将变量转换为整数

- `float()`: 将变量转换为浮点数

- `range(start,end,step)`: 返回一系列从 start (包括) 到 end (不包括) 的数值，以 step 间隔。start默认为0。  

- `abs(n)`:  返回 n 的绝对值

- `round(n1,n)`: 返回保留 n 位小数的 n1

  ​

### 字符串

一串字符串String是字符Characters的序列Sequence。基本上，字符串就是一串词汇。

#### 引号

- 单引号: 来指定字符串。所有引号内的空间，诸如空格与制表符，都将按原样保留。   
- 双引号: 被双引号包括的字符串和被单引号括起的字符串其工作机制完全相同。
- 三引号: 用三个引号`"""` 或 `'''` 来指定多行字符串。你可以在三引号之间自由地使用单引号与双引号。

#### 字符串是不可变的

这意味着一旦你创造了一串字符串，你就不能再改变它。尽管这看起来像是一件坏事，但实际上并非如此。我们将会在稍后展现的多个程序中看到为何这一点不是一个限制。

#### 格式化方法

一个字符串可以使用某些特定的格式。想要从其他信息中构建字符串，`format` 方法将被调用，使用这一方法中与之相应的参数替换这些格式。请注意，Python 从 0 开始计数，这意味着索引中的第一位是 0，第二位是 1，以此类推。             

> Formating:  {selection : formating ! conversion}
>
> `fillchar`  `alignment`  `sign`  `minwidth` . `precision ~ maxwidth`  `type`
>
> *alignment*: < > ^ =
>
> *sign*: + - space
>
> *precision ~ maxwidth*: 0 at start for filling with 0
>
> *type*: 
>
> **integer**: b -- binary, c -- char, d -- decimal (default), o -- octal, x or X -- hexa…
>
> **float**: e or E -- exponential, f or F -- fixed point, g or G -- appropriate (default), % -- percent
>
> **string**: s ....



```
print('{0:.3f}'.format(1.0/3))   ==> 0.333

# 使用下划线填充文本，并保持文字处于中间位置, 使用 (^) 定义 '___hello___'字符串长度为11
print('{0:_^11}'.format('hello'))  ==> ___hello___
"{:+2.3f}".format(45.7273)  ==> +45.727
"{1:>10s}".format(8,"toto")  ==> '        toto'
```

 `print` 总是会以一个不可见的“新一行”字符（`\n`）结尾，因此重复调用 `print`将会在相互独立的一行中分别打印。为防止打印过程中出现这一换行符，可以通过 `end` 指定其应以空白结尾：

```
print('a', end='')
print('b', end='')

```

输出结果如下：

```
ab

```

或者通过 `end` 指定以空格结尾：

```
print('a', end=' ')
print('b', end=' ')
print('c')

```

输出结果如下：

```
a b c

```

#### 转义序列

如何生成一串包含单引号（'）的字符串，如果 ' 已经代表了开头和结尾? 可以通过转义序列（Escape Sequence） 来实现。
通过 `\ (反斜杠)` 来指定单引号。字符串指定为 'What\'s your name?'。
另一种方法："What's your name?"，使用双引号。必须在使用双引号括起的字符串中对字符串内的双引号使用转义序列。
使用转义序列 \\ 来指定反斜杠本身。
如果你想指定一串双行字符串该怎么办？一种方式即使用如前所述的三引号字符串，或者你可以使用一个表示新一行的转义序列——\n 来表示新一行的开始。下面是一个例子：

```
'This is the first line\nThis is the second line'

```

在一个字符串中，一个放置在末尾的反斜杠表示字符串将在下一行继续，但不会添加新的一行：

```
"This is the first sentence. \
This is the second sentence."

```

相当于

```
"This is the first sentence. This is the second sentence."
```

#### 原始字符串

如果需要指定一些未经过特殊处理的字符串，比如转义序列，那么需要在字符串前增加 `r` 或 `R` 来指定一个原始 (Raw) 字符串。

```
r"Newlines are indicated by \n"

```

> **针对正则表达式用户的提示**
>
> 在处理正则表达式时应全程使用原始字符串。否则，将会有大量 Backwhacking 需要处理。举例说明的话，反向引用可以通过 `'\\1'` 或 `r'\1'` 来实现。



#### Cheatsheet 

- `+`: 字符串连接。
- `*`: 返回字符串重复指定次数后的结果。
- `str()`: 将变量转换为字符串
- `s[i]`:  取第 i 位的字符（索引从0开始）
- `s[-i]`:  取倒数第 i 位的字符 
- `s[i:j]`:  取从第 i (包括) 位到第 j (不包括) 位的字符
- `s.upper()`: 将字符串转换为大写
- `s.lower()`: 将字符串转换为小写
- `s.startswith("hel")`: 检测字符串是否以字符串 "hel" 开头
- `s.endswith("lo")`: 检测字符串是否以字符串 "lo" 结尾
- `s.find(x)`: 字符串中第一次出现 x 的位置
- `s.count('w')`: 字符串中 w 出现的次数
- `s.replace('e', 'i')`: 用 i 替换字符串中的所有 e
- `s.split(x)`: 返回一个字符串被 x 拆分后产生的列表
- `s.join(L)`: 返回一个由字符串 s 作为连接符将列表 L连接起来形成的新字符串
- `s.strip()`: 移除字符串头尾指定的字符 (默认为空格)，中间部分不会移除。返回移除字符串头尾指定的字符后生成的新字符串。   
- `s.ljust(width[, fillchar])`: 返回一个原字符串左对齐,并使用 fillchar 填充至长度 width 的新字符串，fillchar 默认为空格。                                   
- `s.rjust(width[, fillchar])`: 返回一个原字符串右对齐,并使用空格填充至长度 width 的新字符串。如果指定的长度小于字符串的长度则返回原字符串。                       
-  `center(width, fillchar)`: 返回一个指定的宽度 width 居中的字符串，fillchar 为填充的字符，默认为空格。                                        


 


### 逻辑

#### Cheatsheet

- `<`: 小于; `>`: 大于; `<=`: 小于等于; `>=`: 大于等于

- `==`: 比较两个对象 (数值或字符串) 是否相等。

- `!=`: 比较两个对象 (数值或字符串) 是否不相等。

- `not`: 布尔“非”; `and`: 布尔“与”; `or`: 布尔“或”

- `in`: x (数值、字符串、列表) 是否存在于 y (字符串、列表、字典...) 中

- `bool()`: 将变量转换为布尔值

  ​



###  二进制数的操作符

- `<<`: 将数字的位向左移动指定的位数。（每个数字在内存中以二进制数表示，即 0 和1）        

- `>>`: 将数字的位向右移动指定的位数。                     

- `&`: 对数字进行按位与操作。              

- `|`: 对数字进行按位或操作。               

- `^`: 对数字进行按位异或操作。                

- `~`: 按位取反。      

  ​



## 数值运算与赋值的快捷方式

一种比较常见的操作是对一个变量进行一项数学运算并将运算得出的结果返回给这个变量。            

`变量 = 变量 运算 表达式` 会演变成 `变量 运算 = 表达式`。

```
x += 4    #equal to x = (x + 1) increment
x -= 3    #equal to x = (x - 1) decrement
```



## 求值顺序

下表中给出 Python 中从最低优先级（最少绑定）到最高优先级（最多绑定）的优先级表。位列同一行的运算符具有相同优先级。在给定的表达式中，Python 将优先计算表中位列于后的较高优先级的运算符与表达式。

- `lambda`：Lambda 表达式                
- `if - else` ：条件表达式                
- `or`：布尔“或”               
- `and`：布尔“与”                
- `not x`：布尔“非”                                                
- `in, not in, is, is not, <, <=, >, >=, !=, ==`：比较，包括成员资格测试（Membership Tests）和身份测试（Identity Tests）。                      
- `|`：按位或                       
- `^`：按位异或                 
- `&`：按位与                      
- `<<, >>`：移动                     
- `+, -`：加与减                      
- `*, /, //, %`：乘、除、整除、取余               
- `+x, -x, ~x`：正、负、按位取反                   
- `**`：求幂                            
- `x[index], x[index:index], x(arguments...), x.attribute`：下标、切片、调用、属性引用                            
- `(expressions...), [expressions...], {key: value...}, {expressions...}`：表示绑定或元组、表示列表、表示字典、表示集合             


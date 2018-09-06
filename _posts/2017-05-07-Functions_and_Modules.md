---
layout: post
title: Functions and Modules
author: CY
tags: [Python]
categories: [Python]
share: false
image:
  background: triangular.png
---



## 函数 (Functions)

函数 (Functions) 是指可重复使用的程序片段。通过对某个代码块赋予名字，可以通过调用 (calling) 这一特殊的名字在程序的任何地方来运行代码块，并可重复任何次数。前面已经介绍了许多内置的函数，例如 `len` 和 `range`。类比R中的function。

函数表达式:  

```
def 函数标识符(函数参数):  #函数不使用参数时，括号中可以不声明变量
	语句块
	
函数标识符(函数参数)   #调用函数
```



### 函数参数

函数中的参数通过将其放置在用以定义函数的一对圆括号中指定，并通过逗号予以分隔。当调用函数时，以同样的形式提供需要的值。

形参 (Parameters): 在定义函数时给定的名称。

实参 (Arguments): 在调用函数时你所提供给函数的值。



### 局部和全局作用域

在一个函数的定义中声明的变量，它们不会以任何方式与所在函数之外但具有相同名称的变量产生关系。即这些变量名只存在于该函数这一局部 (Local)。这些变量被称为局部变量，该函数块为这些局部变量的作用域 (Scope)。                   

通过 `global` 语句声明全局变量                                   

- 全局作用：函数之外                              
- 局部作用：函数之内                                                                         
- 局部可以访问全局变量，而全局不能使用局部变量                                                          
- 同理局部变量不能使用其他局部变量                
- 应尽量避免名称相同的局部变量和全局变量                             




### 默认参数值

经常看到，有些函数中经常有一些参数可选并使用默认的值，以避免用户不想为他们提供值的情况。默认参数值可以有效帮助解决这一情况。可以通过在函数定义时附加一个赋值运算符 (=) 来为参数指定默认参数值。默认参数值应该是不可变的。

```
def say(message, times=1):
    print(message * times)

say('Hello')  ==> Hello
say('World', 5)  ==> WorldWorldWorldWorldWorld
```

> 只有那些位于参数列表末尾的参数才能被赋予默认参数值，意即在函数的参数列表中拥有默认参数值的参数不能位于没有默认参数值的参数之前。这是因为值是按参数所处的位置依次分配的。举例来说，`def func(a, b=5)` 是有效的，但 `def func(a=5, b)` 是*无效的*。
>



### 关键字参数

对于一些具有许多参数的函数，如果只想对其中的一些参数进行指定，可以通过命名它们 (关键字) 来给这些参数赋值， 这就是关键字参数 (Keyword Arguments)。               
关键字参数的优点： 

- 不需要考虑参数的顺序，函数的使用将更加容易        
- 只需要对希望赋予的参数赋值，只要其它的参数都具有默认参数值

```
def key(a, b=5, c=10):
    print('a is', a, 'and b is', b, 'and c is', c)

key(3, 7) ==> a is 3 and b is 7 and c is 10
key(c=50, a=100) ==> a is 100 and b is 5 and c is 50
```



### 可变参数

如果想使定义的函数里面能够有任意数量的变量，也就是参数数量是可变的，可以通过使用星号来实现。      

- 当声明一个`单星号`参数时，如 `*`param，从此处开始直到结束的所有`位置参数`都将被收集并汇集成一个称为param的**元组**。                                                          
- 当声明一个`双星号`参数时，如 `**`param，从此处开始直至结束的所有`关键字参数`都将被收集并汇集成一个名为 param 的 **字典**。                                          

```
def total(a=5, *numbers, **phonebook):
    print('a', a)

    #遍历元组中的所有项目
    for single_item in numbers:
        print('single_item', single_item)

    #遍历字典中的所有项目
    for first_part, second_part in phonebook.items():
        print(first_part,second_part)

print(total(10,1,2,3,Jack=1123,John=2231,Inge=1560))
```

输出：

```
a 10
single_item 1
single_item 2
single_item 3
Inge 1560
John 2231
Jack 1123
None
```



### `return` 语句

`return` 语句用于在中断函数时从函数中返回一个值。每一个函数都在其末尾隐含了一句 `return None`，除非写了自己的 `return` 语句。



### DocStrings

文档字符串 (Documentation Strings,  DocStrings) 能够帮助用户更好地记录程序并让其更加易于理解。当程序实际运行时，可以通过一个函数来获取文档。文档字符串也适用于模块 (Modules) 和类 (Class) 。

文档字符串所约定的是`一串多行字符串`，其中第一行以某一大写字母开始，以句号结束。第二行为空行，后跟的第三行开始是任何详细的解释说明。强烈建议在所有重要功能的所有文档字符串中都遵循这一约定。

可以通过使用函数的 `__doc__`  (一对双下划线) 属性 (属于函数的名称) 来获取函数的文档字符串属性。Python 的 help() 函数所做的便是获取函数的 `__doc__` 属性并以一种整洁的方式将其呈现给用户。

```
def print_max(x, y):
    '''打印两个数值中的最大数。

    这两个数都应该是整数'''
    other sentences
    
print(print_max.__doc__)
```

输出：

```
打印两个数值中的最大数。

    这两个数都应该是整数
```



## 模块 (Modules)

模块是一组Python代码的集合，可以使用其他模块，也可以被其他模块使用。一个包含函数与变量，以 `.py` 为后缀的文件就是一个模块。                                  

创建模块时，要注意：                    

- 模块名要遵循Python变量命名规范，不能使用中文、特殊字符；                  
- 模块名不要和系统模块名冲突，最好先查看系统是否已存在该模块。检查方法是在Python交互环境执行`import 模块名`，若成功则说明系统存在此模块。                                   



### 按字节码编译的 .pyc 文件

通常运行模块的时候，`.py `文件所在的目录中会创建 `.pyc` 文件。这是一种按字节码编译 (Byte-Compiled) 的文件，以 .pyc 为扩展名，是将 Python 转换成中间形式的文件。此文件的产生是因为，导入一个模块是一件代价高昂的事情，此.pyc 文件使得下一次从其它不同的程序导入模块时变得更加快速，因为导入模块时所需要的一部分处理工作已经完成了。同时，这些按字节码编译的文件是独立于运行平台的。当然如果 Python 没有相应的权限对 `.py` 文件所在的目录进行写入文件的操作，那么 `.pyc` 文件将不会被创建。



### `import`载入模块的四种方法

```
1. import module  载入模块             
# 需要用“module.函数名”来引出功能                               
2. import module as __   重命名模块为__       
# 需要用“__.函数名”来引出功能
3. from module import functions  载入模块的部分函数      
# 可以直接用函数名来引出功能
4. from module import *   输入模块的所有功能     
# 可以直接用函数名来引出功能
```



如果想直接将 `argv` 变量导入程序 (为了避免每次都要输入 `sys.`)，可以通过使用 `from sys import argv` 语句来实现。

> **警告：**一般来说，应该尽量避免使用 `from...import` 语句，而去使用 `import` 语句。这是为了避免在程序中出现名称冲突，同时也为了使程序更加易读。



### 模块的 `__name__`

每个模块都有一个名称，而模块中的语句可以找到它们所处的模块的名称。当模块第一次被导入时，它所包含的代码将被执行。可以通过这一特性来使模块以不同的方式运行，这取决于它是为自己所用还是从其它从的模块中导入而来。这可以通过使用模块的 `__name__` 属性来实现。每一个 Python 模块都定义了它的 `__name__` 属性。如果它与 `__main__` 属性相同则代表这一模块是由用户独立运行的，否则是被导入进来运行的。

案例（保存为 `module_using_name.py`）：

```
if __name__ == '__main__':
    print('This program is being run by itself')
else:
    print('I am being imported from another module')

```

输出：

```
$ python module_using_name.py
This program is being run by itself

$ python
>>> import module_using_name
I am being imported from another module
>>>
```



### 包 (package)

 包是一种能够方便地分层组织模块的方式。变量通常位于函数内部，函数与全局变量通常位于模块内部。模块通常位于包的内部。          

包是指一个包含模块与一个特殊的 `__init__.py` 文件的文件夹，后者向 Python 表明这一文件夹是特别的，因为其包含了 Python 模块。            

```
<some folder present in the sys.path>
World                  --package
 ├─ __init__.py        
 ├─ Asia               --sub-package
 │  ├─ __init__.py
 │  ├─ India
 │  	├─ __init__.py
 │  	├─ foo.py
 │  	└─ www.py
 ├─ Africa
 │  ├─ __init__.py
 │  ├─ madagascar
 │  	├─ __init__.py
 │  	├─ bar.py
 │  	└─ casino.py
```



## 标准库

[Python 标准库 (Python Standrad Library)](https://docs.python.org/3/library/) 中包含了大量有用的模块，可以查找到所有模块的全部细节。熟悉 Python 标准库十分重要，熟知这些库可以做到什么事，许多问题都能够轻易解决。

列举一些有用的模块: 

`platform` 用以获取平台操作系统的信息
`logging` 模块用来记录 (Log) 信息。

`sys` 模块包含了与 Python 解释器及其环境相关的功能，即系统功能 (system)。           
`sys.argv` 变量是一系列包含了命令行参数 (Command Line Arguments) 的列表。列表里包含命令行传递的程序的参数。`argv`至少有一个元素，因为第一个参数永远是该`.py`文件的名称                           
`sys.path`包含了导入模块的字典名称列表。如果sys.path的第一段字符串是空的，代表当前目录是 sys.path 的一部分，与PYTHONPATH 环境变量等同。这意味着可以直接导入位于当前目录的模块。否则，必须将模块放置在 sys.path 内所列出的目录中。                                   

`dir()` 能够返回由对象所定义的名称列表。如果对象是一个模块，则该列表会包括函数内所定义的函数、类与变量。 如果没有提供参数，函数将返回当前模块的名称列表。 


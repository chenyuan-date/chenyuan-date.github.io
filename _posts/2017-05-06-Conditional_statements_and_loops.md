---
layout: post
title: Conditional statements and Loops
author: CY
tags: [Python]
categories: [Python]
share: false
image:
  background: triangular.png
---



在 Python 中有三种控制流语句——`if`, `for` 和 `while`。

## `if` 语句

`if` 语句用以检查条件：*如果* 条件为真 (True)，我们将运行一块语句 (称作 if-block 或 if 块)，*否则* 我们将运行另一块语句 (称作 else-block 或 else 块)。其中 *else* 从句是可选的。 `elif` 语句，可以将两个相连的 `if else-if else` 语句合并成一句 `if-elif-else` 语句。这能够使程序更加简便，并且可以减少所需要的缩进量。

**if 语句**

if 条件 (True or False) ：

```
代码块1
```

elif 条件 ：

```
代码块2
```

else:

```
代码块3
```

Example:

```
age = int(input('please enter your age!\n'))  #input()函数以字符串的形式返回从屏幕中输入的内容。
if age < 18:
    print('Hi, kids')
elif 40 >= age >= 18:
    print('Hi, young man')
else:
    print('Hi, old man')
```



## `break` 语句

`break` 语句用以中止循环语句的执行，即使循环条件没有变更为 False，或队列中的项目尚未完全迭代依旧如此。如果中断了一个 for 或 while 循环，任何相应循环中的 else 块都将不会被执行。



## `continue` 语句

`continue` 语句用以告诉 Python 跳过当前循环块中的剩余语句，并继续该循环的下一次迭代。



## `while` 语句

`while` 语句能够让你在条件为真的前提下重复执行某块语句。 `while` 语句是 循环 (Looping) 语句的一种。`while` 语句同样可以拥有 `else` 子句作为可选选项。

```
# 模拟登陆账号

while True:
    name = input('Who are you?\n')
    if name != 'Bob':
        continue  # 将程序跳转到循环开头
    print('Hello, Bob. What is your password?')
    password = input()
    if password == 'fish':
        break    #跳出该while循环
print('Access granted!')
```



## `for` 循环

`for...in` 特点是会在一系列对象上进行迭代 (Iterates)，意即它会遍历序列中的每一个项目。

```
# for 和 range() 实现固定的循环次数
for i in range(5):
    print(i)
    print('Hello world')
```


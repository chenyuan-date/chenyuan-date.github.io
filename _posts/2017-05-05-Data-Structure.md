---
layout: post
title: Python Data Structure
author: CY
tags: [Python]
categories: [Python]
share: false
image:
  background: triangular.png
---



数据结构 (Data Structures) 是一种结构，能够将一些数据聚合在一起，它们是用来存储一系列相关数据的集合。

Python 中有四种内置的数据结构:  列表 (List)、元组 (Tuple)、字典 (Dictionary) 和集合(Set)。



## 列表

`列表` 是一种用于保存一系列有序项目的集合。         

列表用方括号括起来，列表项目之间以逗号相隔。 列表项目可以被添加、移除或搜索， 所以列表是一种可变的 (Mutable) 的数据类型。

### Cheatsheet

选取列表元素 (索引从0开始)
**subset **                        

- `L[0]:` 返回列表的第一个元素
- `L[i]:` 返回列表中索引值为 i 的元素
- `L[-1]:` 返回列表的最后一个元素

**slice **                           

- `L[i:j]`: 返回列表中索引值为 i:(j-1) 的元素 [左闭右开)
- `L[1:]`: 返回列表中索引值大于等于1的元素
- `L[:3]`: 返回列表中索引值小于3的元素
- `L[:]`: 复制列表

**Subset Lists of Lists**              

`L[1][0]`: 
`L[1][:2]`: 

**List 相关函数**                

- `L1 + L2`: 合并两个列表
- `L*n`: 将列表重复 n 次
- `L = list()`: 创建空列表
- `L[i] = x`: 将 x 赋值给列表索引值为 i 的元素
- `len(L)`: 返回列表中项目的数目 
- `sum(L)`: 返回列表中所有数值的和
- `min(L)`: 返回列表中最小的数值
- `max(L)`: 返回列表中最大的数值
- `L.index(item)`: 返回列表中项目 item 的索引值
- `L.append(item)`: 在列表最后追加 item
- `L.insert(i, item)`: 在列表中索引值为 i 的位置插入元素item
- `L.remove(item)`: 从列表中删除第一个出现的 item
- `del L[item]`: 删除列表中的item
- `L.pop(e)`: 删除列表中索引值为 e 的项目，且返回该项目
- `L.count(item)`: 统计 item 在列表中出现的次数
- `L.reverse()`: 颠倒列表中项目的顺序
- `L.sort()`: 升序重新排列列表中的项目
- `" ".join(["A","B","C","D"])`: 将列表转换为字符串 "A B C D"
- `L.extend(L)`: appends L to the end of the list
- `L.clear()`: 清空列表
- `L.copy()`:  复制列表
- `map(function, L)`:  将function函数作用于列表中的数值




## 元组

元组（Tuple）用于将多个对象保存到一起。可以近似地看作列表，但是元组不能提供列表类能够提供的广泛的功能。元组的一大特征类似于字符串，它们是不可变的，不能编辑或更改元组。

元组是通过特别指定项目来定义的，在指定项目时，可以给它们加上括号，并在括号内部用逗号进行分隔。

元组通常用于保证某一语句或某一用户定义的函数可以安全地采用一组数值，意即元组内的数值不会改变。

> 推荐总是对元组使用括号, 来指明元组的开始与结束。尽管括号是一个可选选项, 明了胜过晦涩，显式优于隐式。

> **包含 0 或 1 个项目的元组**
>
> 一个空的元组由一对圆括号构成 `T = ()` 。然而，拥有一个项目的元组必须在第一个（也是唯一一个）项目的后面加上一个逗号来指定它，如此一来 Python 才可以识别出在这个表达式想表达的究竟是一个元组还是只是一个被括号所环绕的对象。如果想指定一个包含项目 `2` 的元组，必须指定 `T = (2, )`。



### Cheatsheet 

* `tuple()`:   Empty tuple                                               
* `T[idx]`, `T[idx1:idx2]`: 获取元组中的项目(索引值)                            
* `T.count(item)`: 元组中item出现的次数                            
* `T.index(item)`: 元组中第一次出现item的索引值。如果不存在会显示: ValueError                                     



## 字典

在字典中，你可以通过使用符号构成 `d = {key : value1 , key2 : value2}` or `d[key] = value`这样的形式，来成对地指定键值(key)与值(value)。在这里要注意到成对的键值与值之间使用冒号分隔，而每一对键值与值则使用逗号进行区分，它们全都由一对花括号括起。键值必须是唯一的。              

另外需要记住，字典中的成对的键值—值配对不会以任何方式进行排序。如果你希望为它们安排一个特别的次序，只能在使用它们之前自行进行排序。                                             

Note: 只能使用不可变的对象（如字符串）作为字典的键值，但是可以使用可变或不可变的对象作为字典中的值。                         



### Cheatsheet

* `dict()`: 空字典
* `D = {}`: 定义一个空字典
* `D[k] = x`: 替换或者赋值 x 给字典中的键值 k; 添加新的键值对
* `D[k]`: 取出键值 k 对象的值
* `D.get(k)`: 取出键值 k 对象的值
* `del D[k]`: 删除键值 k 和其对应的值
* `D.keys()`: 返回字典中的所有键值
* `D.values()`: 返回字典中一系列的值
* `D.items()`: 返回字典中所有的键值对
* `D.pop()`: 删除键值对应的值，并返回它的值
* `D.update(D)`: 添加新的字典D于字典D
* `D.clear()`: 清空字典
* `D.copy()`: 复制字典
* `"key" in D`: 检查某对键值—值配对是否存在 . True， 如果 key 存在于字典, 否则 False



## 集合

集合（Set）是简单对象的无序集合（Collection）。当集合中的项目存在与否比起次序或其出现次数更加重要时，我们就会使用集合。

通过使用集合，你可以测试某些对象的资格或情况，检查它们是否是其它集合的子集，找到两个集合的交集，等等。

```
>>> bri = set(['brazil', 'russia', 'india'])
>>> 'india' in bri   ---> True
>>> 'usa' in bri  ---> False
>>> bric = bri.copy()
>>> bric.add('china')
>>> bric.issuperset(bri)  ---> True
>>> bri.remove('russia')
>>> bri & bric OR bri.intersection(bric)  ---> {'brazil', 'india'}
```



## 序列

序列的主要功能是**资格测试（Membership Test）**（也就是 `in` 与 `not in` 表达式）和**索引操作（Indexing Operations）**，它们能够允许我们直接获取序列中的特定项目。列表、元组和字符串可以看作序列（Sequence）的某种表现形式，它们拥有一种切片（Slicing）运算符，能够允许提取序列中的一部分 (要记得 Python 从 0 开始计数)。                      

同样可以在切片操作中提供第三个参数，这一参数将被视为切片的*步长（Step）*（在默认情况下，步长大小为 1）：

```
>>> shoplist = ['apple', 'mango', 'carrot', 'banana']
>>> shoplist[::1]
['apple', 'mango', 'carrot', 'banana']
>>> shoplist[::2]
['apple', 'carrot']
>>> shoplist[::3]
['apple', 'banana']
>>> shoplist[::-1]
['banana', 'carrot', 'mango', 'apple']
```


---
layout: post
title: Input and Output
author: CY
tags: [Python]
categories: [Python]
share: false
image:
  background: triangular.png
---



## 交互输入输出
通过 input() 函数与 print 函数来实现交互式输入输出



## 文件输入输出

在 Python 中，读文件主要分为三个步骤：

- 打开文件 (open)

- 读取内容 (read)

- 关闭文件(close)

  ​

一般使用形式如下：

```
try:
    f = open('/path/to/file', 'r')    # 打开文件
    data = f.read()                   # 读取文件内容
finally:
    if f:
        f.close()                     # 确保文件被关闭
```

由于文件读写时都有可能产生`IOError`，一旦出错，后面的`f.close()`就不会调用。所以，为了保证无论是否出错都能正确地关闭文件，可以使用`try ... finally`来实现

但是每次都这么写太繁琐，所以Python引入了`with`语句来自动帮我们调用`close()`方法：

```
with open('/path/to/file', 'r') as f:
    data = f.read()
```



### 打开文件 (open)

用`open`函数打开文件，有不同的模式：

默认读入的文件是文本模式`t`。           

- 读模式
  - `r`: 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。
- 写模式
  - `w`: 打开一个文件只用于写入。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。
  - `a`: 打开一个文件用于追加。如果该文件已存在，从文件的结尾写入。如果该文件不存在，创建新文件进行写入。
- 读/写模式 (`+`)
  - `r+`: 打开一个文件用于读写。文件指针将会放在文件的开头。                          
  - `w+`: 打开一个文件用于读写。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。 
  - `a+`: 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。
- `b` 二进制模式 (可添加到其他模式中使用)



### 读取内容 (read) 

通常而言，读取文件有以下几种方式：

- 一次性读取所有内容，使用 `read()` 或 `readlines()`；
  - 把文件读入一个字符串列表，在列表中每个字符串就是一行。文件小的话，方便
- 按字节读取，使用 `read(size)`；
  - 文件较大，可以按字节读取。
- 按行读取，使用 `readline()`；
  - 文件较大，可以按行读取 (很慢)。



### 文件迭代器 

在 Python 中，文件对象是可迭代的，可以直接在 for 循环中使用它们，而且是逐行迭代的，效果和 `readline()` 一样，而且更简洁。

```
with open('data.txt', 'r') as f:
    for line in f:
        print(line.strip()) # 把末尾的'\n'删掉

with open('data.txt', 'r') as f:
    print f.readline(),
```

### 写文件

写文件和读文件是一样的，唯一区别是调用`open()`函数时，传入标识符`'w'`或者`'wb'`表示写文本文件或写二进制文件。如果文件已存在，则会清空原内容并覆盖掉；如果路径正确，但文件不存在，会新建一个文件，并写入；如果路径不正确，会抛出 IOError。    

```
with open('/path/file/data.txt', 'w') as f:
    f.write('one\n')
    f.write('two')
```



## OS 模块的目录文件操作

`os` 用以和操作系统交互。Python 的 `os` 模块封装了常见的文件和目录操作，部分常见用法：

| 方法                 | 说明             |
| ------------------ | -------------- |
| os.mkdir("dir")    | 创建目录           |
| os.rmdir("dir")    | 删除目录           |
| os.rename          | 重命名文件或目录       |
| os.remove          | 删除文件           |
| os.getcwd()        | 获取当前工作路径       |
| os.chdir("newdir") | 改变当前的目录        |
| os.walk            | 遍历目录           |
| os.path.join       | 连接目录与文件名       |
| os.path.split      | 分离文件名与目录       |
| os.path.abspath    | 获取绝对路径         |
| os.path.dirname    | 获取路径           |
| os.path.basename   | 获取文件名或文件夹名     |
| os.path.splitext   | 分离文件名与扩展名      |
| os.path.isfile     | 判断给出的路径是否是一个文件 |
| os.path.isdir      | 判断给出的路径是否是一个目录 |



## Pickle

Python 提供了一个叫作 `Pickle` 的标准模块，通过它你可以将任何纯 Python 对象存储到一个文件中，并在稍后将其取回。这叫作*持久地（Persistently）*存储对象。

案例（保存为 `io_pickle.py`）：

```
import pickle

# 我们存储相关对象的文件的名称
shoplistfile = 'shoplist.data'
# 需要购买的物品清单
shoplist = ['apple', 'mango', 'carrot']

# 准备写入文件
f = open(shoplistfile, 'wb')
# 转储对象至文件
pickle.dump(shoplist, f)
f.close()

# 清除 shoplist 变量
del shoplist

# 重新打开存储文件
f = open(shoplistfile, 'rb')
# 从文件中载入对象
storedlist = pickle.load(f)
print(storedlist)
```

输出：

```
$ python io_pickle.py
['apple', 'mango', 'carrot']

```

**它是如何工作的**

要想将一个对象存储到一个文件中，我们首先需要通过 `open` 以写入（**w**rite）二进制（**b**inary）模式打开文件，然后调用 `pickle` 模块的 `dump` 函数。这一过程被称作*封装（Pickling）*。

接着，我们通过 `pickle` 模块的 `load` 函数接收返回的对象。这个过程被称作*拆封（Unpickling）*。



## Unicode

当阅读或写入某一文件或当希望与互联网上的其它计算机通信时，需要将 Unicode 字符串转换至一个能够被发送和接收的格式，这个格式叫作“UTF-8”。在这一格式下进行读取与写入，需使用 `io.open` 提供的 `编码(Encoding) ` 与 `解码(Decoding)` 参数来告诉 Python 我们正在使用 Unicode。




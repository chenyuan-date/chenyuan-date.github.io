---
layout: post
title: Jupyter notebook 的安装与使用
author: CY
tags: [Python]
categories: [Python]
share: false
image:
  background: triangular.png
---



## Online tool

推荐一个在线的jupyter notebook工具，可以直接在网页上coding and run。我觉得对于初学者还是有帮助的，特别是对我这种不想在电脑上安装太多软件的人来说，好处大大滴。     

[Jupyter](https://hub.mybinder.org/user/ipython-ipython-in-depth-ezdqr7df/notebooks/binder/Index.ipynb#)            



## 安装

等以后实战安装了再来根据我的安装过程补充



## 使用

新建：点击 `New` - `Python3` 就可以新建一个notebook。
书写：鼠标点击即可写代码。按图示更改每个输入框的内容属性，选择Code和Markdown
运行：点击 `run cell` 运行代码， 或转换Markdown文本。



## 快捷操作

Jupyter Notebook 有两种键盘输入模式:                                  

- 编辑模式: 允许你往单元中键入代码或文本；这时的单元框线是绿色的。                                
- 命令模式: 键盘输入运行程序命令；这时的单元框线是灰色。                  

`Shift+Enter`: 运行本单元，选中下个单元                   

`Ctrl+Enter`: 运行本单元                       

`Alt+Enter`: 运行本单元，在其下插入新单元                         

`y`：单元转入代码状态                         

`m`：单元转入markdown状态                     

`a` ：在上方插入新单元                    

`b`：在下方插入新单元                   

`x`：剪切选中的单元                   

`Shift+V`：在上方粘贴单元                    



## 小技巧

1. 代码框输入 `%load sxbd.py` 会加载之前写过的脚本
2. 也可以加载在线代码  `% load http://www.sxbd.com/sxbd.py`
3. 代码框输入`%run progam`即可运行写好的Python脚本(一般不写后缀)
4. 代码框输入`!bash command`可运行bash命令
5. `%matplotlib inline`嵌入matplotlib的图像
6. `%timeit python scripts`评估函数的运行时间和内存使用
7. `%lsmagic`列出所有的magic函数
8. 代码框开头输入`%%writefile sxbd.py`即可把当前cell的命令存到对应文件




## 插件安装

- 安装时先关闭Jupyter程序

- 安装Jupyter插件管理工具 `conda install -c conda-forge jupyter_contrib_nbextensions`

- 激活Jupyter插件管理工具 `jupyter nbextensions_configurator enable --user`

- 安装jupyter-vim-binding

  ```
  # You may need the following to create the directoy
  # 一般是家目录下的 ~/.local/share/jupyter/nbextensions
  mkdir -p $(jupyter --data-dir)/nbextensions
  # Now clone the repository
  cd $(jupyter --data-dir)/nbextensions
  git clone https://github.com/lambdalisue/jupyter-vim-binding vim_binding
  chmod -R go-w vim_binding

  ```

- 激活jupyter-vim-binding

  启动Jupyter notebook, 进入http://localhost:8888/nbextensions/，激活插件

  每个插件点击可查看其功能描述，使用方式，批量`gif`演示插件功能。




## 服务器端使用

`jupyter notebook --no-browser -y`即可启动，访问`IP:8888`即可。



## 主题

安装主题控制插件

```
pip install jupyterthemes

```

修改主题，具体参数看`jt`命令解释 <https://github.com/dunovank/jupyter-themes>。

```
jt -fs 200 -tfs 17 -t grade3 -f roboto -cellw 88% -dfs 12 -ofs 15 -T

```



## References

[nbextensions](https://github.com/ipython-contrib/jupyter_contrib_nbextensions#installation)



[Jupyter notebook使用](http://blog.genesino.com/2017/12/jupyter/)                                                      

[Jupyter Notebook快速安装教程](http://blog.csdn.net/dream_an/article/details/50464940)       

https://bop.mol.uno/05.installation.html
---
layout: post
title: Git Repository init, add, commit, log, diff 
author: CY
tags: [Git]
categories: [Git]
share: false
image:
  background: triangular.png
---



## Git 是啥

[Git](https://git-scm.com/) 是一个分布式版本控制系统. 它的灵活性, 优越性使得它从2005年发布以来. 获得了越来越多的使用和支持。       

Git 可以管理：文本文件 (.txt) 等; 脚本文件 (.py) 等; 以及各种基于文本信息的文件。                           

Git 不可以管理：图片文件 (.jpg) 等; MS word (.doc) 等。               

Git 安装很简单，只需要按照 [Git 官网安装说明](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) 进行即可。      



## 创建版本库 Repository    



![Git工作流程图](https://git-scm.com/book/en/v2/images/lifecycle.png)



### 创建版本库 (init)

首先要确定要把哪个文件夹里的文件进行管理。创建一个叫 `github` 的文件夹。 然后在 Terminal (Windows 的 git bash) 中把当前目录调到这个文件夹 `github`:          

```
$ cd ~/Desktop/github
```

为了更好地使用 git，同时记录进行修改的人，使得人和修改能够对应上。可以在 git 中添加用户名 `user.name` 和 用户 email `user.email`:

```
$ git config --global user.name "CY"
$ git config --global user.email "cy_future@163.com"
```

然后就能在这个文件夹中建立 git 的管理文件了：      

```
$ git init
# Initialized empty Git repository in /Users/CY/Desktop/github/.git/
```

因为这个文件夹中还没有任何的文件，它返回出来一句话告诉我们已经建立了一个空的 git 管理库。      



### 添加文件管理 (add)               

git 创建的管理库文件 `.git` 是被隐藏起来的，所以要通过`ls -a`才能看到被隐藏的文件。                            

使用 `touch` 建立一个新的 `test.txt` 文件，然后 `vim` 编辑内容。最后 `:wq` 保存。                        

现在能用 `status` 来查看版本库的状态：                    

```
$ git status
On branch master    # 在 master 分支
No commits yet
Untracked files:    
  (use "git add <file>..." to include in what will be committed)
	test.txt      #test.txt文件尚未被加入版本库 (unstaged)
nothing added to commit but untracked files present (use "git add" to track)
```

现在 `test.txt` 并没有被放入版本库中 (unstaged)，所以要使用 `add` 把它添加进版本库 (staged)：                    

```
$ git add test.txt

# 再次查看状态 status
$ git status
On branch master
Initial commit
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   test.txt  # 版本库已识别 test.txt (staged)
```

如果想一次性添加文件夹中所有未被添加的文件，可以使用 `git add .`。     



### 提交改变 (commit) 

我们已经添加好了 `test.txt` 文件，最后一步就是提交这次的改变，并在 `-m` 自定义这次改变的信息：             

```
$ git commit -m "create 1.py"
[master (root-commit) cf6eafe] create test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```



## 记录修改 (log & diff)

在 git 中，每一次提交 (commit) 的修改，都会被单独的保存起来。也可以说 git 的中的所有文件都是一次次修改累积起来的。文件好比楼房，每个 commit 记录了盖楼需添加或者拿走的材料，整个施工过程也被记录了下来。  



### [修改记录 log](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)              

之前作者`CY` 对版本库进行了一次修改，添加了一个 `test.txt` 文件。查看该版本库施工过程如下： 

```
$ git log   
commit cf6eafea17b2c3509cd90ad3e20d3f266ac8aa19 (HEAD -> master)
Author: CY <cy_future@163.com>
Date:   Tue Sep 11 15:52:54 2016 +0200
    create test.txt #记录的修改信息
```

如果对`test.txt` 文件进行修改，添加一行文字，然后就可以在 `status` 中看到修改还没被提交的信息。      

```
$ git status     
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
        modified:   test.txt  #这里显示有一个修改尚未被提交
no changes added to commit (use "git add" and/or "git commit -a")    
```

所以要先把这次修改添加 (add) 到可被提交 (commit) 的状态, 然后再提交 (commit) 这次的修改：    

```
$ git add test.txt
$ git commit -m "change add one line" #change后可以是任何对改动内容的解释说明
[master 9e04b97] change add one line 
 1 file changed, 1 insertion(+) #提示添加了一行
```

再次查看 `log`, 现在我们就能看到 `create 1.py` 和 `change 1` 这两条修改信息了. 而且做出这两条 `commit` 的 ID, 修改的 `Author`, 修改 `Date` 也被显示在上面.

```
$ git log
commit 9e04b972f705911c1050577c69fce8c36bf18d54 (HEAD -> master)
Author: CY <cy_future@163.com>
Date:   Tue Sep 11 16:38:03 2018 +0200
    change add one line
commit cf6eafea17b2c3509cd90ad3e20d3f266ac8aa19
Author: CY <cy_future@163.com>
Date:   Tue Sep 11 15:52:54 2018 +0200
    create test.txt
```



### 查看 unstaged 

如果想要查看这次还没 `add` (unstaged) 的修改部分和上个已经 `commit` 的文件有何不同，需使用：[git diff](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#Viewing-Your-Staged-and-Unstaged-Changes)               

```
$ git diff
diff --git a/test.txt b/test.txt
index ca9fde8..b2bcee9 100644
--- a/test.txt
+++ b/test.txt
@@ -1,3 +1,4 @@
 我是示例文件
 我添加了一行文字
-又添加了一行
+minus one line
+add one line      
```



### 查看 staged (--cached) 

如果已经 `add` 了修改，文件变成了 “可提交状态” (staged)，可以在 `diff` 中添加参数 `--cached` 来查看修改：      

```
$ git add .   # add 全部修改文件
$ git diff --cached
输出结果和上面一致    
```



### 查看 staged & unstaged (HEAD) 

查看 `add` 过 (staged) 和 没 `add` (unstaged) 的修改，还可以用另外一种方法。可以对比三种不同的 `diff` 形式。

```
$ git diff HEAD      # staged & unstaged
$ git diff           # unstaged
$ git diff --cached  # staged
```

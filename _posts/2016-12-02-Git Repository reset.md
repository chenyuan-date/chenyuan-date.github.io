---
layout: post
title: Git Repository reset    
author: CY
tags: [Git]
categories: [Git]
share: false
image:
  background: triangular.png
---



# 回到从前 (reset)



### 修改已 commit 的版本 

有时候我们总会忘了什么, 比如已经提交了 `commit` 却发现在这个 `commit` 中忘了附上另一个文件. 接下来我们模拟这种情况. 上节内容中, 我们最后一个 `commit` 是 `change 2`, 我们将要添加另外一个文件, 将这个修改也 `commit` 进 `change 2`. 所以我们复制 `1.py` 这个文件, 改名为 `2.py`. 并把 `2.py` 变成 `staged`, 然后使用 `--amend` 将这次改变合并到之前的 `change 2` 中.

```
$ git add 2.py
$ git commit --amend --no-edit   # "--no-edit": 不编辑, 直接合并到上一个 commit
$ git log --oneline    # "--oneline": 每个 commit 内容显示在一行

# 输出
904e1ba change 2    # 合并过的 change 2
c6762a1 change 1
13be9a7 create 1.py
```

### reset 回到 add 之前 

有时我们添加 `add` 了修改, 但是又后悔, 并想补充一些内容再 `add`. 这时, 我们有一种方式可以回到 `add` 之前. 比如在 `1.py` 文件中添加这一行:

```
d = 3
```

然后 `add` 去 `staged` 再返回到 `add` 之前:

```
$ git add 1.py
$ git status -s # "-s": status 的缩写模式
# 输出
M  1.py     # staged
-----------------------
$ git reset 1.py
# 输出
Unstaged changes after reset:
M	1.py
-----------------------
$ git status -s
# 输出
 M 1.py     # unstaged
```



### reset 回到 commit 之前 

在穿梭到过去的 `commit` 之前, 我们必须了解 git 是如何一步一步累加更改的. 我们截取网上的一些图片 <http://bramus.github.io/ws2-sws-course-materials/xx.git.html>

[![回到从前 (reset)](https://morvanzhou.github.io/static/results/git/2-2-1.png)](https://morvanzhou.github.io/static/results/git/2-2-1.png)

[![回到从前 (reset)](https://morvanzhou.github.io/static/results/git/2-2-2.png)](https://morvanzhou.github.io/static/results/git/2-2-2.png)

[![回到从前 (reset)](https://morvanzhou.github.io/static/results/git/2-2-3.png)](https://morvanzhou.github.io/static/results/git/2-2-3.png)

[![回到从前 (reset)](https://morvanzhou.github.io/static/results/git/2-2-4.png)](https://morvanzhou.github.io/static/results/git/2-2-4.png)

每个 `commit` 都有自己的 `id` 数字号, `HEAD` 是一个指针, 指引当前的状态是在哪个 `commit`. 最近的一次 `commit` 在最右边, 我们如果要回到过去, 就是让 `HEAD` 回到过去并 `reset` 此时的 `HEAD` 到过去的位置.

```
# 不管我们之前有没有做了一些 add 工作, 这一步让我们回到 上一次的 commit
$ git reset --hard HEAD    
# 输出
HEAD is now at 904e1ba change 2
-----------------------
# 看看所有的log
$ git log --oneline
# 输出
904e1ba change 2
c6762a1 change 1
13be9a7 create 1.py
-----------------------
# 回到 c10ea64 change 1
# 方式1: "HEAD^"
$ git reset --hard HEAD^  

# 方式2: "commit id"
$ git reset --hard c6762a1
-----------------------
# 看看现在的 log
$ git log --oneline
# 输出
c6762a1 change 1
13be9a7 create 1.py
```

怎么 `change 2` 消失了!!! 还有办法挽救消失的 `change 2` 吗? 我们可以查看 `$ git reflog` 里面最近做的所有 `HEAD` 的改动, 并选择想要挽救的 `commit id`:

```
$ git reflog
# 输出
c6762a1 HEAD@{0}: reset: moving to c6762a1
904e1ba HEAD@{1}: commit (amend): change 2
0107760 HEAD@{2}: commit: change 2
c6762a1 HEAD@{3}: commit: change 1
13be9a7 HEAD@{4}: commit (initial): create 1.py
```

重复 `reset` 步骤就能回到 `commit (amend): change 2` (id=904e1ba)这一步了:

```
$ git reset --hard 904e1ba
$ git log --oneline
# 输出
904e1ba change 2
c6762a1 change 1
13be9a7 create 1.py
```

我们又再次奇迹般的回到了 `change 2`.



## 回到从前 (checkout 针对单个文件)

之前我们使用 `reset` 的时候是针对整个版本库, 回到版本库的某个过去. 不过如果我们只想回到某个文件的过去, 又该怎么办呢?

### 改写文件 checkout 

其实 `checkout` 最主要的用途并不是让单个文件回到过去, 我们之后会继续讲 `checkout` 在分支 `branch` 中的应用, 这一节主要讲 `checkout` 让文件回到过去.

我们现在的版本库中有两个文件:

```
- gitTUT
    - 1.py
    - 2.py
```

我们仅仅要对 `1.py` 进行回到过去操作, 回到 `c6762a1 change 1` 这一个 `commit`. 使用 `checkout`+ id `c6762a1` + `--` + 文件目录 `1.py`, 我们就能将 `1.py` 的指针 `HEAD` 放在这个时刻 `c6762a1`:

```
$ git log --oneline
# 输出
904e1ba change 2
c6762a1 change 1
13be9a7 create 1.py
---------------------
$ git checkout c6762a1 -- 1.py
```

这时 `1.py` 文件的内容就变成了:

```
a = 1
```

我们在 `1.py` 加上一行内容 `# I went back to change 1` 然后 `add` 并 `commit` `1.py`:

```
$ git add 1.py
$ git commit -m "back to change 1 and add comment for 1.py"
$ git log --oneline

# 输出
47f167e back to change 1 and add comment for 1.py
904e1ba change 2
c6762a1 change 1
13be9a7 create 1.py
```

可以看出, 不像 `reset` 时那样, 我们的 `change 2` 并没有消失, 但是 `1.py` 却已经回去了过去, 并改写了未来.
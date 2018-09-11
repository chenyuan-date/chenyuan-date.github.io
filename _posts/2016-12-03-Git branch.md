---
layout: post
title: Git branch            
author: CY
tags: [Git]
categories: [Git]
share: false
image:
  background: triangular.png
---



## 分支 (branch)



很多时候我们需要给自己或者客户用一个稳定的版本库, 然后同时还在开发另外一个升级版. 自然而然, 我们会想到把这两者分开处理, 用户使用稳定版, 我们开发我们的开发版. 不过 git 的做法却不一样, 它把这两者融合成了一个文件, 使用不同的分支来管理. 所以这一节我们来说说 git 中的 分支 Branch.

### 分支 图例 

之前我们说编辑的所有改变都是在一条主分支 `master` 上进行的. 通常我们会把 `master` 当作最终的版本, 而开发新版本或者新属性的时候, 在另外一个分支上进行, 这样就能使开发和使用互不干扰了. [图片网址](https://www.atlassian.com/git/tutorials/using-branches/)

### 使用 branch 创建 dev 分支 

我们之前的文件当中, 仅仅只有一条 `master` 分支, 我们可以通过 `--graph` 来观看分支:

```
$ git log --oneline --graph
# 输出
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```

### 使用 checkout 创建 dev 分支 

接着我们建立另一个分支 `dev`, 并查看所有分支:

```
$ git branch dev    # 建立 dev 分支
$ git branch        # 查看当前分支

# 输出
  dev       
* master    # * 代表了当前的 HEAD 所在的分支
```

当我们想把 `HEAD` 切换去 `dev` 分支的时候, 我们可以用到上次说的 `checkout`:

```
$ git checkout dev

# 输出
Switched to branch 'dev'
--------------------------
$ git branch

# 输出
* dev       # 这时 HEAD 已经被切换至 dev 分支
  master
```



### 在 dev 分支中修改 

使用 `checkout -b` + 分支名, 就能直接创建和切换到新建的分支:

```
$ git checkout -b  dev

# 输出
Switched to a new branch 'dev'
--------------------------
$ git branch

# 输出
* dev       # 这时 HEAD 已经被切换至 dev 分支
  master
```

### 将 dev 的修改推送到 master 

`dev` 分支中的 `1.py` 和 `2.py` 和 `master` 中的文件是一模一样的. 因为当前的指针 `HEAD` 在 `dev`分支上, 所以现在对文件夹中的文件进行修改将不会影响到 `master` 分支.

我们在 `1.py` 上加入这一行 `# I was changed in dev branch`, 然后再 `commit`:

```
$ git commit -am "change 3 in dev"  # "-am": add 所有改变 并直接 commit
```

### 

好了, 我们的开发板 `dev` 已经更新好了, 我们要将 `dev` 中的修改推送到 `master` 中, 大家就能使用到正式版中的新功能了.

首先我们要切换到 `master`, 再将 `dev` 推送过来.

```
$ git checkout master   # 切换至 master 才能把其他分支合并过来

$ git merge dev         # 将 dev merge 到 master 中
$ git log --oneline --graph

# 输出
* f9584f8 change 3 in dev
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```

要注意的是, 如果直接 `git merge dev`, git 会采用默认的 `Fast forward` 格式进行 `merge`, 这样 `merge` 的这次操作不会有 `commit` 信息. `log` 中也不会有分支的图案. 我们可以采取 `--no-ff` 这种方式保留 `merge` 的 `commit` 信息.

```
$ git merge --no-ff -m "keep merge info" dev         # 保留 merge 信息
$ git log --oneline --graph

# 输出
*   c60668f keep merge info
|\  
| * f9584f8 change 3 in dev         # 这里就能看出, 我们建立过一个分支
|/  
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```



## merge 分支冲突 

今天的情况是这样, 想象不仅有人在做开发版 `dev` 的更新, 还有人在修改 `master` 中的一些 bug. 当我们再 `merge dev` 的时候, 冲突就来了. 因为 git 不知道应该怎么处理 `merge` 时, 在 `master` 和 `dev` 的不同修改.

当创建了一个分支后, 我们同时对两个分支都进行了修改.

比如在:

- `master` 中的 `1.py` 加上 `# edited in master`.
- `dev` 中的 `1.py` 加上 `# edited in dev`.

在下面可以看出在 `master` 和 `dev` 中不同的 `commit`:

```
# 这是 master 的 log
* 3d7796e change 4 in master # 这一条 commit 和 dev 的不一样
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
-----------------------------
# 这是 dev 的 log
* f7d2e3a change 3 in dev   # 这一条 commit 和 master 的不一样
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```

当我们想要 `merge` `dev` 到 `master` 的时候:

```
$ git branch
  dev
* master
-------------------------
$ git merge dev

# 输出
Auto-merging 1.py
CONFLICT (content): Merge conflict in 1.py
Automatic merge failed; fix conflicts and then commit the result.
```

git 发现的我们的 `1.py` 在 `master` 和 `dev` 上的版本是不同的, 所以提示 `merge` 有冲突. 具体的冲突, git 已经帮我们标记出来, 我们打开 `1.py` 就能看到:

```
a = 1
# I went back to change 1
<<<<<<< HEAD
# edited in master
=======
# edited in dev
>>>>>>> dev
```



所以我们只要在 `1.py` 中手动合并一下两者的不同就 OK 啦. 我们将当前 `HEAD` (也就是`master`) 中的描述 和 `dev` 中的描述合并一下.

```
a = 1
# I went back to change 1

# edited in master and dev
```

然后再 `commit` 现在的文件, 冲突就解决啦.

```
$ git commit -am "solve conflict"
```

再来看看 `master` 的 `log`:

```
$ git log --oneline --graph

# 输出
*   7810065 solve conflict
|\  
| * f7d2e3a change 3 in dev
* | 3d7796e change 4 in master
|/  
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```

回到这张图, 他也诠释了两个分支都有更改的时候的样子, 在这种情况下 `merge`, 我们就要使用上述的流程.

[![merge 分支冲突](https://morvanzhou.github.io/static/results/git/4-2-1.png)](https://morvanzhou.github.io/static/results/git/4-2-1.png) 





## rebase 分支冲突



### 什么是 rebase 

和上节内容一样, 不过我们今天来玩一个更高级的合并方式 `rebase`. 同样是合并 `rebase` 的做法和 `merge` 不一样.

假设共享的 branch 是 `branch B`, 而我在 `branch A` 上工作, 有一天我发现`branch B`已经有一些小更新, 我也想试试我的程序和这些小更新兼不兼容, 我也我想合并, 这时就可以用 `rebase`来补充我的分支`branch B`的内容. 补充完以后, 和后面那张图的 `merge` 不同, 我还是继续在 `C3` 上工作, 不过此时的 `C3` 的本质却不一样了, 因为吸收了那些小更新. 所以我们用 `C3'` 来代替.

[![rebase 分支冲突](https://morvanzhou.github.io/static/results/git/4-3-1.png)](https://morvanzhou.github.io/static/results/git/4-3-1.png)

[![rebase 分支冲突](https://morvanzhou.github.io/static/results/git/4-3-2.png)](https://morvanzhou.github.io/static/results/git/4-3-2.png)

[![rebase 分支冲突](https://morvanzhou.github.io/static/results/git/4-3-3.png)](https://morvanzhou.github.io/static/results/git/4-3-3.png)

[![rebase 分支冲突](https://morvanzhou.github.io/static/results/git/4-3-4.png)](https://morvanzhou.github.io/static/results/git/4-3-4.png)

可以看出 `rebase` 改变了 `C3` 的属性, `C3` 已经不是从 `C1` 衍生而来的了. 这一点和 `merge` 不一样. `merge` 在合并的时候创建了一个新的 `C5` `commit`. 这一点不同, 使得在共享分支中使用 `rebase` 变得危险. 如果是共享分支的历史被改写. 别人之前共享内容的 `commit` 就被你的 `rebase` 修改掉了.

[![rebase 分支冲突](https://morvanzhou.github.io/static/results/git/4-2-1.png)](https://morvanzhou.github.io/static/results/git/4-2-1.png)

所以需要强调的是 **!!! 只能在你自己的分支中使用 rebase, 和别人共享的部分是不能用 !!!**. 如果你不小心弄错了. 没事, 我们还能用在 [reset 这一节](https://morvanzhou.github.io/tutorials/others/git/3-1-reset/) 提到的 `reflog` 恢复原来的样子. 为了验证在共享分支上使用 `rebase` 的危险性, 我们在下面的例子中也验证一下.



### 使用 rebase 

初始的版本库还是和上回一样, 在 `master` 和 `dev` 分支中都有自己的独立修改.

```
# 这是 master 的 log
* 3d7796e change 4 in master # 这一条 commit 和 dev 的不一样
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
-----------------------------
# 这是 dev 的 log
* f7d2e3a change 3 in dev   # 这一条 commit 和 master 的不一样
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```

当我们想要用 `rebase` 合并 `dev` 到 `master` 的时候:

```
$ git branch

# 输出
  dev
* master
-------------------------
$ git rebase dev 

# 输出
First, rewinding head to replay your work on top of it...
Applying: change 3 in dev
Using index info to reconstruct a base tree...
M	1.py
Falling back to patching base and 3-way merge...
Auto-merging 1.py
CONFLICT (content): Merge conflict in 1.py
error: Failed to merge in the changes.
Patch failed at 0001 change 3 in dev
The copy of the patch that failed is found in: .git/rebase-apply/patch

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".
```

git 发现的我们的 `1.py` 在 `master` 和 `dev` 上的版本是不同的, 所以提示 `merge` 有冲突. 具体的冲突, git 已经帮我们标记出来, 我们打开 `1.py` 就能看到:

```
a = 1
# I went back to change 1
<<<<<<< f7d2e3a047be4624e83c1265a0946e2e8790f79c
# edited in dev
=======
# edited in master
>>>>>>> change 4 in master
```

这时 `HEAD` 并没有指向 `master` 或者 `dev`, 而是停在了 `rebase` 模式上:

```
$ git branch
* (no branch, rebasing master) # HEAD 在这
  dev
  master
```

所以我们打开 `1.py`, 手动合并一下两者的不同.

```
a = 1
# I went back to change 1

# edited in master and dev
```

然后执行 `git add` 和 `git rebase --continue` 就完成了 `rebase` 的操作了.

```
$ git add 1.py
$ git rebase --continue
```

再来看看 `master` 的 `log`:

```
$ git log --oneline --graph

# 输出
* c844cb1 change 4 in master    # 这条 commit 原本的id=3d7796e, 所以 master 的历史被修改
* f7d2e3a change 3 in dev       # rebase 过来的 dev commit
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```

**!! 注意 !!** 这个例子也说明了使用 `rebase` 要万分小心, 千万不要在共享的 branch 中 `rebase`, 不然就像上面那样, 现在 `master` 的历史已经被 `rebase` 改变了. `master` 当中别人提交的 `change 4` 就被你无情地修改掉了, 所以千万不要在共享分支中使用 `rebase`. 



## 临时修改 (stash)

想想有天在开开心心地改进代码, 突然接到老板的一个电话说要改之前的一个程序. 怎么办? 虽然还需要很久时间才能改进完自己的代码, 可我有强迫症, 又不想把要改的程序和自己改进代码的部分一起 `commit` 了.

这时 `stash` 就是我的救星了. 用 `stash` 能先将我的那改进的部分放在一边分隔开来. 再另外单独处理老板的任务.

### 暂存修改 

假设我们现在在 `dev` 分支上快乐地改代码:

```
$ git checkout dev
```

在 `dev` 中的 `1.py` 中加上一行 `# feel happy`, 然后老板的电话来了, 可是我还没有改进完这些代码. 所以我就用 `stash` 将这些改变暂时放一边.

```
$ git status -s
# 输出
 M 1.py
------------------ 
$ git stash
# 输出
Saved working directory and index state WIP on dev: f7d2e3a change 3 in dev
HEAD is now at f7d2e3a change 3 in dev
-------------------
$ git status
# 输出
On branch dev
nothing to commit, working directory clean  # 干净得很
```

### 做其它任务 

然后我们建立另一个 `branch` 用来完成老板的任务:

```
$ git checkout -b boss

# 输出
Switched to a new branch 'boss' # 创建并切换到 boss
```

然后苦逼地完成着老板的任务, 比如添加 `# lovely boss` 去 `1.py`. 然后 `commit`, 完成老板的任务.

```
$ git commit -am "job from boss"
$ git checkout master
$ git merge --no-ff -m "merged boss job" boss
```

`merge` 如果有冲突的话, 可以像[上次那样](https://morvanzhou.github.io/tutorials/others/git/4-2-merge-conflict/) 解决.

```
a = 1
# I went back to change 1
<<<<<<< HEAD

# edited in master and dev

=======
# edited in dev

# lovely boss
>>>>>>> boss
```

通过以下步骤来完成老板的任务, 并观看一下 `master` 的 log:

```
$ git commit -am "solve conflict"
$ git log --oneline --graph
*   1536bea solve conflict
|\  
| * 27ba884 job from boss
* | 2d1961f change 4 in master
|/  
* f7d2e3a change 3 in dev
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```



### 恢复暂存 

轻松了, 现在可以继续开心的在 `dev` 上刷代码了.

```
$ git checkout dev
$ git stash list    # 查看在 stash 中的缓存

# 输出
stash@{0}: WIP on dev: f7d2e3a change 3 in dev
```

上面说明在 `dev` 中, 我们的确有 `stash` 的工作. 现在可以通过 `pop` 来提取这个并继续工作了.

```
$ git stash pop

# 输出
On branch dev
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   1.py

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (23332b7edc105a579b09b127336240a45756a91c)
----------------------
$ git status -s
# 输出
 M 1.py     # 和最开始一样了
```


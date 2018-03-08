---
layout: post
title: Send instant messages on linux server
author: CY
description: "Send messages on linux server"
tags: [Linux]
categories: [Linux]
share: false
image:
  background: triangular.png
---



Today I learned a new skill -- send instant messages to all/specific users via linux server

the usage of write and talk

## Write
在局域网络内很多时候是许多人共用一些机器，但如果多个人同时在使用同一台机器必定会发生一些冲突，比如系统的某些配置被修改，这样引起一些麻烦。那么如果在使用该机器之前，先给登录到该机器的所有其他用户发送一个消息，告诉其他用户（如果已经登录）你将使用该机器。这样如果有其他用户登录到该机器，他们就会收到该信息。这样能有效的避免一些冲突。

### 给指定用户发送消息
首先，可使用w或who命令查看当前登录的用户信息；然后，使用write命令将信息发送到用户的终端上，用法步骤如下：

```
1、write + shh登陆用户名+ttyname(例如pts/1)
2、ENTER
3、输入信息（所要发送的消息，中文可能会乱码）。
4、结束信息ctrl+d
```

example:

```
root# write root pts/1
I'll come by at 12:00 to look at your problem.
root#
```

然后使用root账号登录，且tty号为pts/1的登录用户终端会收到如下消息：

```
Message from root@cs2c.com.cn on pts/3 at 10:20 ...
I'll come by at 12:00 to look at you problem.
EOF
```

### 给所有用户发送消息
给当前登录所有用户发送消息，使用wall（write all的缩写）
首先，你可以通过who命令查看登录到该机器的所有用户。比如：

```
# who
root pts/0 Jun 13 04:28 (10.56.226.25)
root pts/1 Jun 13 22:32 (10.140.1.37)
root pts/2 Jun 13 23:31 (10.140.2.70)
root pts/3 Jun 13 23:56 (10.140.2.70)
```

表示有三个用户登录到该机器，有个用户有两个登录Console。
广播消息:

```
#wall 'I will use this host. If somebody is using it, pls let me know. Thanks a lot.'
Broadcast message from root (pts/3) (Fri Jun 13 23:57:13 2008):
I will use this host. If somebody is using it, pls let me know. Thanks a lot.
```

执行wall命令，所有登录到该机器的控制台(console)界面上都会收到如上所示的消息。

## Talk
Linux talk命令用于与其他使用者对谈。

```
talk person [ttyname]
person: 预备对谈的使用者帐号，如果该使用者在其他机器上，则可输入 person@machine.name
ttyname: 如果使用者同时有两个以上的 tty 连线，可以自行选择合适的 tty 传讯息
```
	user只有一个连线：talk user
	接下来就是等user回应，若user接受，则user输入 `talk cy`即可开始对谈，结束请按 ctrl+c
	多个连线，选一个tty： talk user@linux pts/1
	接下来就是等user回应，若user接受，则user输入 `talk cy@linux.home`即可开始对谈，结束请按 ctrl+c



## References

[Linux给指定用户或全部用户（已登录）发送消息](http://www.cnblogs.com/gaojun/p/3387427.html)
[Linux talk命令](http://www.runoob.com/linux/linux-comm-talk.html)
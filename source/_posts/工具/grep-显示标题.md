---
title: grep 显示标题
date: 2018-11-14 21:39:24
categories: 工具
tags:
  - Linux
---
# grep 显示标题

我们使用 `grep` 获取信息时，结果会丢失标题。

```shell
$ ps aux | head -1; ps aux | grep nginx
deploy   25879  0.0  0.0   9000   376 pts/0    R+   18:38   0:00 grep --color=auto nginx
root     32065  0.0  0.0  36836  5932 ?        Ss   Nov10   0:00 nginx: master process nginx -g daemon off;
systemd+ 32128  0.0  0.0  37340  3840 ?        S    Nov10   0:00 nginx: worker process
```

`Google` 一下可以找到一个方法：

先用命令本身加 `head -1` 取到标题，然后再使用该命令输出内容，两者叠加输出即得到所要结果。

```shell
$ ps aux | head -1; ps aux | grep nginx
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
deploy   25879  0.0  0.0   9000   376 pts/0    R+   18:38   0:00 grep --color=auto nginx
root     32065  0.0  0.0  36836  5932 ?        Ss   Nov10   0:00 nginx: master process nginx -g daemon off;
systemd+ 32128  0.0  0.0  37340  3840 ?        S    Nov10   0:00 nginx: worker process
```

这种方法似乎就是我们想要的解决方案了，但是问题是命令要运行 2 次。

我们回想一下 `grep` 的本质是什么？它其实是使用正则表达式去获取信息。

以上面的命令为例，丢失标题问题的本质是因为我们使用时，告诉 `grep` 去查找包含 `nginx` 的信息，而标题里面并没有 `nginx`。

想清楚了这一点，那么只要我们同时匹配标题的一部分，只运行 `1` 次命令，也可以实现同样的效果。

```shell
$ ps aux | grep -E 'PID|nginx'
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
deploy   25879  0.0  0.0   9000   376 pts/0    R+   18:38   0:00 grep --color=auto nginx
root     32065  0.0  0.0  36836  5932 ?        Ss   Nov10   0:00 nginx: master process nginx -g daemon off;
systemd+ 32128  0.0  0.0  37340  3840 ?        S    Nov10   0:00 nginx: worker process
```
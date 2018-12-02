---
title: Nginx 进程结构
date: 2018-12-02 10:24:48
categories: 工具
tags:
  - Nginx
---
# Nginx 进程结构

## 进程结构

一般来说 Nginx 有一个父进程 Master，和一个或多个子进程。

子进程分两类，一种是 Worker 进程，另一种是 Cache 相关的进程。

Cache 在多个 Worker 间共享使用。同时被进程 Cache manager 和 Cache loader 使用。Cache loader 做缓存的载入，Cache manager 做缓存的管理。这些进程间的通讯都是使用共享内存来解决的。

为什么不用多线程？因为线程之间是共享地址空间的，当某一个第三方模块引发了地址空间的段错误时，地址越界出现时，会导致整个进程挂掉。

Nginx 希望每个 Worker 进程从头到尾占有一个 CPU，所以往往不止要把 Worker 进程的数量配置与服务器的 CPU 核数一致以外，还需要把每一个 Worker 进程与某一个 CPU 核绑定在一起。这样可以更好的每个 CPU 核上面的 CPU 缓存来减少缓存失效的命中率。

不仅仅是缓存的原因，一个进程从头到尾占有一个 CPU，减少 CPU 上下文切换的次数和耗时，让 CPU 更多的时间用在运行进程上。

### Master 进程

监控 Worker 进程，接受信号

- CHLD，子进程终止的时候会向父进程发送 CHLD。Master 进程通过这个信号维持 Worker 进程的数量。

管理 Worker 进程，发送信号

- TERM/INT，立刻停止进程。
- QUIT，优雅的退出，等请求处理完才退出，用户无感知。
- HUP，重载配置文件。
- USR1，重新打开日志文件，做日志文件的切割。

下面 2 个信号，Nginx 命令行中没有对应的操作，只能通过 kill 直接向 Master 进程发送

- USR2，平滑升级，此时旧的 Nginx 主进程 Master 将会把自己的进程文件改名为 .oldbin，然后执行新版 Nginx。新旧 Nginx 会同时运行，共同处理请求。
- WINCH，平滑升级，逐步停止旧版 Nginx 的 Worker 进程就都会随着任务执行完毕而退出，新版的 Nginx 的 Worker 进程会逐渐取代旧版 Worker 进程。

### Worker 进程

和上面对应，接受信号

- TERM/INT
- QUIT
- USR1
- WINCH

### Nginx 命令行

启动 Nginx 以后，Nginx 会把 Master 进程的 pid 记录到一个文件中，一般是 Nginx 安装目录下 logs/nginx.pid。

我们平时使用的命令行其实就是对这个 pid 发送对应的信号。

- reload: HUP
- reopen: USR1
- stop: TERM
- quit: QUIT
---
title: Go 语言的 goroutine
date: 2019-03-28 22:14:05
categories: 后端
tags:
  - Go
---
# Go 语言的 goroutine

`Go` 语言中，主 `goroutine` 中的代码执行完毕，当前程序就会立刻结束运行，无论其他 `goroutine` 是否正在运行。

```go
package main

import "fmt"

func main() {
  for i := 0; i < 10; i++ {
    go func() {
      fmt.Println(i)
    }()
  }
}
```

执行上面的代码，会发现在绝大部分情况下，是什么都没有输出的。

其他 `goroutine` 还没有执行到 `fmt.Println(i)` 时，主 `goroutine` 中的代码就执行完毕了，让当前程序立刻结束运行。

如何让其他 goroutine 先执行完呢？最简单的方法，是让主 `goroutine` 等待一下。

```go
package main

import (
  "fmt"
  "time"
)

func main() {
  for i := 0; i < 10; i++ {
    go func() {
      fmt.Println(i)
    }()
  }

  time.Sleep(time.Millisecond * 500)
}
```

问题解决了，但是，等待多久是合适的呢？这是一个新的问题。

这种情况，我们应该用 `sync.WaitGroup`。

```go
package main

import (
  "fmt"
  "sync"
)

var waitgroup sync.WaitGroup

func main() {
  for i := 0; i < 10; i++ {
    waitgroup.Add(1)
    go func() {
      fmt.Println(i)
      waitgroup.Done()
    }()
  }

  waitgroup.Wait()
}
```

我们看到 `sync.WaitGroup` 解决了等待的问题，但是打印的全是 10，顺序不确定线程也不安全。

那么问题来了，如何让多个 `goroutine` 按顺序执行并且线程安全？

一般来说，我们使用锁解决这种问题，而自旋锁就是一种具体的实现。

```go
package main

import (
  "fmt"
  "sync"
)

var mu sync.Mutex

func main() {
  for i := 0; i < 10; i++ {
    mu.Lock()
    fun := func() {
      fmt.Println(i)
      defer mu.Unlock()
    }

    go fun()
  }
}
```

在 `GO` 语言中，通道是一种比锁更简单的实现。

```go
package main

import (
  "fmt"
)

func main() {
  message := make(chan int)

  for i := 0; i < 10; i++ {
    go func() {
      message <- i
    }()

    fmt.Println(<-message)
  }
}
```

## 通道和锁

通道的能力是让数据流动起来，擅长的是数据流动的场景。

* 传递数据的所有权，即把某个数据发送给其他协程
* 分发任务，每个任务都是一个数据
* 交流异步结果，结果是一个数据

锁的能力是数据不动，某段时间只给一个协程访问数据的权限擅长数据位置固定的场景。

* 缓存
* 状态
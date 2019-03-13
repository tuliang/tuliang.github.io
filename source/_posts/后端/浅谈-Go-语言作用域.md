---
title: 浅谈 Go 语言作用域
date: 2019-03-13 20:46:08
categories: 后端
tags:
  - Go
---
# 浅谈 Go 语言作用域

```go
package main

import "fmt"

var block = "package"

func main() {
  block := "function"

  {
    // := 会声明一个新变量并且将其初始化
    block := "inner"
    fmt.Printf("The block is %s.\n", block)
  }

  fmt.Printf("The block is %s.\n", block)
}
```

输出

```shell
The block is inner.
The block is function.
```

在这里 `block := "inner"` 等价于 `var block = "inner"`，它声明了一个新变量并且将其初始化。

在 `{}` 这个代码块中新的变量 `block` 和`main` 中声明的 `block` 名称相同。

- 在 `{}` 这个代码块中，它的优先级更高。
- 它的作用范围只在 `{}` 这个代码块中。

```go
package main

import "fmt"

var block = "package"

func main() {
  block := "function"

  {
    // = 会覆盖 block
    block = "inner"
    fmt.Printf("The block is %s.\n", block)
  }

  fmt.Printf("The block is %s.\n", block)
}
```

输出

```shell
The block is inner.
The block is inner.
```

这种情况很好理解：在 `{}` 这个代码块中，使用 `=` 改变了变量 `block` 的值。
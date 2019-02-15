---
title: LeetCode 344. Reverse String
date: 2019-02-15 19:58:36
categories: 算法与数据结构
tags:
  - Go
  - 算法
---
# [LeetCode 344. Reverse String](https://leetcode.com/problems/reverse-string/)

> Easy

Write a function that reverses a string. The input string is given as an array of characters `char[]`.

Do not allocate extra space for another array, you must do this by **modifying the input array** [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with O(1) extra memory.

You may assume all the characters consist of [printable ascii characters](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

## Example 1

```code
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

## Example 2

```code
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

## Go Code

使用双索引技术，时间复杂度 `O(n/2)`。

```go
func reverseString(s []byte)  {
    var length int = len(s)

    if length <= 1 {
        return
    }

    var head int = 0
    var tail int = length-1

    for head < tail {
        s[head], s[tail] = s[tail], s[head]

        head++
        tail--
    }
}
```

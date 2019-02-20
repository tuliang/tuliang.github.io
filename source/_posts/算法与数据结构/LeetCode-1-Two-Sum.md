---
title: LeetCode 1. Two Sum
date: 2019-02-20 20:00:54
categories: 算法与数据结构
tags:
  - Go
  - 算法
---
# [LeetCode 1. Two Sum](https://leetcode.com/problems/two-sum/)

> Easy

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the same element twice.

## Example

```code
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Go Code

最容易理解的双循环穷举，时间复杂度 `O(n^2)`。

```go
func twoSum(nums []int, target int) []int {
    var length int = len(nums)

    var i int = 0

    for i < length {
        var j int = i+1

        for j < length {
            if target - nums[i] == nums[j] {
                return []int{i, j}
            }

            j++
        }

        i++
    }

    return nil
}
```

使用 HashMap 查找元素时间为 `O(1)` 的特性，时间复杂度 `O(2n)`。

```go
func twoSum(nums []int, target int) []int {
  length := len(nums)

  var m = map[int]int{}

  for i := 0; i < length; i++ {
    m[nums[i]] = i
  }

  for i := 0; i < length; i++ {
    index := target - nums[i]

    // 排除 i 和 m[index] 相等的情况
    if num, ok := m[index]; ok && i != num {
      return []int{i, num}
    }
  }

  return nil
}
```

进一步优化，时间复杂度 `O(n)`。

```go
func twoSum(nums []int, target int) []int {
    m := map[int]int{}

    for i, num := range(nums) {
        if index, ok := m[target - num]; ok {
            return []int{index, i}
        }

        m[num] = i
    }

  return nil
}
```
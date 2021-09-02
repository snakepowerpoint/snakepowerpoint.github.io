---
title: LeetCode 1. Two Sum
date: 2021-08-29 19:03:58
tags: [LeetCode, easy]
categories:
  - 程式
  - LeetCode
  - Array
---


### Description

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

一開始的思路是暴力解法，遍歷 ```nums``` 中每個數字，然後找該數字是否和後面的數字相加得到 ```target```，不過這個方法最差的情況應該會是 ```n!```，所以換個方式。

另一個想法是從減法的角度來解，並解透過 hash table 來記錄 ```nums``` 中所有元素的 index。做法如下：先建立一個 hash_table，然後遍歷 ```nums``` 中所有元素，計算當下元素和 ```target``` 的差，然後看 hash_table 裡面有沒有這個差，有的話，等於是得到答案：因為當前這個數字與 hash_table 裡的元素的和就是 ```target```，因此，只要返回當前元素的 index 以及 hash_table 中差值元素的 index 即可。

如果差不存在的話，則將目前的元素及其 index 存入 hash_table，繼續找下一個。

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hash_table = {}
        for i, num in enumerate(nums):
            diff = target - num
            if diff in hash_table.keys():
                return [hash_table[diff], i]
            hash_table[num] = i
            
```

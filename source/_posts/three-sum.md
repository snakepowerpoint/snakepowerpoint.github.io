---
title: LeetCode 15. 3Sum
date: 2021-09-01 23:03:49
mathjax: true
tags: [LeetCode, medium]
categories:
  - 程式
  - LeetCode
  - Array
---

### Description

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

題目是給定一串數列，找出所有3個為一組且不重複的 triplets，使得這3個數字的總合為0。

這題比較複雜，單純用暴力解的話，時間複雜度會是 $O(N^3)$

需要用到二個指針。


```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        if len(nums) < 3:
            return []
        
        nums.sort()
        n = len(nums)
        res = set()
        
        for i, v in enumerate(nums[:n-2]):
            # if nums[i] = nums[i-1], no need to check
            if i >= 1 and nums[i] == nums[i-1]:
                continue
            
            d = {}
            for x in nums[(i+1):]:
                if x not in d:
                    d[-v-x] = 1
                else:
                    res.add((v, -v-x, x))
        return res        
```


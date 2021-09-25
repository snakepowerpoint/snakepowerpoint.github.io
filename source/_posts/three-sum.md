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

Given an integer array nums, return all the triplets ```[nums[i], nums[j], nums[k]]``` such that ```i != j, i != k```, and ```j != k```, and ```nums[i] + nums[j] + nums[k] == 0```.

Notice that the solution set must not contain duplicate triplets.

題目是給定一串數列，找出所有3個為一組且不重複的 triplets，使得這3個數字的總合為0。

這題的解法比較複雜，首先，最簡單的做法是暴力解，需要考慮 ```nums``` 中所有可能的 triplets，時間複雜度會是 $O(N^3)$。

第二種解法需要用到二個指針的操作，並且假設 ```nums``` 是已經排序過的。針對一個已經排序的 ```nums```，例如題目給的例子是 ```[-1,0,1,2,-1,-4]```，排序後為 ```[-4,-1,-1,0,1,2]```，目標是要在這裡面找到 a, b, c 三個數字，使得 a + b + c = 0。因為 ```nums``` 已經排序過，我們可以假設 a < b < c，先把 a 當成第一個數字，也就是 -4，接下來要找的 b 和 c 必須符合 b + c = -4。找法是先放二個指針，一個在頭，一個在尾，例如 b = -1, c = 2，然後把它們相加，如果和比 a 小，表示 b 要往右邊移動去找更大的數字（因為 ```nums``` 已經排序）；反之，如果和比 a 大，那麼 c 就要往左移動，去找更小的數字。

另一種解法和前述雙指針的解法類似，一樣先將 ```nums``` 排序，接著從第一個數開始，依序當作 triplets 中的一個數值 v，然後從剩下的數去找 triplets 中的另外二個數字。假設另外二個數值其中一個是 x，則另一個一定是 -v-x，三者相加 v + x + (-v-x) = 0。重複前面的步驟，遍歷 ```nums``` 中所有的數字，就能得到所有的 triplets。


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

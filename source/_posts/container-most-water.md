---
title: LeetCode 11. Container With Most Water
date: 2021-10-19 23:58:18
tags: [LeetCode, medium]
categories:
  - 程式
  - LeetCode
  - Pointer
---

### Description

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of the line i is at (i, ai) and (i, 0). Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

Notice that you may not slant the container.

Example 1:

> Input: height = [1,8,6,2,5,4,8,3,7]
> Output: 49
> Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.


<!--more-->

解題思路：

暴力解法是用 for 迴圈遍歷任二條線所圍出來的面積，結果可能會受到時間限制無法通過測試。

另一種解法是雙指針搭配貪婪演算法。首先把指針放在左右端點，然後計算這二個端點所圍出來的面積，並更新目前記錄到的最大面積。接著，剔除高度比較矮的那個端點，把指針往對應的方向往前移動一格，例如左邊指針對應的高度比右邊指針對應的高度矮的話，則左邊的指針往右邊移動一格。

重複上述的動作，每次都紀錄最大的面積，然後再踢掉最矮的那條線，去找更高的線來圍出更大的面積，直到二個指針相遇。


```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        ans = 0
        l = 0
        r = len(height) - 1
        while l < r:
            ans = max(ans, (r - l) * min(height[l], height[r]))
            
            if height[l] <= height[r]:
                l += 1
            else:
                r -= 1
        
        return ans 
```
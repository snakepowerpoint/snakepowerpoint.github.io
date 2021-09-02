---
title: LeetCode 3. Longest Substring Without Repeating Characters
date: 2021-09-01 00:31:01
tags: [LeetCode, medium]
categories:
  - 程式
  - LeetCode
  - Array
---

Given a string s, find the length of the longest substring without repeating characters.

本題主要測驗 string 的操作，如 slicing 及找尋 substring。解法是依序建立 substring，當遇到有重複的字元時，拿掉該字元以前的所有字元，從該重複字元的下一個開始，並且新增當前的字元。依此類推，當遇到比較長的 substring 時，更新 substring 的長度。全部跑完就能得到最長的 substring。


```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s:
            return 0
        
        ans = 0
        subs = ''
        for x in s:
            if x in subs:
                if ans < len(subs):
                    ans = len(subs)
                
                pos = subs.find(x) + 1
                subs = subs[pos:] + x
            else:
                subs += x
        
        if ans < len(subs):
            ans = len(subs)
        return ans
```
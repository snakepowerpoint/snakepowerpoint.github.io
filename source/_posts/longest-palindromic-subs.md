---
title: LeetCode 5. Longest Palindromic Substring
date: 2021-09-01 21:45:58
tags: [LeetCode, medium]
categories:
  - 程式
  - LeetCode
  - Array
---

### Description

Given a string s, return the longest palindromic substring in s.

本題主要考 string 操作。想法上先建一個 helper function 來找回文的 substring，然後從 string 頭開始，依序帶入 substring 去找回文，並在過程中儲存目前長度最長的 substring，最後便可找到答案。

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        if n == 1:
            return s
        
        ans = ''
        max_len = 0
        for i in range(n):
            subs = self.find_palindrome(s[i:])
                        
            if len(subs) > max_len:
                max_len = len(subs)
                ans = subs
        return ans
    
    def find_palindrome(self, s: str):
        res = ''
        end = -1
        while True:
            end = s.find(s[0], end+1)
            if end == -1:
                break
            subs = s[:(end+1)]
            if subs == subs[::-1]:
                res = subs
        
        return res
```
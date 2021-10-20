---
title: LeetCode 17. Letter Combinations of a Phone Number
date: 2021-09-28 21:49:21
tags: [LeetCode, medium]
categories:
  - 程式
  - LeetCode
  - Search
---

### Description

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example 1

> Input: digits = "23"
> Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]


<!--more-->

題目給定一組數字和英文字母的對照表，問一組 digits 中，所有可能的字母組合，例如 2 和 3 分別對應 abc 及 def，則 ```23``` 所有可能的組合就是 ```["ad","ae","af","bd","be","bf","cd","ce","cf"]```。

這是一個滿好的練習題，可以練習到很多演算法的基本觀念，包括遞迴、DFS (depth-first search)、對各種資料結構的基本操作等。

本題的解法是透過 tree 做 search，概念上可以想像成先將 digits 中所有數字放到 tree 的各階層，例如 ```23``` 有二個數字，2 放 root，3 放第一層。其中，2 有 a, b, c 三種可能性，所以在 tree 上 2 有三個 branch，分別接到三個同為 3 的 node，每個 branch 分別代表 a, b, c。同理，3 有 d, e, f 三種可能性，所以這三個 node 各自再接出三個 branch 出來，形成九個 leaf，這九個 leaf 就是 ```23``` 這個 digits 所有可能的字母組合。

其中一個解法是 DFS，從 root 開始，先往左直接探到最深層的 leaf，得到一組答案後，往回一個 node，重複上述的操作，最後就能得到所有的 leaf。

具體來說，先定義好各個 digits 對應的字母，在樹狀結構下，每一層數字有其對應的字母，如果用 DFS 來解的話，會直探最後一個 digits 對應的所有字母，然後回到上一層的第二個字母，再去配對最後一層所有的字母。這裡透過 ```cur``` 紀錄當前深度下的數字所對應的字母，```l``` 表示當前層數，將所有資訊輸入遞迴函數 ```dfs``` 中。

遞迴函數 ```dfs``` 一開始會先判斷遞迴的中斷條件，如未滿足，則繼續跑遞迴的主邏輯區塊。一旦中斷條件滿足，```dfs``` 就會把目前所有的字母組合在一起，然後加到結果 ```ans``` 中。持續重複以上動作，最後就能得到答案。


```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        
        mapping = ["", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"]
        cur = ['' for _ in range(len(digits))]
        ans = []
        self.dfs(digits, cur, 0, mapping, ans)  # start recursive
        return ans

    def dfs(self, digits, cur, l, mapping, ans):
        if l == len(digits):  # condition to stop recursive
            if l > 0:
                ans.append("".join(cur))
            return

        for c in mapping[int(digits[l])]:  # main recursive
            cur[l] = c
            self.dfs(digits, cur, l+1, mapping, ans)
```
---
title: LeetCode 983. Minimum Cost For Tickets
date: 2021-09-03 00:15:25
tags: [LeetCode, medium]
categories:
  - 程式
  - LeetCode
  - Array
---

### Description
You have planned some train traveling one year in advance. The days of the year in which you will travel are given as an integer array days. Each day is an integer from 1 to 365.

Train tickets are sold in three different ways:

- a 1-day pass is sold for costs[0] dollars,
- a 7-day pass is sold for costs[1] dollars, and
- a 30-day pass is sold for costs[2] dollars.

The passes allow that many days of consecutive travel.

- For example, if we get a 7-day pass on day 2, then we can travel for 7 days: 2, 3, 4, 5, 6, 7, and 8.

Return the minimum number of dollars you need to travel every day in the given list of days.


這是我第一次碰到 dynamic programming (DP) 問題，其實最早碰到的應該是費布納西數列，不過那個問題相對簡單。

本題考 DP 觀念，想法上是第 i 天的花費，是截至第 i-1 天的花費再加上當天的花費。因此，如果第 i 天不用旅遊的話，那該天的花費就是累積到第 i-1 天的花費。反之，如果第 i 天要旅遊的話，那麼有三種情況，分別是第 i-1 天加上 1-day pass、第 i-7 天加上 7-day pass、第 i-30 天加上 30-day pass。透過這種推法，就能導出每個 travel day 的最低花費。要注意的是，起始值 DP(0) 要給一個合理的數字，才能透過 DP 演算法一直往下推 DP(1), DP(2), ..., DP(t)。本題把 DP(0) 設為 0 （花費為 0）是個合理的設定。


```python
class Solution:
    def mincostTickets(self, days: List[int], costs: List[int]) -> int:
        dp = [float("inf")] * 366
        for day in days:
            dp[day] = 0
        
        # set initial point
        dp[0] = 0
        for i in range(1, 366):
            if dp[i] == float("inf"):
                dp[i] = dp[i-1]
            else:
                case1 = dp[max(i-1, 0)] + costs[0]
                case2 = dp[max(i-7, 0)] + costs[1]
                case3 = dp[max(i-30, 0)] + costs[2]
                
                dp[i] = min(case1, case2, case3)
        
        return dp[days[-1]]
```
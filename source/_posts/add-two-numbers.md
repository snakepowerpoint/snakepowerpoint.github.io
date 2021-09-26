---
title: LeetCode 2. Add Two Numbers
date: 2021-08-30 00:30:07
tags: [LeetCode, medium]
categories:
  - 程式
  - LeetCode
  - Array
---

### Description

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

這題主要測驗的是 ```Linked list``` 的操作，以及餘數的處理。首先新增一個空的 ```List```，並新建一個餘數。接著，遍歷 ```l1``` 及 ```l2```，當有述職的時候，就按照位置相加，並且更新餘數，直到 ```l1``` 及 ```l2``` 都沒有 ```next```。

<!--more-->

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        head = ans = ListNode()
        remainder = 0
        while l1 or l2 or remainder:
            l1_val = l1.val if l1 is not None else 0
            l2_val = l2.val if l2 is not None else 0
            
            summation = l1_val + l2_val + remainder
            remainder = summation // 10
            
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
            ans.next = ListNode(summation % 10)
            ans = ans.next
        
        return head.next
```
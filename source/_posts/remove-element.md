---
title: LeetCode 27. Remove element
tags: [LeetCode, easy]
categories:
  - 程式
  - LeetCode
  - Array
date: 2021-08-29 16:17:37
---


### Description

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

題目並不難，大意是給定一個含有整數的陣列 ```nums``` 及一個整數 ```val```，要把 ```nums``` 中所有的 ```val``` 都刪掉，然後返回剩餘陣列的長度。條件是必須在 O(1) 的記憶體實現。

在 python 中，可以透過 ```list.remove(val)``` 刪除 ```list``` 中的 ```val```。由於 ```list.remove()``` 只能刪除第一個出現的 ```val```，因此，透過 while 迴圈來刪除所有 ```val```，同時透過 has_element 這個 tag 來判斷 ```nums``` 中是否還有 ```val```，如果已經全部刪除的話，則結束迴圈。

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        if not nums:
            return
        
        has_element = True
        while has_element:
            try:
                nums.remove(val)
            except ValueError:
                has_element = False
        return len(nums)
```
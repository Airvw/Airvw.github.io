---
layout: post
title: "3sum(python)"
tags:
  - [algorithm]
  - [leetcode]
  - [투 포인터]
  - [python]
---

## 참고 자료

[leetcode - 3sum](https://leetcode.com/problems/3sum/)  
파이썬 알고리즘 인터뷰

## 문제 설명

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0?  
Find all unique triplets in the array which gives the sum of zero.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

```python
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

**Example 2:**

```python
Input: nums = []
Output: []
```

**Example 3:**

```python
Input: nums = [0]
Output: []
```

**Constraints:**

- 0 <= nums.length <= 3000
- -10<sup>5</sup> <= nums[i] <= 10<sup>5</sup>

## 나의 생각

## 코드

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        answer = []
        if len(nums) < 3:
            return answer
        nums.sort()
        for i in range(len(nums) - 2):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            left, right = i + 1, len(nums) - 1
            while left < right:
                total = nums[i] + nums[left] + nums[right]
                if total < 0:
                    left += 1
                elif total > 0:
                    right -= 1
                else:
                    answer.append([nums[i], nums[left], nums[right]])
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1
                    left += 1
                    right -= 1

        return answer
```

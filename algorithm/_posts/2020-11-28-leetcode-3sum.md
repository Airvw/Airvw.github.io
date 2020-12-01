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

투 포인터가 생각이 났다.  
for문을 통해서 처음 인덱스 i를 고르고, left는 i + 1에서 시작하고, right은 left + 1로 시작해서   
sum이 0보다 크거나 작을 때 left, right을 조절해야 겠다고 생각했고, 정렬이 필요하다고 생각했다.   
하지만 중복이 발생하는 경우를 제대로 생각하지 못했다.  


## 코드

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        answer = []
        if len(nums) < 3:
            return answer
        nums.sort()
        for i in range(len(nums) - 2):
            #  중복이 발생하는 경우
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
                    # left가 중복인 경우
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    # right이 중복인 경우
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1
                    # 합이 0이 되는 또 다른 경우 탐색
                    left += 1
                    right -= 1

        return answer
```

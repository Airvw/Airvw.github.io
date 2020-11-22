---
layout: post
title: "Two Sum(python)"
tags:
  - [algorithm]
  - [leetcode]
  - [완전 탐색]
  - [python]
---

## 참고 자료

[leetcode - Two Sum](https://leetcode.com/problems/two-sum/)  
파이썬 알고리즘 인터뷰

## 문제 설명

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

**Example 1:**

```python
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```python
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**

```python
Input: nums = [3,3], target = 6
Output: [0,1]
```

**Constraints:**

- 2 <= nums.length <= 10^3^
- -10^9^ <= nums[i] <= 10^9^
- -10^9^ <= target <= 10^9^
- Only one valid answer exists.

## 나의 생각

target보다 큰 수가 있으면 스킵을 하기 위해서 정렬을 하고, 작은 수 부터 차례대로 계산하려고 했다.  
하지만 이전의 인덱스를 기억해야 하므로 정렬은 포기했다.  
이후 이중 for문을 돌면서 target 값에서 두 수를 빼서 0이 되는 경우를 찾으려고 했다.

## 코드

- 제일 비효율적인 방법

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums) - 1):
            t = target - nums[i]
            for j in range(i + 1, len(nums)):
                if t - nums[j] == 0:
                    return [i, j]
```

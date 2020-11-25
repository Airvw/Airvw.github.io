---
layout: post
title: "Array Partition i(python)"
tags:
  - [algorithm]
  - [leetcode]
  - [python]
---

## 참고 자료

[leetcode - Array Partition I](https://leetcode.com/problems/array-partition-i/)  
파이썬 알고리즘 인터뷰

## 문제 설명

Given an integer array nums of 2n integers, group these integers into n pairs (a1, b1), (a2, b2), ..., (an, bn) such that the sum of min(ai, bi) for all i is maximized.  
Return the maximized sum.

**Example 1:**

```
Input: nums = [1,4,3,2]
Output: 4
Explanation: All possible pairings (ignoring the ordering of elements) are:

1. (1, 4), (2, 3) -> min(1, 4) + min(2, 3) = 1 + 2 = 3
2. (1, 3), (2, 4) -> min(1, 3) + min(2, 4) = 1 + 2 = 3
3. (1, 2), (3, 4) -> min(1, 2) + min(3, 4) = 1 + 3 = 4
   So the maximum possible sum is 4.
```

**Example 2:**

```python
Input: nums = [6,2,6,5,1,2]
Output: 9
Explanation: The optimal pairing is (2, 1), (2, 5), (6, 6). min(2, 1) + min(2, 5) + min(6, 6) = 1 + 2 + 6 = 9.
```

**Constraints:**

- 1 <= n <= 10<sup>4</sup>
- nums.length == 2 \* n
- -10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>

## 나의 생각

가장 작은 수끼리 짝을 지어주는게 제일 좋다고 생각해서 정렬을 사용했다.

## 코드

- 생각과 같은 코드

```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        answer = 0
        nums.sort()
        pair = []
        for i in nums:
            pair.append(i)
            if len(pair) == 2:
                answer += min(pair)
                pair = []
        return answer
```

- 2개 페어이므로, 정렬했을 때 짝수 값만 더하면 된다.

```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        answer = 0
        nums.sort()
        for i, num in enumerate(nums):
            if i % 2 == 0:
                answer += num

        return answer
```

- 파이썬 다운 방식

```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        return sum(sorted(nums[::2]))
```

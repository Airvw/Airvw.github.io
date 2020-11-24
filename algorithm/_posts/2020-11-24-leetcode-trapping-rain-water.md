---
layout: post
title: "Trapping Rain Water(python)"
tags:
  - [algorithm]
  - [leetcode]
  - [투 포인터]
  - [python]
---

## 참고 자료

[leetcode - Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)  
파이썬 알고리즘 인터뷰

## 문제 설명

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

**Example 1:**
![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9
```

**Constraints:**

- n == height.length
- 0 <= n <= 3 \* 10<sup>4</sup>
- 0 <= height[i] <= 10<sup>5</sup>

## 나의 생각

이전 코딩 테스트에 비슷한 문제가 나왔는데, 완전 탐색을 시도했지만 시간초과가 나서 실패했다.  
아직도 완전 탐색밖에 생각이 안나는 문제.

## 솔루션

최대 높이의 막대까지 각각 좌우 기둥 최대 높이가 현재 높이와의 차이만큼 물을 채워넣으면 된다.  
각각의 높이를 비교해서 거리를 좁히면 최대 높이의 막대까지 비교하게 된다.

## 코드

- 투 포인터 사용.

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        if not height:
            return 0

        volume = 0
        left, right = 0, len(height) - 1
        left_max, right_max = height[left], height[right]

        while left < right:
            left_max, right_max = max(left_max, height[left]), max(right_max, height[right])

            if left_max <= right_max:
                volume += left_max - height[left]
                left += 1
            else:
                volume += right_max - height[right]
                right -= 1

        return volume
```

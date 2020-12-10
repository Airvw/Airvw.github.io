---
layout: post
title: "Binary Search(python)"
tags:
  - [algorithm]
  - [python]
---

## 이진 탐색

이진 탐색은 O(logN)으로 선형 탐색 O(n)보다 빠르다.  
단, 이진 탐색은 정렬되어 있어야 한다.

코드를 보지 않고 처음부터 작성해보자~!

## 이진 탐색 구현 코드

- 반복문 사용.

```python
def solution(nums, x):
    answer = -1
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if x == nums[mid]:
            answer = mid
            return answer
        elif:
            x < nums[mid]:
            right = mid - 1
        else:
            left = mid + 1
    return answer
```

- 재귀 사용.

```python
def solution(nums, x, left, right):
    if left > right:
        return -1

    mid = (left + right) // 2
    if x == nums[mid]:
        return mid
    elif x < nums[mid]:
        return solution(nums, x, left, mid - 1)
    else:
        return solution(nums, x, mid + 1, right)

```

---
layout: post
title: "Product of Array Except Self(python)"
tags:
  - [algorithm]
  - [leetcode]
  - [python]
---

## 참고 자료
[leetcode - Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)  
파이썬 알고리즘 인터뷰

## 문제 설명

Given an array nums of n integers where n > 1,  return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

**Example:**

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

**Constraint:**
 It's guaranteed that the product of the elements of any prefix or suffix of the array (including the whole array) fits in a 32 bit integer.


**Note:**
Please solve it without division and in O(n).

**Follow up:**
Could you solve it with constant space complexity? (The output array does not count as extra space for the purpose of space complexity analysis.)

## 나의 생각 
O(n<sup>2</sup>)을 이용한 이중 for문, sum()과 나누기를 이용한 방법밖에 생각나지 않았다.  

## 솔루션

자기 자신을 제외한 왼쪽의 값들을 곱한 값들의 배열을 만들고,
자기 자신을 제외한 오른쪽의 값들을 곱한 값들의 배열을 만든다.
이 두 배열 각 인덱스를 곱하면 자기 자신을 제외한 값들의 곱을 알 수 있다.

p = 1로 초기화하여 자기 자신을 제외한 왼쪽 값들을 곱해서 배열로 만든다는 점에서 참신했다.  

## 코드

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        #  자기 자신을 제외한 왼쪽 값들을 곱한 배열
        p = 1
        answer = []
        for i in range(len(nums)):
            answer.append(p)
            p *= nums[i]
        
        # 자기 자신을 제외한 오른쪽 값들을 곱한 배열
        p = 1
        for i in range(len(nums) - 1, -1, -1):
            answer[i] = answer[i] * p
            p *= nums[i]
        
        return answer
```
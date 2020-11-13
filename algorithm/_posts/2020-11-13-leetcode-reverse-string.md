---
layout: post
title: "Reverse String(python)"
tags:
  - [algorithm]
  - [leetcode]
  - [투 포인터]
  - [python]
---

## 참고 자료

파이썬 알고리즘 인터뷰
[leetcode - Reverse String](https://leetcode.com/problems/reverse-string/)

## 문제

Write a function that reverses a string. The input string is given as an array of characters char[].

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

You may assume all the characters consist of printable ascii characters.

**Example 1:**

```python
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Example 2:**

```python
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

## 나의 생각

단순하게 s.reverse() 함수를 사용해야겠다고 생각했다.  
투 포인터를 생각하지 못했다.  
재귀도 생각하지 못했다.

## 코드

- s.reverse() 사용.

```python
class Solution:
    def reverseString(self, s):
        s.reverse()
```

- 투 포인터 사용.

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        left, right = 0, len(s) - 1
        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1

```

- 재귀와 투 포인터 사용

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        def helper(left, right):
            if left < right:
                s[left], s[right] = s[right], s[left]
                helper(left + 1, right - 1)
        helper(0, len(s) - 1)
```

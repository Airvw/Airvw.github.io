---
layout: post
title: "Longest Palindromic Substring(python)"
tags:
  - [algorithm]
  - [leetcode]
  - [투 포인터]
  - [python]
---

## 참고 자료

[leetcode - Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)  
파이썬 알고리즘 인터뷰

## 문제 설명

Given a string s, return the longest palindromic substring in s.

**Example 1:**

```python
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```python
Input: s = "cbbd"
Output: "bb"
```

**Example 3:**

```python
Input: s = "a"
Output: "a"
```

**Example 4:**

```python
Input: s = "ac"
Output: "a"
```

**Constraints:**

- 1 <= s.length <= 1000
- s consist of only digits and English letters (lower-case and/or upper-case),

## 나의 생각

이전 [leetcode - Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)을 푼 기억을 생각해서 투 포인터를 생각했다.  
하지만 투 포인터를 어떻게 설정해야 될지 감이 잡히질 않았다.

## 솔루션

팰린드롬은 `bb`처럼 짝수일 때가 있고, `bab`처럼 홀수일 때가 있다.  
따라서 짝수나 홀수 모든 경우에 대해 판별해야한다.  
for문 반복문을 사용해서 left을 설정하고,  
left를 중앙으로 팰린드롬이 홀수인 경우(+ 1), 짝수인 경우(+2)를 통해 가장 긴 팬린드롬을 찾는다.  
expend는 2칸씩 확장되므로 시작이 홀수인지 짝수인지에 따라 홀수, 짝수의 경우가 결정된다.  
left를 중앙으로 했을 때 홀수인 경우 left 하나만을 중심으로 right이 `left + 1`이 된 경우이므로 right - 1과 비교를 해야 된다.  
짝수인 경우 left와 left + 1이 중심이 된 경우이므로 right이 `lett + 1` + 1가 된 경우이므로 비교할 때 right - 1을 해서 비교해야 된다.

## 코드

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if len(s) < 2 or s == s[::-1]:
            return s
        def expand(left, right):
            while left >= 0 and right <= len(s) and s[left] == s[right - 1]:
                left -= 1
                right += 1
            return s[left + 1: right - 1]

        answer = ""
        for i in range(len(s) - 1):
            answer = max(answer, expand(i, i + 1), expand(i, i + 2), key = len)
        return answer
```

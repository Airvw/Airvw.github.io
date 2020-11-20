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

[leetcode - Group Anagrams](https://leetcode.com/problems/longest-palindromic-substring/)  
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

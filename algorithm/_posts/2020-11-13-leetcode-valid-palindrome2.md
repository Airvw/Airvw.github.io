---
layout: post
title: "Valid Palindrome2(python)"
tags:
  - [algorithm]
  - [leetcode]
  - [완전 탐색]
  - [정규 표현식]
  - [투 포인터]
  - [python]
---

## 참고 자료

파이썬 알고리즘 인터뷰  
[leetcode - Valid Palindrome](https://leetcode.com/problems/valid-palindrome-ii/)

## 문제

Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome.

**Example 1:**

```python
Input: "aba"
Output: True
```

**Example 2:**

```python
Input: "abca"
Output: True
Explanation: You could delete the character 'c'.
```

**Note:**

- The string will only contain lowercase characters a-z. The maximum length of the string is 50000.

## 나의 생각

`s != s[::-1]`일 때 slicing을 이용해서 완전 탐색을 생각했다.
투 포인터 생각 못했다.

## 코드

- 시간 초과..

```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        for i in range(len(s)):
                tmp = s[ : i] + s[i + 1:]
                if tmp == tmp[::-1]:
                    return True
        return s == s[::-1]
```

- 투 포인터 사용.

```python
    class Solution:
        def validPalindrome(self, s: str) -> bool:

            if s == s[::-1]:
                return True
            else:
                left, right = 0, len(s) - 1
                while left < right:
                    if s[left] == s[right]:
                        left += 1
                        right -= 1
                    else:
                        leftpart = s[: left] + s[left + 1:]
                        rightpart = s[: right] + s[right + 1:]
                        if leftpart == leftpart[::-1]:
                            return True
                        if rightpart == rightpart[::-1]:
                            return True

                        return False
                return True
```

- 재귀, 투 포인터 사용.

```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        return helper(s, 0)
    def helper(self, s, cnt):
        left, right = 0, len(s) - 1
        while left < right:
            if s[left] != s[right]:
                if cnt == 1:
                    return False
                return self.helper(s[left + 1: right + 1], cnt + 1) or self.helper(s[left : right], cnt + 1)
            else:
                left += 1
                right -= 1
            return True
```

- leetcode Approach #2: Greedy (탐욕법)
  왜 탐욕법인지 모르겠다. 오히려 투 포인터에 가까운듯..?

```python
class Solution(object):
    def validPalindrome(self, s):
        def is_pali_range(i, j):
            return all(s[k] == s[j-k+i] for k in range(i, j))

        for i in range(len(s) // 2):
            if s[i] != s[~i]:
                j = len(s) - 1 - i
                return is_pali_range(i+1, j) or is_pali_range(i, j-1)
        return True
```

## 새로 배운 것

- all(iterable) : python 내장 함수
  - iterable 내의 모든 요소가 참이거나 혹은 iterable 이 비어 있다면 True 를 반환하고, 그 외의 경우에는 False 를 반환하는 함수

```python
def all(iterable):
    for element in iterable:
     if not element:
        return False return True
```

- 예제

```python
print(all([]))
print(all([1, 2, 3, 4]))
print(all([0, 1, 2, 3]))
```

결과

```python
True
True
False
```

- `if s[i] != s[~i]:` 비트 연산자를 사용해서 반대 index에 접근한 부분이 신기했다.

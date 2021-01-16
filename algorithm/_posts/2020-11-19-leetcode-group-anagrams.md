---
layout: post
title: "Group Anagrams(python)"
tags:
  - [algorithm]
  - [leetcode]
  - [python]
---

## 참고 자료

[leetcode - Group Anagrams](https://leetcode.com/problems/group-anagrams/)   
파이썬 알고리즘 인터뷰

## 문제 설명

Given an array of strings strs, group the anagrams together.  
You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

```python
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

**Example 2:**

```python
Input: strs = [""]
Output: [[""]]
```

**Example 3:**

```python
Input: strs = ["a"]
Output: [["a"]]
```

**Constraints:**

- 1 <= strs.length <= 104
- 0 <= strs[i].length <= 100
- strs[i] consists of lower-case English letters.

## 나의 생각

같은 그룹의 단어는 알파벳이 같은 것을 알 수 있다.  
그래서 딕셔너리를 활용해서 알파벳의 개수를 계산해서 비교하면 어떨까 생각했다.  
하지만 각 딕셔너리를 어떻게 비교할지 몰라서 다른 방법을 생각했다.  
그 다음 단어의 정렬을 비교해서 그룹화를 생각했다.  
그룹화를 하기 위해서 딕셔너리밖에 생각이 안났고, key값을 어떻게 할지 고민했다.  
그룹의 공통적인 부분이 정렬된 문자열이 같다는 것을 알고 이것을 key값으로 했다.

## 코드

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        d = {}
        for str in strs:
            key = "".join(sorted(str))
            if key not in d:
                d[key] = [str]
            else:
                d[key].append(str)
        return d.values()
```

- defaultdict 사용.

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        anagrams = collections.defaultdict(list)
        for word in strs:
            anagrams["".join(sorted(word))].append(word)

        return anagrams.values()
```

- defaultdict, key로 tuple을 사용.

```python
class Solution(object):
    def groupAnagrams(self, strs):
        ans = collections.defaultdict(list)
        for s in strs:
            ans[tuple(sorted(s))].append(s)
        print(ans)
        return ans.values()
```

- 첫번째 생각인 알파벳의 개수로 비교하는 경우.

```python
class Solution:
    def groupAnagrams(strs):
        ans = collections.defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord('a')] += 1
            ans[tuple(count)].append(s)
        return ans.values()
```

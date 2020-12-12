---
layout: post
title: "Binary Search Tree(python)"
tags:
  - [자료구조]
  - [이진 탐색 트리]
  - [python]
---

## 이진 탐색 트리

**원칙**

- 모든 노드에 대해서 다음을 만족하는 이진 트리
  - 왼쪽 서브트리에 있는 데이터는 모두 현재 노드의 값보다 작다.
  - 오른쪽 서브트리에 있는 데이터는 모두 현재 노드의 값보다 크다.

**구조**

- 각 노드는 (key, value) 쌍의 데이터를 가진다.

## 배열을 이용한 이진 탐색 vs 이진 탐색 트리

이진 탐색 트리 **장점**

- 데이터 원소의 추가, 삭제가 용이(빠르다)

이진 탐색 트리 **단점**

- 공간 소요가 큼

## 코드 구현

```python
class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.left = None
        self.right = None


    def inorder(self):
        tarversal = []
        if self.left:
            tarversal += self.left.inorder()
        tarversal.append(self)
        if self.right:
            tarversal += self.right.inorder()
        return tarversal

    # 최소 값을 가지는 노드
    def min(self):
        if self.left:
            self.left.min()
        else:
            return self

    # 최대 값을 가지는 노드
    def max(self):
        if self.right:
            self.right.max()
        else:
            return self

    # 원하는 key 값을 가진 노드와 그 노드의 부모를 찾는 메소드
    def lookup(self, key, parent=None):
        if key < self.key:
            if self.left:
                return self.left.lookup(key, self)
            else:
                return None, None
        elif key > self.key:
            if self.right:
                return self.right.lookup(key, self)
            else:
                return None, None
        else:
            return self, parent

    # 트리에 원하는 key, value값을 가진 노드를 삽입
    def insert(self, key, value):
        if key < self.key:
            if self.left:
                return self.left.insert(key, value)
            else:
                self.left = Node(key, value)
        elif key > self.key:
            if self.right:
                return self.right.insert(key, value)
            else:
                self.right = Node(key, value)
        else:
            raise KeyError()

    # child 노드 개수를 세는 메소드
    def countChildren(self):
        cnt = 0
        if self.left:
            cnt += 1
        if self.right:
            cnt += 1
        return cnt


class BinSearchTree:
    def __init__(self):
        self.root = None

    def inorder(self):
        if self.root:
            return self.root.inorder()
        else:
            return []
    def min(self):
        if self.root:
            return self.root.min()
        else:
            return None

    def max(self):
        if self.root:
            return self.root.max()
        else:
            return None

    def lookup(self, key):
        if self.root:
            return self.root.lookup(key)
        else:
            return None, None

    def insert(self, key, value):
        if self.root:
            self.root.insert(key, value)
        else:
            self.root = Node(key, value)

    def remove(self, key):
        node, parent = self.lookup(key)
        if node:
            children = node.countChildren()
            # 자식 노드가 없는 경우
            if children == 0:
                if parent:
                    # 없애려는 노드가 부모의 왼쪽 노드인 경우
                    if parent.left == node:
                        parent.left = None
                     # 없애려는 노드가 부모의 오른쪽 노드인 경우
                    if parent.right == node:
                        parent.right = None
                # 부모가 없는 경우 -> root 노드인 경우
                else:
                    self.root = None
            # 자식 노드가 1개인 경우
            elif children == 1:
                if node.left:
                    tmp = node.left
                if node.right:
                    tmp = node.right

                # 부모 노드가 존재하는 경우
                if parent:
                    # 없애려는 노드가 부모의 왼쪽 노드인 경우
                    if parent.left == node:
                        parent.left = tmp
                    # 없애려는 노드가 부모의 오른쪽 노드인 경우
                    if parent.right == node:
                        parent.right = tmp
                # 부모 노드가 없는 경우
                else:
                    self.root = tmp

            # 자식 노드가 2개인 경우
            else:
                parent = node
                successor = node.right

                # 제거하려는 노드 다음으로 큰 노드를 찾는 과정
                while successor.left:
                    parent = successor
                    successor = successor.left

                # 제거하려는 노드에 제거하려는 노드 다음으로 큰 노드를 대입해서 제거
                node.key = successor.key
                node.value = successor.value

                # successor에 있는 자식 노드를 successor의 부모 노드와 연결하는 과정
                if parent.left == successor:
                    parent.left = successor.right
                # successor가 제거하려는 노드의 오른쪽 노드인 예외 상황.
                if parent.right == successor:
                    parent.right = successor.right
            return True
        else:
            return False

```

## 인상 깊은 부분

- lookup() 메소드에서 parent를 기억해서 remove() 메소드에서 활용하는 부분

## 오류 났던 부분

- successor를 통해서 제거하려는 노드 다음으로 큰 노드인 것은 알았지만, 기존의 노드를 successor로 대체하는 부분에서 제대로 이해하지 못했었고,  
  successor를 기존 node로 대체하는 경우 `parent.left = successor.right`, `parent.right = successor.right` 부분에서 successor.right 할당하는 것을  
  이해하지 못했었다. 이후 successor는 가장 작은 노드이기 때문에 successor의 자식은 없을 수도 있지만 있으면 오른쪽 자식 밖에 없다는 것을 알게되었다.

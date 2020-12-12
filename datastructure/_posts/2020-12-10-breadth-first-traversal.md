---
layout: post
title: "Binary Tree - Breadth First Traversal(python)"
tags:
  - [자료구조]
  - [트리]
  - [python]
  - [넓이 우선 순회]
---

## 넓이 우선 순회(Breadth Fisrt Traversal)

**원칙**

- 수준(level)이 낮은 노드를 우선으로 방문
- 같은 수준의 노드들 사이에는
  - 부모 노드의 방문 순서에 따라 방문
  - 왼쪽 자식을 오른쪽 자식보다 먼저 방문

**구현 방법**

- 노드를 방문했을 때 나중에 방문할 노드들을 순서대로 기록해야 한다. -> **큐**를 이용한다.

## 솔루션

1. 빈 리스트와 빈 큐를 초기화한다.
1. 빈 트리가 아니면(루트 노드가 존재하면) root 노드를 큐에 추가
1. 큐가 존재하는 동안:
   1. 큐에서 노드를 dequeue
   1. dequeue한 노드를 방문
   1. dequeue한 노드의 왼쪽, 오른쪽 자식이 존재하면 큐에 추가
1. 빈 큐면 모든 노드 방문 완료

## 코드 구현

```python
class ArrayQueue:

    def __init__(self):
        self.data = []

    def size(self):
        return len(self.data)

    def isEmpty(self):
        return self.size() == 0

    def enqueue(self, item):
        self.data.append(item)

    def dequeue(self):
        return self.data.pop(0)

    def peek(self):
        return self.data[0]


class Node:

    def __init__(self, item):
        self.data = item
        self.left = None
        self.right = None


class BinaryTree:

    def __init__(self, r):
        self.root = r

    def bft(self):
        # 빈 리스트와 빈 큐를 초기화한다.
        traversal = []
        q = ArrayQueue()
        # 빈 트리가 아니면(루트 노드가 존재하면) root 노드를 큐에 추가
        if self.root:
            q.enqueue(self.root)
            # 큐가 존재하는 동안
            while not q.isEmpty():
                # 큐에서 노드를 dequeue
                node = q.dequeue()
                # dequeue한 노드를 방문
                traversal.append(node.data)
                # dequeue한 노드의 왼쪽, 오른쪽 자식이 존재하면 큐에 추가
                if node.left:
                    q.enqueue(node.left)
                if node.right:
                    q.enqueue(node.right)
        return traversal


def solution(x):
    return 0
```

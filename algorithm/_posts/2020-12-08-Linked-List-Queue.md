---
layout: post
title: "Queue(Doubly Linked Lists로 구현)(python)"
tags:
  - [algorithm]
  - [python]
  - [양방향 연결 리스트]
  - [큐]
---

## 코드 구현

```python
# 이전에 작성한 Node, Doubly Linked List 클래스를 활용.
from dobuly import Node
from dobuly import DoublyLinkedList

class LinkedListQueue:

    def __init__(self):
        self.data = DoubleyLinkedList()

    def size(self):
        return self.data.getLength()

    def isEmpty(self):
        return self.size() == 0

    def enqueue(self, item):
        node = Node(item)
        self.data.insertAt(self.size() + 1, node)

    def dequeue(self):
        return self.data.popAt(1)

    def peek(self):
        return self.data.getAt(1).data
```

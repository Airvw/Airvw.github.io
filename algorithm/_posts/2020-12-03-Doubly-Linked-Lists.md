---
layout: post
title: "Doubly Linked List(python)"
tags:
  - [algorithm]
  - [python]
  - [양방향 연결 리스트]
---

## 양방향 연결 리스트

양방향으로 이동할 수 있는 연결 리스트이다.  
그렇기 때문에 head뿐 아니라 tail도 dummy 노드로 구성되어 있다.

## 코드 구현

```python
class Node:
    def __init__(self, item):
        self.data = item
        self.prev = None
        self.next = None

class DoubleyLinkedList:
    def __init__(self):
        self.nodeCount = 0
        self.head = Node(None)
        self.tail = Node(None)
        self.head.next = self.tail
        self.tail.prev = self.head

    def getLength(self):
        return self.nodeCount

    # 연결 리스트 순회
    def traverse(self):
        result = []
        curr = self.head
        # head와 tail 모두 더미 노드이므로 2번의 next를 통해 노드가 있는지 판단한다.
        while curr.next.next:
            curr = curr.next
            result.append(curr.data)
        return result

    # 연결 리스트 역순회
    def reverse(self):
        result = []
        curr = self.tail
        while curr.prev.prev:
            curr = curr.prev
            result.append(curr.data)
        return result

    # 특정 원소 얻어내기
    def getAt(self, pos):
        # 범위 밖의 경우
        if pos < 0 or pos > self.nodeCount + 1:
            raise IndexError

        # tail부터 시작하는 경우
        if pos > self.nodeCount // 2:
            i = 0
            curr = self.tail
            while i < self.nodeCount - pos:
                curr = curr.prev
                i += 1
        else:
            i = 0
            curr = self.head
            while i < pos:
                curr = curr.next
                i += 1
        return curr

    # 원소의 삽입
    def insertAfter(self, prev, newNode):
        curr = prev.next
        curr.prev = newNode
        prev.next = newNode
        newNode.prev = prev
        newNode.next = curr
        self.nodeCount += 1
        return True

    def insertBefore(self, next, newNode):
        curr = next.prev
        newNode.next = next
        newNode.prev = curr
        curr.next = newNode
        next.prev = newNode
        self.nodeCount += 1
        return True

    def insertAt(self, pos, newNode):
        if pos < 1 or pos > self.nodeCount + 1:
            raise IndexError

        prev = self.getAt(pos - 1)
        return self.insertAfter(prev, newNode)

    def popAfter(self, prev):
        curr = prev.next
        next = curr.next
        if next is None:
            return None
        data = curr.data
        prev.next = next
        next.prev = prev
        self.nodeCount -= 1
        return data

    def popBefore(self, next):
        curr = next.prev
        prev = curr.prev
        if prev is None:
            return None
        data = curr.data
        next.prev = prev
        prev.next = next
        self.nodeCount -= 1
        return data

    def popAt(self, pos):
        if pos < 1 or pos > self.nodeCount:
            raise IndexError

        prev = self.getAt(pos - 1)
        return self.popAfter(prev)

    def concat(self, L):
        prev = self.tail.prev
        next = self.head.next
        prev.next = next
        next.prev = prev
        if L.tail:
            self.tail = L.tail
        self.nodeCount += L.nodeCount
```

## 오류났던 부분

head와 tail 모두 더미 노드이므로 예외 상황 처리할 부분이 많이 없어서 전보다 쉽게 구현했다.

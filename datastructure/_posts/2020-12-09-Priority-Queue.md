---
layout: post
title: "Priority Queue(python)"
tags:
  - [자료구조]
  - [우선순위 큐]
  - [python]
---

## 우선순위 큐

FIFO(First-In First-Out) 방식을 따르지 않고 원소들의 우선순위에 따라 큐에서 빠져나오는 방식
-> 운영체제의 CPU 스케줄러에 활용

구현의 두 가지 방법

1. Enqueue 할때 우선순위 순서를 유지하도록 하는 방법
1. 큐에 들어있을 때는 아무 순서나 상관없지만 Dequeue 할때 우선순위 높은 것을 선택하는 방법

어느 것이 더 유리할까? -> **1번**이 더 유리하다.  
why? -> 2번의 경우 Dequeue 할때마다 모든 원소를 다 살펴봐야하기 때문이다.

재료의 두 가지 방법

1. 선형 배열 이용
1. 연결 리스트 이용

어느 것이 더 유리할까? -> **2번**이 더 유리하다.  
why? -> 1번의 경우 중간 삽입 과정에서 뒤에 있는 원소를 다 미뤄야 하기 때문이다.  
대신 2번의 경우 메모리를 더 많이 사용한다.

## 코드 구현

```python
# 이전에 작성한 Node, Doubly Linked List 클래스를 활용.
from dobuly import Node
from dobuly import DoublyLinkedList

class PriorityQueue():

    def __init__(self):
        self.queue = DoublyLinkedList()

    def size(self):
        return self.queue.getLength()

    def isEmpty(self):
        return self.size() == 0

    def enqueue(self, item):
        newNode = Node(item)
        curr = self.queue.head
        # 작은 수가 우선순위가 높다.
        while curr.next != self.queue.tail and curr.next.data > newNode.data:
            curr = curr.next
        self.queue.insertAfter(curr, newNode)

    def dequeue(self):
        return self.queue.popAt(self.size())

    def peek(self):
        return self.queue.getAt(self.size()).data
```

## 오류난 부분

- enqueue 부분에서 우선 순위가 높으면 head부분으로 와야한다고 생각해서, `curr.next.data < newNode.data`같이 반대로 비교했다.  
  dequeue 부분을 보면 우선 순위가 높은 부분(낮은 숫자)이 제일 tail에 있다.

- `while curr.next != self.queue.tail`부분에서 `while curr.next.next`로 대체 가능하다.  
  양방향 리스트는 head와 tail 모두 노드이므로 `while curr.next`대신 `while curr.next.next`로 써야한다.

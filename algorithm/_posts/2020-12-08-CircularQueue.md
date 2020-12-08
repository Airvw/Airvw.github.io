---
layout: post
title: "Circular Queue(python)"
tags:
  - [algorithm]
  - [programmers]
  - [환형 큐]
  - [python]
---

## 환형 큐

정해진 개수의 저장 공간을 돌려가며 이용하기 때문에, 환형 큐의 사이즈를 정해줘야 한다.

## 코드 구현

```python
class CircularQueue:
    def __init__(self, n):
        self.maxCount = n
        self.data = [None] * n
        self.count = 0
        self.rear = -1
        self.front = -1

    def size(self):
        return self.count

    def isEmpty(self):
        return self.size() == 0

    def isFull(self):
        return self.size() == self.maxCount

    def enqueue(self, item):
        if self.isFull():
            raise IndexError("Queue full")
        self.rear = (self.rear + 1) % self.maxCount
        self.data[self.rear] = item
        self.count += 1

    def dequeue(self):
        if self.isEmpty():
            raise IndexError("Queue empty")
        self.front = (self.front + 1) % self.maxCount
        data = self.data[self.front]
        self.count -= 1
        return data

    def peek(self):
        if self.isEmpty():
            raise IndexError("Queue empty")
        return self.data[(self.front + 1) % self.maxCount]
```

## 오류난 부분

peek() 메소드에서 rear와 front가 헷갈려서 오류가 났다.  
rear는 처음에 들어온 부분을 가르키고, front는 마지막에 들어온 가르킨다.

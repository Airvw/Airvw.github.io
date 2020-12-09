---
layout: post
title: "Linked List(python)"
tags:
  - [자료구조]
  - [python]
  - [연결 리스트]
---

## 연결 리스트(더미 노드 없는 경우)

연결 리스트는 노드로 구성되어 있고, 노드는 Data와 link로 이루어져있다.  
그리고 맨앞을 가르키는 head와 끝을 가르키는 Tail의 정보를 가지고 있다.  
마지막으로 연결 리스트에 노드가 몇개 있는지에 대한 정보가 있다.

![](https://airvw.github.io\assets\img\github\linked-list.png)

구현에서의 연결 리스트의 시작 인덱스는 1부터 시작한다.  
여기서 head와 tail은 dummy 노드가 아니다.  
처음에 dummy 노드로 생각해서 헷갈린 적이 있다.

코드를 보지 않고 처음부터 작성해보자~!

## 연산 정의

1. 특정 원소 참조(k 번째)
1. 리스트 순회
1. 길이 얻어내기
1. 원소 삽입
1. 원소 삭제
1. 두 연결 리스트 합치기

## 연결 리스트 구현 코드

```python
class Node:
    def __init__(self, item):
        self.data = item
        self.next = None

class LinkedList:
    def __init__(self):
        self.nodeCount = 0
        self.head = None
        self.tail = None

    # 특정 노드 참조
    def getAt(self, pos):
        # 범위 밖인 경우
        if pos < 1 or pos > self.nodeCount:
            raise IndexError

        # 연결 리스트의 인덱스는 1부터 시작하므로
        i = 1
        curr = self.head
        while i < pos:
            curr = curr.next
            i += 1
        return curr

    #  연결 리스트 순회
    def traverse(self):
        result = []
        curr = self.head
        while curr is not None:
            result.append(curr.data)
            curr = curr.next
        return result

    # 원소의 삽입
    def insertAt(self, pos, newNode):
        # 범위 밖인 경우
        if pos < 1 or pos > self.nodeCount + 1:
            return False

        # head 앞에 삽입하는 경우 -> head의 재정의가 필요하다.
        if pos == 1:
            curr = self.head
            newNode.next = curr
            self.head = newNode
        # 일반적인 경우
        else:
            # tail 뒤에 삽입하는 경우 -> self.tail을 통해서 prev를 손쉽게 구할 수 있다.
            if pos == self.nodeCount + 1:
                prev = self.tail
            # prev를 구하기 위해서 처음부터 노드를 찾아야 한다.
            else:
                prev = self.getAt(pos - 1)
            curr = prev.next
            prev.next = newNode
            newNode.next = curr

        # tail 뒤에 삽입하는 경우 -> tail의 재정의가 필요하다.
        if pos == self.nodeCount + 1:
            self.tail = newNode

        self.nodeCount += 1
        return True

    # 원소의 삭제(삭제하는 노드의 data를 리턴)
    def popAt(self, pos):
        data = None
        # 범위 밖인 경우
        if pos < 1 or pos > self.nodeCount:
            return IndexError

        # head에 위치한 노드를 제거하는 경우 -> head의 재정의 필요
        if pos == 1:
            curr = self.head
            data = curr.data
            self.head = curr.next
        # 일반적인 경우
        else:
            prev = self.getAt(pos - 1)
            curr = prev.next
            data = curr.data
            prev.next = curr.next
            # tail에 위치한 노드를 제거하는 경우 -> tail의 재정의 필요
            if pos == self.nodeCount:
                self.tail = prev

        # 연결 리스트의 노드가 1개인 경우 -> tail의 재정의 필요
        # self.head를 재정의 및 데이터를 갱신하지 않는 이유는 if pos == 1: 에서 이미 head를 재정의 및 데이터 갱신을 해주기 때문이다.
        if pos == 1 and pos == self.nodeCount:
            self.tail = None

        self.nodeCount -= 1
        return data

    def concat(self, L):
        # self의 끝과 L의 시작을 이어줘야 한다.
        prev = self.tail
        next = L.head
        prev.next = next
        # tail의 재정의가 필요하다.
        if L.tail:
            self.tail = L.tail
        self.nodeCount += L.nodeCount
```

## 오류났던 부분

def popAt(self, pos)를 작성하는 중에 초기에 data를 초기화하지 않고, if문 안에서 data를 초기화하고, 갱신하면서 data부분에서 오류가 났다.  
if문 안에서의 data는 지역 변수이므로, if문 밖의 data에 대해 영향을 끼치지 않는다는 점을 간과했다..

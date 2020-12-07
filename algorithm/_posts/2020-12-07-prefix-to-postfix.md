---
layout: post
title: "중위 표현 수식 -> 후위 표현 수식(python)"
tags:
  - [algorithm]
  - [programmers]
  - [stack]
  - [python]
---

## 중위 표기법(infix notation)

연산자가 피연산자들의 사이에 위치  
ex) `(A + B) * (C + D)`

## 후위 표기법(postfix notation)

연산자가 피연산자들의 뒤에 위치  
ex) `A B + C D + *`

## 중위 표현 수식 -> 후위 표현 수식 솔류션

1. 연산자를 만나면 스택에 넣는다.
1. 만약 스택에 다른 연산자가 있다면 직전 연산자와 우선 순위를 비교한다.

- 현재의 연산자가 우선 순위가 더 크면 스택에 넣어준다.
- 스택에 있는 연산자가 우선 순위가 더 크면 스택에 있는 연산자를 pop 해주고, 현재의 연산자를 스택에 넣어준다.  
  (단, 스택에 있는 연산자의 우선 순위가 작을 때까지 비교 해야한다.)

1. 만약 괄호가 나타난다면 여는 괄호는 스택에 넣는다.

- 닫는 괄호의 경우 스택에서 여는 괄호가 나올 때 까지 pop를 해준다.  
  (여는 괄호 너머까지 pop 하지 않도록 여는 괄호의 우선 순위는 가장 낮게 설정해준다.)

1. 수식을 모두 탐색한 이후 스택에 남아 있는 연산자는 모두 pop해준다.

## 코드 구현

```python
class ArrayStack:

    def __init__(self):
        self.data = []

    def size(self):
        return len(self.data)

    def isEmpty(self):
        return self.size() == 0

    def push(self, item):
        self.data.append(item)

    def pop(self):
        return self.data.pop()

    def peek(self):
        return self.data[-1]

prec = {
    '*': 3, '/': 3,
    '+': 2, '-': 2,
    '(': 1
}

def solution(s):
    opStack = ArrayStack()
    answer = ""
    for op in s:
        # 닫는 괄호를 만나는 경우
        if op == ")":
            #  여는 괄호를 만날 때까지 pop
            while opStack.peek() != "(":
                answer += opStack.pop()
            # 스택에 있는 여는 괄호 pop
            opStack.pop()
        # 연산자들이 아닌 경우
        elif op not in prec:
            answer += op
        else:
            # 스택이 비어있는 경우
            if opStack.isEmpty():
                opStack.push(op)
            # 스택에 연산자들이 있는 경우
            else:
                # 현재의 연산자의 우선 순위가 더 큰 경우
                if prec[opStack.peek()] < prec[op] or op == "(":
                    opStack.push(op)
                # 현재의 연산자의 우선 순위가 더 작은 경우
                else:
                    # 스택에 있는 연산자들 중 현재의 연산자보다 우선 순위가 더 큰 경우 모두 pop
                    while not opStack.isEmpty():
                        if prec[opStack.peek()] >= prec[op]:
                            answer += opStack.pop()
                        else:
                            break
                    opStack.push(op)
    while not opStack.isEmpty():
        answer += opStack.pop()

    return answer
```

## 오류났던 부분

```python
while not opStack.isEmpty():
  if prec[opStack.peek()] >= prec[op]:
      answer += opStack.pop()
  else:
      break
opStack.push(op)
```

while문 조건 부분에서
`while prec[opStack.peek()] >= prec[op]:`로 구현해서 스택에 더이상 연산자가 없는 경우로 인해서 `list index out of range`오류가 발생했다.

while문 else 부분에서

```python
else:
  opStack.push(op)
  break
```

이렇게 구현해서 스택에 있는 연산자들 중 현재의 연산자보다 우선 순위가 더 큰 경우들만 있는 경우 `while not opStack.isEmpty():` 조건으로 인해서  
`else`가 구현되지 않아, 연산자가 스택에 push가 되지 않는 경우가 발생했다.

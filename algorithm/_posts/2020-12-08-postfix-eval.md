---
layout: post
title: "후위표현 수식 계산(python)"
tags:
  - [algorithm]
  - [programmers]
  - [stack]
  - [python]
---

## 솔루션

1. 피연산자이면 스택에 push
1. 연산자이면 스택에서 pop, 또 다시 pop, 연산자로 계산 후 결과를 스택에 push
1. 끝에 도달하면 스택에서 pop(계산 결과)

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

# 숫자와 연산자를 구분해서 리스트로 반환하는 함수
def splitTokens(exprStr):
    tokens = []
    val = 0
    valProcessing = False
    for c in exprStr:
        if c == ' ':
            continue
        if c in '0123456789':
            # 한 자리수 이상의 숫자들을 판별
            val = val * 10 + int(c)
            valProcessing = True
        else:
            if valProcessing:
                tokens.append(val)
                val = 0
            valProcessing = False
            tokens.append(c)
    # 마지막 숫자를 push
    if valProcessing:
        tokens.append(val)

    return tokens


def infixToPostfix(tokenList):
    prec = {
        '*': 3,
        '/': 3,
        '+': 2,
        '-': 2,
        '(': 1,
    }

    opStack = ArrayStack()
    postfixList = []

    for token in tokenList:
        # 숫자인 경우 경우
        if type(token) is int:
            postfixList.append(token)
        # 닫는 괄호를 만나는 경우
        elif token == ")":
            #  여는 괄호를 만날 때까지 pop
            while opStack.peek() != "(":
                postfixList.append(opStack.pop())
            # 스택에 있는 여는 괄호 pop
            opStack.pop()
        # 연산자인 경우
        else:
            # 스택이 비어있는 경우
            if opStack.isEmpty():
                opStack.push(token)
            # 스택에 연산자들이 있는 경우
            else:
                # 현재의 연산자의 우선 순위가 더 큰 경우 및 여는 괄호인 경우
                if prec[token] > prec[opStack.peek()] or token == "(":
                    opStack.push(token)
                # 현재의 연산자의 우선 순위가 더 작은 경우
                else:
                    # 스택에 있는 연산자들 중 현재의 연산자보다 우선 순위가 더 큰 경우 모두 pop
                    while not opStack.isEmpty():
                        if prec[token] <= prec[opStack.peek()]:
                            postfixList.append(opStack.pop())
                        else:
                            break
                    opStack.push(token)

    while not opStack.isEmpty():
        postfixList.append(opStack.pop())

    return postfixList


def postfixEval(tokenList):
    valStack = ArrayStack()

    for token in tokenList:
        if type(token) is int:
            valStack.push(token)
        else:
            b = valStack.pop()
            a = valStack.pop()
            if token == "*":
                valStack.push(a * b)
            elif token == "/":
                valStack.push(a / b)
            elif token == "+":
                valStack.push(a + b)
            elif token == "-":
                valStack.push(a - b)
    return valStack.pop()

def solution(expr):
    tokens = splitTokens(expr)
    postfix = infixToPostfix(tokens)
    val = postfixEval(postfix)
    return val
```


## 오류난 부분

- splitToken() 함수에서 
    ```python
    val = val * 10 + int(c)
    valProcessing = True
    ```
    val과 valProcessing이 무슨 역할을 하는지 몰랐었다.  
    val과 valProcessing은 한 자리수 이상의 숫자들을 판별하기 위해서 필요하다.

- postfixEval() 함수에서 
    ```python
    else:
    b = valStack.pop()
    a = valStack.pop()
    if token == "*":
        valStack.push(a * b)
    ```
    a, b의 순서를 바꿔서 구현해서 오류가 발생했다.  
    스택에서 pop 해주는 것이라서 a가 b보다 먼저 들어간 숫자다.  
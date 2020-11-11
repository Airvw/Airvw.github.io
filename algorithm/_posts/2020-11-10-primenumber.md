---
layout: post
title: "소수 찾기"
tags:
  - [algorithm]
  - [python]
---

## 참고 자료

[나동빈님의 유튜브](https://www.youtube.com/watch?v=cswJ1h-How0&list=PLRx0vPvlEmdAghTr5mXQxGpHjWqSz0dgC&index=9)

## 기본적인 소수 찾기

기본적인 소수 찾기 생각이다.  
이 경우 모든 수를 확인한다는 점에서 시간 복잡도는 **O(X)**이다.

```python
# 소수 판별 함수
def is_prime_number(x):
    #  2부터 x -1 까지 모든 수를 확인하며
    for i in range(2, x):
        # x가 해당 수로 나누어 떨어진다면
        if x % i == 0:
            #  소수가 아니다.
            return False
    # 모든 수로 나누어 떨어지지 않으면 소수다.
    return True

print(is_prime_number(4))
print(is_prime_number(7))
```

결과

```
False
True
```

## 약수의 성질

모든 약수가 가운데 약수를 기준으로 곱셈 연산에 대해 대칭을 이룬다.  
16의 약수는 1, 2, 4, 8, 16  
4를 기준으로 2 _ 8 = 16, 1 _ 16 = 16  
따라서 약수를 찾을 때 가운데 약수(제곱근)까지만 확인하면 된다.  
16이 2로 나누어떨어진다는 것은 8로도 나누어떨어진다는 것을 의미한다.

## 약수의 성질을 이용한 소수 찾기

이 경우 제곱근까지 확인한다는 점에서 시간 복잡도는 **O(X<sup>1/2</sup>)**이다.

```python
import math

# 소수 판별 함수
def is_prime_number(x):
    #  2부터 x의 제곱근까지 모든 수를 확인하며
    for i in range(2, int(math.sqrt(x)) + 1):
        # x가 해당 수로 나누어떨어진다면
        if x % i == 0:
            #  소수가 아니다.
            return False
    # 모든 수로 나누어떨어지지 않으면 소수다.
    return True

print(is_prime_number(4))
print(is_prime_number(7))
```

결과

```
False
True
```

## 에라토스테네스의 체 알고리즘

다수의 자연수에 대하여 소수 여부를 판별할 때 사용된다.

- 동작과정
  1.  2부터 N까지의 모든 자연수를 나열한다.
  1.  남은 수 중에서 처리하지 않은 가장 작은 수 i를 찾는다.
  1.  남은 수 중에서 i의 배수를 모두 제거한다.(단, i는 제거하지 않는다.)
  1.  더 이상 반복할 수 없을 때까지 2, 3번 과정을 반복한다.

## 에라토스테네스의 체를 이용한 소수 찾기

이 경우 시간 복잡도는 **O(NloglogN)**이고, 선형 시간에 가깝다.  
하지만 소수 여부를 저장해야 하므로 메모리가 많이 필요하다.

```python
import math

n = 1000
array = [True for _ in range(n + 1)]

for i in range(2, int(math.sqrt(n)) + 1):
    #  처리하지 않은 가장 작은 수인 경우
    if array[i] == True:
        #  i를 제외한 i의 모든 배수를 지우기
        j = 2
        while i * j <= n:
            array[i * j] = False
            j += 1

# 모든 소수 출력
for i in range(2, n + 1):
    if array[i]:
        print(i, end = "")
```

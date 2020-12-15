---
layout: post
title: "선형 시스템"
tags:
  - [math]
  - [linear system]
---

## 선형 시스템

---

중등 교과과정에서의 배운 조금 복잡한 연립일차방정식 -> **linear system(선형시스템)**  
$$ 3x + y + z = 4 $$  
$$ x - 2y - z = 1 $$  
$$ x + y + z = 2 $$

## 선형 대수의 목표

---

어떤 연립일차방정식, 즉 **linear system(선형 시스템)**문제라도 정형적인 방법으로  
표현하고 해결하는 방법을 배우는 것  
$ Ax = b $

## 선형 시스템의 구성 요소

---

- **Linear Equations(선형 방정식)** : 선의 형태
- **Unknown(미지수)**

## m X n 선형 시스템

---

<span style="color:red">**3개의 linear equations**</span>, <span style="color:green">**3개의 unkowns**</span>로 구성된 연립일차방정식  
<span style="color:red">**3**(식의 갯수)</span> X <span style="color:green">**3**(미지수의 갯수)</span> linear system

## 선형 방정식, 비선형 방정식 구분 방법

---

선형 방정식 : unknown의 승수가 1로만 구성되어 있다.  
그외 : 비선형 방정식

## 선형 시스템의 대수적 표현

---

$$ Ax = b $$로 표현하기

1. 선형 시스템의 unknowns를 모아 column vector(열벡터) x로 표현
1. coefficients(계수)를 모아 A의 row vector(행벡터)로 표현
1. constant(상수)를 모아 b에 표현

$$ 3x + y = 2 $$  
$$ x - 2y = 3 $$ => $$ A x = b $$ => $$ \left[\begin{array}{lcr} 3 & 1\\1 & -2\\2 & -4\end{array}\right] \left[\begin{array}{lcr} x \\ y\end{array}\right] = \left[\begin{array}{lcr} 2 \\ 3 \\ 6\end{array}\right] $$  
$$ 2x - 4y = 6$$

## m x n 선형 시스템의 Ax = b 표현 정리

---

- m은 선형 방정식의 갯수
- n은 unknown의 갯수
- A는 m x n 행렬
- x는 n-벡터
- b는 m-벡터

## 선형 시스템(Ax = b)의 해

---

1. 해가 하나인 경우 : $ 3x = 6 $
1. 해가 없는 경우 : $ 0x = 6 $ (평행인 경우)
1. 해가 여러개인 경우 : $ 0x = 0 $ (겹치는 경우)

- A의 역수가 존재하지 않는 경우, A는 **특이(singular)**하다고 한다. (2, 3번의 경우)
- 해가 있으면 선형 시스템이 **consistent**하다고 한다. (1, 3번의 경우)
- 해가 없으면 선형 시스템이 **inconsistent**하다고 한다. (2번의 경우)

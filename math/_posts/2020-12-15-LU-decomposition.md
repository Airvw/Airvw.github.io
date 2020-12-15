---
layout: post
title: "LU 분해(행렬분해)"
tags:
  - [math]
  - [matrix decomposition]
  - [LU decomposition]
---

## 행렬 분해

---

- LU 분해(LU decomposition)
- QR 분해(QR decomposition)
- 특이값 분해(SVD, Singular Value Decomposition)

## LU 분해

---

주어진 행렬을 아래의 형태를 가지는 두 행렬의 곱으로 나누는 행렬 분해
![](https://airvw.github.io\assets\img\github/LU.png)

- L : lower triangular matrix(하삼각행렬)
- U : upper trianular matrix(상삼각행렬)

## LU 분해의 역할

---

$$ Ax = b => (LU)x = b => L(Ux) = b => Ly = b(단, Ux = y) $$  
Ax = b문제에서 먼저 Ly = b(풀기 쉬운 형태)풀고, Ux = y를 푸는 문제로 바뀜

1. Forward-substition(전방대입법) : y 구하기
   ![](https://airvw.github.io\assets\img\github/forword-substition.png)
2. Back-substition(후방대입법) : x 구하기
   ![](https://airvw.github.io\assets\img\github/back-substition.png)

## LU 분해의 의미

---

가우스 소거법의 forward elimination(전방소거법)을 행렬로 코드화 한 것
$$ A = PLU $$

- L : 행렬 A를 전방소거하는데 쓰인 replacement와 scaling에 대한 EROs를 기록해 둔 행렬
- U : 행렬 A를 전방소거한 후 남은 upper triangular matrix(상삼각행렬)
- P : 행렬 A를 전방소거하는데 쓰인 interchange(행과 행의 교환)에 대한 EROs를 기록해 둔 행렬(옵션)

## LU 분해의 활용

---

- 수치적 안정성 : 역행렬 A<sup>-1</sup>를 직접 구하는 것보다 PLU 분해를 이용하는 것이 안정적
- 행렬 A가 고정이고, b가 자주 업데이트되는 경우 : PLU 분해는 b가 업데이트될 때마다 x를 실시간으로 구할 수 있다.

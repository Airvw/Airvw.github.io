---
layout: post
title: "선형 조합"
tags:
  - [math]
  - [partitioned matrix]
  - [linear combination]
---

## 선형 조합

---

- Ax : 행렬 A가 가지고 있는 열벡터의 선형 조합
- 벡터(열벡터)들에 대한 가중치 합

![](https://airvw.github.io\assets\img\github/linear-combination.png)
(a<sub>i</sub>는 A의 열벡터들)

## 선형 시스템 Ax = b를 선형조합 관점에서 바라보기

---

- 선형 조합으로 벡터 b를 만들 수 있는 가중치 조합이 존재한다면, Ax = b의 해는 존재.
- 어떤 특징을 담고 있는 행렬을 weight들의 합으로 선형조합할 때 벡터 b를 만들 수 있는 weight들의 조합이 존재한다면, 해가 존재하며, 그 해는 weight들로 구성되어 있다.

## 열공간(Column Space)

---

col(A) : 행렬 A의 열벡터들에 대한 가능한 모든 선형조합의 결과를 모아 집합으로 구성한 것

- 선형 시스템 Ax = b가 해를 가지면(consistent) : $ b \in col(A) $
- 선형 시스템 Ax = b가 해가 없으면(inconsistent) : $ b \notin col(A) $

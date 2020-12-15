---
layout: post
title: "행렬과 텐서"
tags:
  - [math]
  - [matrix]
  - [tensor]
---

## 행렬

---

직사각형 구조에 숫자들을 담아 놓은 구조 **(여러개의 열벡터를 나열한 구조)**

- 하나의 행을 가진 행렬 : 행벡터(row vector)
- 하나의 열을 가진 행렬 : 열벡터(column vector)
- 1 x 1 행렬 : 스칼라(scalar)

## 전치 행렬(Transpose Matrix)

---

m x n 행렬 A에 대한 전치 행렬 A<sup>T</sup>는 A의 행을 열로, 열을 행으로 가지는 n x m 행렬

## 벡터 표기법

---

- 벡터라고 하면 일반적으로 열벡터(column vector)를 의미
- n-벡터는 n개의 스칼라(scalar)로 구성된 열벡터(column vector)를 의미
  ![](https://airvw.github.io\assets\img\github/column-vector.png)

## 정방 행렬(Square Matrix)

---

행과 열 모두 n인 정사각형 모양의 행렬을 n차 **정방행렬**이라고 한다.  
a<sub>i</sub><sub>j</sub>를 행렬 A<sub>n</sub>의 주 대각선(main diagonal)이라 한다.  
![](https://airvw.github.io\assets\img\github/square-matrix.png)

## 항등 행렬(Identity Matrix)

---

주대각선이 모두 1이고, 나머지 요소가 모두 0인 n차 정방행렬을 **항등행렬**이라고 한다.
![](https://airvw.github.io\assets\img\github/identity-matrix.png)

## 행렬 곱

---

- 병렬 처리(parallel processing)로 가속할 수 있다. (결과가 독립적)

## 텐서(tensor)

---

스칼라, 벡터, 행렬을 아우르는 개념.  
숫자가 늘어설 수 있는 방향이 k개면 k-텐서

- 0-텐서 : 스칼라
- 1-텐서 : 벡터
- 2-텐서 : 행렬

---
layout: post
title: "가우스 소거법"
tags:
  - [math]
  - [linear system]
  - [gauss elimination]
---

## 가우스 소거법

---

임의의 m x n 선형 시스템의 해를 구하는 가장 대표적인 방법

1. Forward elimination(전방소거법) : 아래로 갈수록 더 단순한 형태의 선형방정식을 가지도록 변형
1. Back-substitution(후방대입법) : 아래에서부터 위로 미지수를 실제값으로 대체(해를 구하는 과정)
   ![](https://airvw.github.io\assets\img\github/gauss.png)

## 소거법에 쓰이는 기본행연산(EROs : Elementary Row Operations)

---

- Replacement(치환): r<sub>j</sub> <- r<sub>j</sub> - mr<sub>i</sub>
  - j번째 행을 기준행인 i번째 행을 m배하여 빼서 수정
- Interchange(교환): r<sub>j</sub> <-> r<sub>i</sub>
  - j번째 행과 i번째 행의 위치를 서로 바꾼다.
- Scaling(스케일링): r<sub>j</sub> <- sr<sub>j</sub>
  - j번째 행을 s배 스케일링한다.

## Forward Elimination(전방소거법)의 의미

---

- 선형 시스템을 가장 풀기 쉬운 꼴로 변형 **(상삼각형태 : Upper triangular form)**
- 선형 시스템의 rank를 알려준다.
- 선형 시스템이 consistent(해가 있는지) 아니면 inconsistent(해가 없는지) 알려준다.

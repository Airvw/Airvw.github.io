---
layout: post
title: "Fork한 repository 최신화하기"
tags:
  - [github]
---

## 참고 자료

---

[Fork 한 Repository 업데이트 하기](https://velog.io/@k904808/Fork-%ED%95%9C-Repository-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%ED%95%98%EA%B8%B0)
https://gmlwjd9405.github.io/2017/10/28/how-to-collaborate-on-GitHub-2.html
[이미지로 과정 살펴보기](https://gmlwjd9405.github.io/2017/10/28/how-to-collaborate-on-GitHub-2.html)
[Pull과 fetch의 차이](https://yuja-kong.tistory.com/60)

## fork된 repository 최신으로 동기화

---

1. remote 현황 파악 : `git remote -v`
1. upstream이라는 이름으로 원격 저장소 주소를 등록 : `git remote add upstream '원본 repository url'`
1. `git fetch upstream`
1. `git merge upstream/브랜치 이름`
1. `git push origin 브랜치 이름`

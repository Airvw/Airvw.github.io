---
layout: post
title: "git으로 github repository 초기화 하기"
tags:
- [git]
- [github]
---

## 참고자료
<https://opentutorials.org/course/2708> 생활코딩  
<https://gutmate.github.io/2017/03/22/git-history-remove/> gutmate님의 블로그  

## Git과 Github
Git은 파일을 추적하는 시스템으로 생각
- 파일이 생성되었는지, 없어졌는지, 코드가 변했는지 등등
- 파일명으로 추적하는 것이 아니라 내용으로 추적
    - 파일명이 달라도 내용이 같으면 같은 오브젝트로 취급
    - 내용에 대해서 SHA-1 Hash 알고리즘을 통해서 나온 값으로 파일명을 생성하여 추적하기 때문

Github는 협업을 위해서 사용하는 저장소로 생각
- Git을 통해서 Github에 업무 파일을 저장하여 서로가 다운받고, 고칠 수 있음
- 프로젝트 진행시 서로가 진행한 업무 파일을 이메일 등으로 보낼 필요없음

## Git을 통한 초기화 시도
Git을 초기화 하는 이유
- jekyll 테마를 변경하기 위해서
- 기존 코드에서 수정하며 바꾸기에는 실력이 부족함

Git으로 초기화 시도
- git clone으로 repository를 다운 받고, 해당 폴더를 git remote로 Github 저장소와 연결
- git clone한 파일들을 다 삭제하고 다른 테마를 복사함
- git add, commit, push를 통해서 Github 저장소에 저장함 -> 기존 폴더들을 다 삭제해서 없어지고, 복사한 파일들이 저장될 줄 알았음

발생한 문제점
- 복사한 파일들이 저장되긴 했는데, 기존의 파일들도 존재하는 현상이 발생

이유
- 내용으로 추적하기 때문에 같은 내용을 담고 있는 파일들이 바뀌지 않고 그대로 존재

## Git을 통한 초기화 방법  
1. 기존의 히스토리 삭제
```bash
$ rm -rf .git
```
1. 파일정리 후 새로운 git 설정
```bash
$ git init
$ git add .
$ git commit -m "first commit"
```
1. git 저장소 연결 후 강제 push
```bash
$ git remote add origin {git remote url}
$ git push -u --force origin master
``` 

## commit의 원리  
Object 파일은 크게 3가지
- blob : 파일의 내용을 담고 있는 해쉬값
- tree : 파일명과 blob에 대한 정보를 담고 있는 해쉬값
- commit : tree에 대한 정보와 이전 커밋의 부모에 대한 정보를 담고 있는 해쉬값

## 더 알아보기  
- git branch
- sha-1 Hash 알고리즘
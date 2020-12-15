---
layout: post
title: "github.io 블로그 제작 과정"
tags:
  - [Blog]
  - [github.io]
---

## 참고자료

---

저는 [devinlife님의 블로그](https://devinlife.com/howto/)사이트를 참조하여 제작하였습니다.  
단계별로 차근차근 설명이 잘 되어있기 때문에 참조하시면 됩니다.  
저는 윈도우에서 블로그를 만들었기 때문에 블로그 제작 과정에서 여러가지 문제점과 해결방법을 소개해드리려고 합니다.

## Ruby와 jekyll을 사용하는 이유

---

지킬을 로컬에 깔아서 블로그를 로컬에서 실행하고 고치는 과정이 훨씬 편하다는 것을 알 수 있었습니다.
로컬에서 확인하는 작업이 없으면 github에서 push된 이후 블로그 확인하는데 1~2분의 기다림이 있기에 상당히 귀찮습니다.

## GitHub Pages 블로그 준비하기

---

루비 설치는 rubyinstaller-devkit-2.6.5을 설치했었지만 nexT theme <https://simpleyyt.com/jekyll-theme-next/tutorial/2017/07/20/next-tutorial/>을 사용하려고 하니 2.5버전을 설치하라고 해서 다시 rubyinstaller-devkit-2.5.7을 설치했습니다.  
이 과정에서 윈도우에서 루비 버전 변경이 궁금했는데 그냥 2.5.7버전을 설치했더니 버전 변경이 되었습니다.
설치 과정에서 path를 자동으로 추가했습니다.
이후 명령어 실행시 path경로 앞쪽부터 순서대로 실행이 되기 때문에 버전이 자동으로 변경될 수 있었습니다.
ruby 삭제시 깔린 폴더에서 unins000을 실행하여 제거하고, 폴더 삭제를 진행했습니다.

jekyll과 bundler 설치는 cmd창에서 gem install jekyll bundler 명령어를 실행하여 설치했습니다.

## Jekyll theme을 사용하여 블로그 생성하기

---

저는 <https://github.com/simpleyyt/jekyll-theme-next> 이것을 git clone했습니다.
이 테마를 로컬에서 돌리니 github.api가 없다는 오류가 떴습니다. ~~아직 오류는 해결 못했지만~~ github.io 블로그는 정상적으로 작동했습니다.
description에 대한 내용이 없어서 오류가 발생하였습니다.
이름 변경은 gui상에서 변경하였고, remote 추가 후 push를 하니 보안상 문제가 떴는데 넘어갔습니다.

## GitHub 블로그 첫글쓰기

---

touch라는 파일 생성 명령어는 윈도우에 없으므로 copy /Y /b NUL 2019-04-13-first-post.md 명령어를 통해서 md 파일을 생성해줬고 notepad 2019-04-13-first-post.md 명령어를 통해 편집을 해주고 저장했더니
2019-04-13-first-post.md: invalid byte sequence in UTF-8 이러한 에러가 발생했습니다. 알아보니 윈도우 메모장은 저장시에 기본 설정이 ANSI 형식이어서 오류가 발생했습니다.
다시 notepad 2019-04-13-first-post.md 명령어를 통해 편집을 시도하였고 메모장 탭에서 다른 이름 저장을 \_posts 폴더안에서 utf-8형식으로 저장해줬더니 오류가 해결되었습니다. 그리고 저장할때 파일형식을 모든 파일로 하고 기존에 존재하는 md 파일에 덮어쓰면 됩니다.
(vscode IDE를 사용하는 것이 더 편하다고 생각합니다.)

## 블로그 카테고리와 태그 목록 구성하기

---

last_modified_at: 2019-04-13T08:06:00-05:00를 직접 작성해야 되는지 궁금해서 찾아봤는데 아직 찾지 못하였습니다.

## 11번 이후

---

아직 필요하지 않다고 생각되서 시도하지 않았습니다. 차후에 시도해볼 예정입니다.

## 윈도우에서 notepad 편집의 문제점

---

cmd창에서 notepad를 사용해서 md 파일을 수정하였더니 ![](https://airvw.github.io\assets\img\github/markdown-error.png)와 같이 표시됩니다.  
원래는 ![](https://airvw.github.io\assets\img\github\markdown.png)와 같이 표시되어야 합니다.  
오류의 원인은 윈도우에서 윈도우 계열과 유닉스(맥, 리눅스) 계열에서의 서로 다른 플랫폼에서의 공유시 발생하는 소스의 줄바꿈이었습니다.  
이것을 해결하기 위해서 윈도우에서 ubuntu 쉘을 사용할 수 있는 WSL을 사용했습니다.  
<https://wnsgml972.github.io/setting/wsl.html> 사이트를 참조하여 설치하였고, microsoft store에서 ubuntu를 설치했습니다.  
설치 후 user 설정하고 sudo apt-get update, sudo apt-get install vim git 명령어로 vim과 git만 설치했습니다.  
ubuntu쉘에서 cd /mnt 하니 윈도우상의 폴더로 접근 가능하였고, 여기서 새로운 md 파일을 생성하고 vim으로 편집했더니 위 사진의 오류는 발생하지 않았습니다.

## nexT 테마 기본설정

---

무엇을 수정했는지는 <https://github.com/Airvw/airvw.github.io/blob/master/_config.yml> 여기에서 확인해보시면 됩니다.  
크게 site, url, atom feed, authoricon, menu, sidebar settings, disqus를 수정했습니다.  
댓글 기능을 추가할시 shortname을 입력해야 정상적으로 작동되는 것 같습니다.  
shortname은 <https://disqus.com/>에서 계정의 Install on Site의 General탭에서 확인하실 수 있습니다.

## 현재 의문점

---

~날짜와 시간을 직접 입력해야 하는지~  
~~next 테마에서는 로컬 작동이 안되는지~~

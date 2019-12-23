---
title: "github.io 블로그 제작 과정"
categories:
- Blog
tags:
- Blog
- github.io
---

저는 블로그를 <https://devinlife.com/>사이트를 참조하여 제작하였습니다.  
단계별로 차근차근 설명이 잘 되어있기 때문에 참조하시면 됩니다.  
저는 윈도우에서 블로그를 만들었기 때문에 블로그 제작 과정에서 여러가지 문제점과 해결방법을 소개해드리려고 합니다.

##1. GitHub Pages 블로그 소개  
확실히 지킬을 로컬에 깔아서 로컬에서 실행하고 고치는 과정이 훨씬 편하다는 것을 알 수 있었습니다.  
로컬에서 확인하는 작업이 없으면 github에서 push된 이후 블로그 확인하는데 1~2분의 기다림이 있기에 상당히 귀찮습니다.  
  
##2. GitHub Pages 블로그 준비하기  
루비 설치는 rubyinstaller-devkit-2.6.5을 설치했었지만 nexT theme <https://simpleyyt.com/jekyll-theme-next/tutorial/2017/07/20/next-tutorial/>을 사용하려고 하니 2.5버전을 설치하라고 해서 다시 rubyinstaller-devkit-2.5.7을 설치했습니다.  
이 과정에서 윈도우에서 루비 버전 변경이 궁금했는데 그냥 2.5.7버전을 설치했더니 버전 변경이 되었습니다.  
  
jekyll과 bundler 설치는 cmd창에서 gem install jekyll bundler 명령어를 실행하여 설치했습니다.  
  
bundle exec jekyll serve 명령어를 사용하여 로컬 작동을 하였지만 bundle exec jekyll serve -H 192.168.0.8 명령어를 통한 작동은 성공은 했는데 바로 종료되었습니다. 이유는 잘 모르겠습니다.  
  
##3. Jekyll theme을 사용하여 블로그 생성하기  
저는 <https://github.com/simpleyyt/jekyll-theme-next> 이것을 git clone하였습니다.  
이 테마를 로컬에서 돌리니 github.api가 없다는 오류가 떴습니다. 아직 오류는 해결 못했지만 github.io 블로그는 정상적으로 작동했습니다.  
이름 변경은 gui상에서 변경하였고, remote 추가 후 push를 하니 보안상 문제가 떴는데 넘어갔습니다.  
  

---
layout: post
title: "Github 블로그에 MathJax로 수식 작성하기"
tags:
  - [Mathjax]
  - [github.io]
---

## 참고 자료

---

[MKKIM님의 블로그](https://mkkim85.github.io/blog-apply-mathjax-to-jekyll-and-github-pages/#mathjax-%EC%A0%81%EC%9A%A9-%EB%B0%A9%EB%B2%95)  
[Seongkyun Han님의 블로그](https://seongkyun.github.io/others/2019/01/03/MathJax/)

## Mathjax를 hydejack 테마 블로그에 적용

---

1.  \_config.yml 파일 설정

    - \_config.yml에 이미 해당 설정이 존재하기 때문에 굳이 변경할 필요가 없다고 생각해서 수정하지 않았다.

    ```python
    kramdown:
    math_engine: mathjax
    math_engine_opts: {}

    footnote_backlink: "&#x21a9;&#xfe0e;"
    ```

1.  \_includes 디렉토리의 `my-head.html`파일의 마지막에 다음 내용을 추가한다.

    ```python
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            TeX: {
            equationNumbers: {
                autoNumber: "AMS"
            }
            },
            tex2jax: {
            inlineMath: [ ['$', '$'] ],
            displayMath: [ ['$$', '$$'] ],
            processEscapes: true,
        }
        });
        MathJax.Hub.Register.MessageHook("Math Processing Error",function (message) {
            alert("Math Processing Error: "+message[1]);
            });
        MathJax.Hub.Register.MessageHook("TeX Jax - parse error",function (message) {
            alert("Math Processing Error: "+message[1]);
            });
    </script>
    <script type="text/javascript" async
    src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
    </script>
    ```

1.  모든 페이지에서 수식을 허용하므로 아래 내용을 굳이 삽입하지 않았다.  
    {% raw %}
    ```html
    {% if page.use_math %} {% include mathjax_support.html %} {% endif %}
    ```
    {% endraw %}

## 오류 발생 부분

---

- \_includes 디렉토리의 `my-head.html`파일의 마지막에 다음 내용을 추가했을 때
  inline 수식이 적용되지 않았다.

  ```python
  <script type="text/javascript" async
      src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
  </script>
  ```

  혹은

  ```python
  <script type="text/x-mathjax-config">
      MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});
  </script>
  <script type="text/javascript" src="http://cdn.mathjax.org/math..."></script>
  ```

- 처음에는 수식이 적용되지 않다가 새로고침하면 적용되어 있는 경우가 있다.
  (아직 이유는 모르겠다..)

## 수식 작성에 도움이 되는 사이트

---

- <https://johngrib.github.io/wiki/mathjax-latex/> (간단한 사용예시)
- <https://www.codecogs.com/latex/eqneditor.php> (온라인에서 수식 확인 가능 사이트)
- <https://brunch.co.kr/@meenmo/14>
- <https://suhak.tistory.com/171>
- <https://learningaboutmyself.tistory.com/72>

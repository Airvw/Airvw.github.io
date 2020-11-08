---
layout: post
title: "정규 표현 다루기(python)"
tags:
- [파이썬 라이브러리 레시피]
- [정규 표현]
- [python]
---

## 참고자료
파이썬 라이브러리 레시피
[파이썬 공식문서](https://docs.python.org/3/library/re.html)
(https://support.google.com/a/answer/1371415?hl=ko)

## 정규 표현
패턴을 정의해서, 해당 패턴에 맞는 문자열을 찾거나 치환하는 등의 작업을 의미한다.  

## 메타 문자

문자 | 설명
:---- | :------
^ | 텍스트의 행 또는 문자열의 **시작부분**
$ | 텍스트의 행 또는 문자열의 **끝부분**
. | 새로운 행을 제외하고 모든 단일 문자를 매칭
\| | "또는"을 의미
\\ | 다음 문자가 특수 문자가 아닌 문자 그대로의 의미
\\w | 문자, 숫자 또는 밑줄(`a-z, A-Z, 0-9, _`)을 매칭
\\W | 문자, 숫자 또는 밑줄이 아닌 문자를 매칭
\\s | 공백 문자를 매칭
\\S | 공백 이외의 문자를 매칭
\\d | 0-9 사이의 숫자를 매칭
\\D | 0-9 사이의 숫자 외의 문자를 매칭합니다.

## 수량 한정자


## 함수
- re.compile(`pattern`, `flags=0`)
    - 정규 표현을 컴파일하여 정규 표현 객체를 반환  
    (정규표현을 객체로 바꿔서 사용)
    - ex) `prog = re.compile(pattern)`, `result = prog.match(string)`  
    - `pattern` : 정규 표현을 정의
    - `flags` : 특수한 동작을 설정(대소문자를 구별하지 않는다 등)
- re.seacrh(`pattern`, `string`, `flags=0`)
    - 정규 표현이 문자열에 일치하는지 확인
    - `pattern` : 정규 표현을 정의
    - `string` : 확인할 문자열
    - `flags` : 특수한 동작을 설정(대소문자를 구별하지 않는다 등)
- re.match(`pattern`, `string`, `flags=0`)
    - 정규 표현이 문자열에 일치하는지 확인. 단, 맨 앞글자부터 일치하는지 확인
    - `pattern` : 정규 표현을 정의
    - `string` : 확인할 문자열
    - `flags` : 특수한 동작을 설정
- re.fullmatch(`pattern`, `string`, `flags=0`)
    - 정규 표현이 문자열 전체와 일치하는지 확인
    - `pattern` : 정규 표현을 정의
    - `string` : 확인할 문자열
    - `flags` : 특수한 동작을 설정
- re.split(`pattern`, `string`, `maxsplit=0`, `flags=0`)
    - 문자열을 정규 표현에 일치하는 문장열로 분할. 반환은 list
    - `pattern` : 정규 표현을 정의
    - `string` : 확인할 문자열
    - `maxsplit` : 분할할 최대 개수
    - `flags` : 특수한 동작을 설정
- re.findall(`pattern`, `string` `flags=0`)
    - 문자열 안의 정규 표현에 일치한 문자열을 리스트로 반환
    - `pattern` : 정규 표현을 정의
    - `string` : 확인할 문자열
    - `flags` : 특수한 동작을 설정
- re.finditer(`pattern`, `string`, `flags=0`)
    - 문자열 안의 정규 표현에 일치한 객체를 반복자(iterator)로 반환  
    (일치하는 문자열의 시작, 끝 index를 파악할 때 쓰임)
    - `pattern` : 정규 표현을 정의
    - `string` : 확인할 문자열
    - `flags` : 특수한 동작을 설정

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
[plas님의 블로그](https://plas.tistory.com/72)  
[ednadev님의 블로그](https://velog.io/@ednadev/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC-re%EB%AA%A8%EB%93%88)

## 정규 표현
패턴을 정의해서, 해당 패턴에 맞는 문자열을 찾거나 치환하는 등의 작업을 의미한다.  

## 메타 문자

문자 | 설명
:---- | :------
^ | 텍스트의 행 또는 문자열의 **시작부분**
$ | 텍스트의 행 또는 문자열의 **끝부분**
r | 구성된 문자열 그대로를 의미
. | 새로운 행을 제외하고 모든 단일 문자를 매칭
\\ | 다음 문자가 특수 문자가 아닌 문자 그대로의 의미
\\w | 문자, 숫자 또는 밑줄(`a-z, A-Z, 0-9, _`)을 매칭
\\W | 문자, 숫자 또는 밑줄이 아닌 문자를 매칭
\\s | 공백 문자를 매칭
\\S | 공백 이외의 문자를 매칭
\\d | 0-9 사이의 숫자를 매칭
\\D | 0-9 사이의 숫자 외의 문자를 매칭합니다.

## 선택 패턴

문자 | 설명
:---- | :------
\| | "또는"을 의미
[...] | 대괄호속에 넣은 문자들 중에서 하나에 매칭
[^...] | 대괄호속에 넣은 문자들 제외해서 매칭

## 그룹

문자 | 설명
:---- | :------
() | 매칭 결과를 각 그룹별로 분리 가능

## 수량 한정자
앞에 문자에 대해 반복을 몇번 할 것인가, 또는 얼마나 허용할 것인가에 관한 규칙을 표현

문자 | 설명
:---- | :------
`X`? | `X`가 0번 또는 한번
`X`+ | `X`가 한번 이상
`X`* | `X`가 0번 이상
`X`{n} | `X`가 정확히 n번 반복
`X`{n, m} | `X`가 n번 이상, m번 이하


## 함수
- re.compile(`pattern`, `flags=0`)
    - 정규 표현을 컴파일하여 정규 표현 객체를 반환  
    (정규표현을 객체로 바꿔서 사용)
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

## 예제 

- r  
```python
a = 'abcdef\n'
b = r'abcdef\n'
print(a)
print(b)
```  
결과  
abcdef<br/><br/>abcdef\n

- re.compile()
```python
prog = re.compile(r"app\w")
prog.findall("application orange apple banana")
```  
결과  
["application", "apple"]

- ()
```python
g = re.search(r"(\w+)@(.+)", "test@gmail.com")
print(g.group(0))
print(g.group(1))
print(g.group(2))
```

- re.split()  
패턴을 구분자로 문자열을 나눠줌  
```python
a = re.split("[:., ]+", "apple orange:banana,tomato")
print(a)
```  
결과  
['apple', 'orange', 'banana', 'tomato']<br/><br/>
패턴을 구분자로 문자열을 나눠줌 (단, 구분자도 배열에 추가함)     
```python
a = re.split("([:., ])+", "apple orange:banana,tomato")
print(a)
```  
결과  
['apple', ' ', 'orange', ':', 'banana', ',', 'tomato']  
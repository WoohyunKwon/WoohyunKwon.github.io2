--- 
layout: post
title: "[MySQL] MySQL 특정 문자포함 검색 LIKE & REGEXP"
author: Woohyun Kwon
categories: SQL
tags: [SQL, MySQL, 사용자 정의 변수, LIKE, REGEXP]
---

## LIKE

`LIKE` 연산자는 특정 문자가 포함되어 있는 데이터를 검색 할때 사용한다.

- 특정 문자로 시작하는 데이터 검색

```mysql
SELECT [필드명] FROM [테이블명] WHERE [필드명] LIKE '특정 문자열%'
```

- 특정 문자로 끝나는 데이터 검색

```mysql
SELECT [필드명] FROM [테이블명] WHERE [필드명] LIKE '%특정 문자열'
```

- 특정 문자를 포함하는  데이터  검색

```mysql
SELECT [필드명] FROM [테이블명] WHERE [필드명] LIKE '%특정 문자열%'
```

다만 `LIKE` 연산자는 복수의 특정 문자로 시작/끝나거나 특정 문자를 포함하는 데이터를 검색하기엔 불편하다. 예를 들어 알파벳 모음(a,e,i,o,u)로 시작하는 단어만 포함시킨다 가정하자.

```mysql
SELECT [필드명] 
FROM [테이블명]
WHERE 
    [필드명] LIKE '%a' OR
    [필드명] LIKE '%e' OR
    [필드명] LIKE '%i' OR
    [필드명] LIKE '%o' OR
    [필드명] LIKE '%u'
```

이처럼 `LIKE`는 특정 문자열의 조건이 늘어날수록 쿼리가 상당히 지저분해지는 단점이 있다.


## REGEXP

`REGEXP`를 사용하면 `LIKE`를 이용한 검색과 달리 정규표현식(Regular Expression)을 활용하여 기본 연산자보다 복잡한 문자열 조건을 걸어 데이터를 검색할 수 있다.

### 정규표현식 Regular Expression

- 특정한 규칙을 가진 문자열의 집합을 표현하는데 사용하는 형식 언어
- 문자열을 처리하는 방법 중의 하나로, 특정한 조건의 문자를 ‘검색’하거나 ‘치환’하는 과정을 매우 간편하게 처리할 수    있도록 해주는 수단
- SQL부터 스크립트 언어까지 다양한 곳에서 활용될 수 있으며 Pattern을 사용해서 문자열을 처리
- 찾고자 하는 대상에서 정규표현식을 사용해 해당 Pattern과 일치하는 문자열 검색

정규 표현식은 `Pattern`을 사용해서 문자열을 처리한다. 찾을 대상문자열에서 정규 표현식을 사용해 해당 `Pattern`과 일치하는 문자열을 검색하는 것이다. `Pattern`과 일치하는 문자열을 찾은 이후 추출하거나 치환 할 수 있다.

### 정규표현식 Pattern

#### Matching

| Pattern	| Example | Explain | 
|:---------:|:----:|------|
| .	| ... | 길이가 세 글자 이상인 문자열만 검색 |
| `|` | a\|b | 조건 `a` or `b`에 해당하는 문자열 검색 | 
| OR | a OR b |  |
| [] | \[123\]d | 대상 문자열에서 ‘1d’ 또는 ‘2d’ 또는 ‘3d’인 문자열 검색 |
| `^` | ^안녕 | 대상 문자열에서 ‘안녕’으로 시작하는 문자열 검색 |
| $ | 니다$ | 대상 문자열에서 ‘니다’로 끝나는 문자열 검색 |

#### Numbers Limit

| Pattern	| Example | Explain | 
|:---------:|:----:|------|
| \* |	a*n | **a**가 **n**번 이상 등장하는 문자열 검색 |
| + | 국+ |	‘국’이 1번 이상 등장하는 문자열 검색 |
| {m,n} | 치{m,n} |	‘치’가 m회 이상 n회 이하 반복하는 문자열 검색 |
| ? | [가나다]? |‘가’ 또는 ‘나’ 또는 ‘다’가 0~1회 등장하는 문자열 검색 |

#### String Group

| Pattern	| Example | Explain | 
|:---------:|:----:|------|
| [A-z] |  [A-z]+ |	대상 문자열에서 알파벳이 한 개 이상인 문자열을 찾음 |
| [:alpha:] |  |  |
| \a |  |  |
| [0-9] | ^[0-9]+ |	한 개 이상의 숫자로 시작하는 문자열 검색 |
| [:digit:] |  |  |
| \d |  |  |

#### Not

| Pattern	| Example | Explain | 
|:---------:|:----:|------|
| [^문자] | [^사람] | ‘사’ 또는 ‘람’을 포함하지 않는 문자열 검색 |


## References

- [gillog, \[MySQL\] REGEXP(Regular Expression(정규 표현식))](https://velog.io/@gillog/MySQL-REGEXPRegular-Expression%EC%A0%95%EA%B7%9C-%ED%91%9C%ED%98%84%EC%8B%9D)
- [코딩하는금융인, \[MySQL\] 정규표현식 검색하기 REGEXP, LIKE](https://codingspooning.tistory.com/entry/MySQL-정규표현식-검색하기-REGEXP-LIKE)
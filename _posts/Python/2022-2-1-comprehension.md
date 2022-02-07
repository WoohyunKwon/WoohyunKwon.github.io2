--- 
layout: post
title: "[Python] 파이썬 컴프리헨션(Comprehension) & 제너레이터(Generator)"
author: Woohyun Kwon
categories: Python
tags: [Python, 파이썬, 컴프리헨션, Comprehension, generator, 제너레이터, iterable, iterator]
use_math: true
---

## Iterable

`iterable` 객체는 반복 가능한 객체를 말하며, sequence type인 `list`, `dict`, `set`, `str`, `tuple`, `range`가 대표적이다.

## Iterator

`iterator` 객체는 값을 차례대로 꺼낼 수 있는 객체이다. `iterator`는 `iterable`한 객체를 내장함수 또는 `iterable` 객체의 메소드로 객체를 생성할 수 있다. 파이썬 내장함수 `iter()`를 사용해 iterator 객체를 만들 수 있다.

## 컴프리헨션(Comprehension)

파이썬에서는 하나 이상의 이터레이터(iterator)로부터 파이썬의 자료구조(`list`, `set`, `dictionary`, `tuple`)을 보다 간단하게 작성할 수 있는 `컴프리헨션`이라는 문법을 지원한다.

## List Comprehension

리스트를 생성하는 컴프리헨션을 리스트 컴프리헨션(List Comprehension)이라고 한다. 리스트 컴프리헨션을 통해 1~100까지 정수 리스트를 생성하는 방법은 다음과 같다.

```python
<기본 for 문>
numlst = []
for i in range(1,11):
    numlst.append(i)
# 결과: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

<리스트 컴프리헨션>
[i for i in range(1,11)]
# 결과: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### 조건문: 여러 반복문 

다음은 여러 반복문이 사용된 예이다.

```python
[i*j for i in range(1,4) for j in ['A','B','C']]
# 결과: ['A', 'B', 'C', 'AA', 'BB', 'CC', 'AAA', 'BBB', 'CCC']
```

### 조건문: if

if문은 for문의 오른쪽, if-else문은 for문의 왼쪽에 사용해야한다.

1~20까지의 정수 중 짝수만 출력하는 예를 보면 다음과 같다.

```python
[i for i in range(1,21) if i%2 == 0]
# 결과: [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

### 조건문: if-else

if문은 for문의 오른쪽, if-else문은 for문의 왼쪽에 사용해야한다.

1~10까지의 정수 중 \<if 짝수이면 출력 else 아니면 'X' 출력\>하는 예를 보자.

```python
[i if i%2==0 else 'X' for i in range(1,11)]
# 결과: ['X', 2, 'X', 4, 'X', 6, 'X', 8, 'X', 10]
```

컴프리헨션에서 elif를 바로 사용할 수는 없지만 if-else를 통해 표현할 수 있다.

1~20까지의 정수 중 \<if 짝수이면 출력 elif 9이면 출력 else 아니면 'X' 출력\>하는 예를 보자.

```python
[i if i%2==0 else i if i==9 else 'X' for i in range(1,11)]
# 결과: ['X', 2, 'X', 4, 'X', 6, 'X', 8, 9, 10]
```

## Set Comprehension

리스트 컴프리헨션과 만드는 방법은 거의 동일하며 대괄호(`[]`)대신 중괄호(`{}`)를 이용하면 셋 컴프리헨션이 된다.

```python
<List Comprehension>
[x+y for x in range(5) for y in range(5)]
# 결과: [0, 1, 2, 3, 4, 1, 2, 3, 4, 5, 2, 3, 4, 5, 6, 3, 4, 5, 6, 7, 4, 5, 6, 7, 8]

<Set Comprehension>
{x+y for x in range(5) for y in range(5)}
# 결과: {0, 1, 2, 3, 4, 5, 6, 7, 8}
```

## Dictionary Comprehension

`{key: value}`의 형태를 이용하면 `Dictionary Comprehension`을 만들 수 있다.

```python
name = ['철수','영희','길동','순희']
score = [55, 60, 90, 70]

<이름과 점수>
{i:j for i,j in zip(name,score)}
# 결과: {'길동': 90, '순희': 70, '영희': 60, '철수': 55}

<이름과 pass/fail>
{i:'pass' if j >= 60 else 'fail' for i,j in zip(name,score)}
# 결과: {'길동': 'pass', '순희': 'pass', '영희': 'pass', '철수': 'fail'}
```

## Tuple Comprehension / Generator

소괄호(`()`)를 쓰면 튜플 컴프리헨션이 만들어질까? 결과적으로 `generator`가 만들어진다.

```python
(x for x in range(1,11))
# 결과: <generator object <genexpr> at 0x7f57bf54e8d0>
```

제너레이터(Generator)는 이터레이터(Iterator)를 생성해주는 함수이다. 이터레이터는 클래스에 `__iter__`, `__next__` 또는 `__getitem__` 메서드를 구현해야 하지만 제너레이터는 함수 안에서 `yield`라는 키워드만 사용하면된다. 그래서 제너레이터는 이터레이터보다 훨씬 간단하게 작성할 수 있다.

## References

- [위키독스, 제대로 파이썬](https://wikidocs.net/22800)
- [위키독스, 파이썬 - 기본을 갈고 닦자!](https://wikidocs.net/16069)
- [위키독스, 레벨업 파이썬](https://wikidocs.net/74399)
- [위키피디아, generator](https://en.wikipedia.org/wiki/Generator_(computer_programming))
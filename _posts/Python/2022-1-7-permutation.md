--- 
layout: post
title: "[Python] 파이썬 순열, 조합, 중복순열, 중복조합 구현하기"
author: Woohyun Kwon
categories: Python
tags: [Python, 파이썬, 순열, 조합, 중복순열, 중복조합, permutation, combination]
---

## 조합(combination)

`조합(combination)`이란 서로 다른 $n$개의 원소에서 $k$개의 원소를 순서에 상관없이 선택하는 방법의 가짓수를 말하며, 그 값은 다음과 같다:

$$nCk = {n \choose k} = {n! \over k!(n-k)!}$$

### 파이썬 조합 구현: `itertools.combinatios`

`itertools` 라이브러리의 `combinations`을 사용하면 조합을 구할 수 있다.

```python
<기본형>
from itertools import combinations

print(list(combinations('뽑을 리스트', '뽑을개수')))

<예제>
from itertools import combinations

print(list(combinations(['A', 'B', 'C'], 2)))

<결과>
[('A', 'B'), ('A', 'C'), ('B', 'C')]
```

## 순열(permutation)

`순열(permutation)`이란 $n$개의 원소에서 $k$개의 원소를 골라 배열하는 방법의 가짓수을 말하며, 그 값은 다음과 같다:

$$nPk=P(n,k)=n(n-1)...(n-k+1)$$

### 파이썬 순열 구현: `itertools.permutaions`

`itertools` 라이브러리의 `permutations`을 사용하면 순열을 구할 수 있다.

```python
<기본형>
from itertools import permutations

print(list(permutations('뽑을 리스트', '뽑을개수')))

<예제>
from itertools import permutations

print(list(permutations(['A', 'B', 'C'], 2)))

<결과>
[('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
```

## 중복조합(combinations with replacement)

중복조합(combinations with replacement)은 서로 다른 $n$개의 원소에서 중복을 허락하여 $k$개를 뽑는 경우를 말하며, 기호로는 다음과 같이 쓴다:

$$nHk=_{k+(n-1)}{C}_{k}={k+(n-1) \choose k}$$

### 파이썬 중복조합 구현: `itertools.combinations_with_replacement`

```python
<기본형>
from itertools import combinations_with_replacement

print(list(combinations_with_replacement('뽑을 리스트', '뽑을개수')))

<예제>
from itertools import combinations_with_replacement

print(list(combinations_with_replacement(['A', 'B', 'C'], 2)))

<결과>
[('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]
```

## 중복순열(permutation with repetition)

중복순열(permutation with repetition)은 $n$개의 원소 중에 중복이 가능하게 $k$개를 골라서 순서 있게 나열한 것을 말하며, $n^k$개의 가짓수가 있다.

### 파이썬 중복순열 구현: `itertools.product`

```python
<기본형>
from itertools import product

print(list(product('뽑을 리스트', '뽑을 리스트', ...)))

<예제>
from itertools import product

print(list(product(['A', 'B', 'C'], ['A', 'B', 'C'])))

<결과>
[('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('C', 'A'), ('C', 'B'), ('C', 'C')]
```

## References

- [위키백과, 순열](https://ko.wikipedia.org/wiki/%EC%88%9C%EC%97%B4#%EC%A4%91%EB%B3%B5_%EC%88%9C%EC%97%B4)
- [위키백과, 조합](https://ko.wikipedia.org/wiki/%EC%A1%B0%ED%95%A9)
- [maengjh, (Python) 순열, 조합, 중복순열, 중복조합 쉽게 구현하기](https://juhee-maeng.tistory.com/91)
- [쌍쌍바나나, 파이썬 (Python)에서 리스트에 있는 값들의 모든 조합을 구하기](https://ourcstory.tistory.com/414)
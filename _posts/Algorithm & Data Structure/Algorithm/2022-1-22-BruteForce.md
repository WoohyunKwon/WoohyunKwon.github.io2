--- 
layout: post
title:  "[Algorithm] 브루트 포스 Brute force"
categories: "Algorithm"
tags: [알고리즘, algorithm, 브루트 포스, Brute force]
use_math: true
---

## 브루트 포스(Brute force)란?

조합 가능한 모든 문자열을 하나씩 대입해 보는 방식으로 암호를 해독하는 방법이다. 브루트 포스는 완전 대입 또는 무차별 대입이라고 말하기도 한다. 일반적으로 브루트 포스의 시간 복잡도는 $O(n!)$ 또는 $O(2^n)$이다.

## 특징

모든 경우를 탐색하기 때문에 항상 정확도는 100%이지만, 시간 복잡도(time complex)에 매우 민감하다. 

다음은 비밀번호 길이에 따른 암호를 풀기위해 비밀번호를 대입하는 경우의 수를 나타내는 표이다.

| 비밀번호 길이 | 영문+숫자 경우의수 | 특수문자포함 경우의 수 |
|--------------|---------|-----------|
| 6 | 61,474,519 | 156,238,908
| 7 | 491,796,152 | 1,473,109,704
| 8 | 3,381,098,545 | 11,969,016,345
| 9 | 20,286,591,270 | 85,113,005,120
| 10 | 107,518,933,731 | 536,211,932,256
| 11 | 508,271,323,092 | 3,022,285,436,352

참고로 파이썬에서 6자리의 영문+숫자로 구성된 비밀번호의 경우 브루트 포스 방식으로 푸는데 걸리는 시간은 파이썬일 경우 약 4분(240초), C언어로는 약 2초만에 풀 수 있다.

## References

- [나무위키, 브루트포스](https://namu.wiki/w/%EB%B8%8C%EB%A3%A8%ED%8A%B8%20%ED%8F%AC%EC%8A%A4)
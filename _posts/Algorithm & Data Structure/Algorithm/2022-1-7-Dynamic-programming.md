--- 
layout: post
title:  "[Algorithm] 동적 계획법 Dynamic Programming"
categories: "Algorithm"
tags: [알고리즘, algorithm, 동적계획법, dynamic programming]
---

## 동적 계획법(dynamic programming)이란?

`동적 계획법(dynamic programming)`이란 복잡한 문제를 간단한 여러 개의 문제로 나누어 푸는 방법을 말한다. 이것은 부분 문제 반복과 최적 부분 구조를 가지고 있는 알고리즘을 일반적인 방법에 비해 메모리 공간을 더 사용하지만 빠른 시간 내에 연산을 할 수 있다.

## 예제

동적 계획법의 대표적인 예로는 `피보나치 수열(Fibonacci numbers)`이 있다. 피보나치 수열은 첫항과 둘째 항의 값이 1이며, 이어지는 항은 바로 앞 두 항의 합인 수열이다. 첫째항부터 순서대로 1, 1, 2, 3, 5, 8, ...이 되며 **피보나치 수** $F_n$은 다음과 같은 점화식으로 나타낼 수 있다.

$F_1 = F_2 = 1$

$F_n = F_{n-1} + F_{n-2}$, $n \in \{3, 4,...\}$

이런 피보나치 수열을 다음과 같은 트리 형태로 소분하게 되면 동적 계획법에 맞게 부분 문제(subproblem)가 상위 문제를 해결하는 것을 볼 수 있다.

![피보나치 수열 트리](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb2OF5h%2FbtqRAjvzuO5%2FeJtAFf5D7bQ9WKLGca4aR1%2Fimg.png)

**피보나치 수열의 파이썬 코드는 다음과 같다**

```python
def fib(n):
  if n == 0:
    return 0
  elif n == 1:
    return 1
  else:
    return fib(n-1) + fib(n-2)
```

## References

- [위키백과, 동적 계획법](https://ko.wikipedia.org/wiki/%EB%8F%99%EC%A0%81_%EA%B3%84%ED%9A%8D%EB%B2%95)
- [위키백과, 피보나치수](https://ko.wikipedia.org/wiki/%ED%94%BC%EB%B3%B4%EB%82%98%EC%B9%98_%EC%88%98)
- [sh9404, \[알고리즘\] Dynamic programming (동적 계획법) 완전정복 with Python](https://lsh424.tistory.com/76)
--- 
layout: post
title: "[Mathemarics] 유클리드 호제법 Euclidean Algorithm"
author: Woohyun Kwon
categories: Mathematics
tags: [Python, 파이썬, 알고리즘, 유클리드 호제법, Euclidean Algorithm, 정수론, Number Theory, 대수학, Algebra]
---

## 유클리드 호제법 Euclidean Algorithm

유클리드 호제법(Euclidean algorithm) 또는 유클리드 알고리즘은 2개의 양의 정수 또는 두 다항식의 최대공약수를 구하는 알고리즘의 하나이다. 정수에 대한 유클리드 호제법은 다음의 정리에 기인한다.

$\forall a, b, r \in \mathbb{Z}$, $a$를 $b$로 나눈 나머지를 $r$라 하자(단, $0 \le r<b\le a$). $gcd(a,b)$가 두 정수 $a$, $b$의 최대공약수(greatest common divisor)라 하면 다음식이 성립한다.

$$gcd(a,b) = gcd(b,r). $$

## 증명

$\forall a, b\in \mathbb{Z}$일 때, $a \ge b$라 하자. 그러면 $a=bq+r$를 만족하는 유일한 정수 $q,r$($0 \le r < b$)이 존재한다. $gcd(a,b)=G$를 만족하는 $G$가 존재한다면,

$$a=Gu,\ b=Gv$$

를 만족하는 서로 다른 두 정수 $u,v$가 존재하며 $u$와 $v$는 서로소이다.

$$
\begin{matrix}
a   &=& bq+r \\
Gu  &=& Gvq + r \\
r   &=& G(u-vq)
\end{matrix}
$$

따라서 $r$은 $G$의 배수이다. 

이제 $r=Gt\ (t \in \mathbb{Z})$라 하자. $gcd(v,t)=G'>1$, $v=G'v'$, $t=G't'$를 만족하는 $G', v', t'$이 존재한다 가정하자. 그러면,

$$
\begin{matrix}
a   &=& bq+r \\
Gu  &=& Gvq + Gt \\
    &=& GG'v'q + GG't' \\
    &=& GG'(v'q+t') \\
u   &=& G'(v'q+t')
\end{matrix}
$$

이므로 $u$는 $G'$의 배수이므로 $u$와 $v$는 서로소라는 사실에 모순이 된다. 따라서 $(b,r)=G$이고,

$$gcd(a,b) = gcd(b,r)$$

를 만족한다.

## 활용

### 최대공약수

이 알고리즘은 두 정수의 최대공약수를 구할 때 쓸 수 있다. 파이썬에서는 반복문과 재귀문을 사용하여 이를 활용할 수 있다.

**반복문**

```python
def gcd(a,b): # a = bq + r
    while b != 0:
            r = a % b
            a = b
            b = r
    return a
```

**재귀문**

```python
def gcd(a,b):
  while b:
    a, b = b, a % b
  return a
```

## 출처

- [Wolfram, Euclidean Algorithm](https://mathworld.wolfram.com/EuclideanAlgorithm.html)
- [위키백과, 유클리드 호제법](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)
- [나무위키, 유클리드 호제법](https://namu.wiki/w/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C%20%ED%98%B8%EC%A0%9C%EB%B2%95)
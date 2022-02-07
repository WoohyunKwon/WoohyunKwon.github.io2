--- 
layout: post
title: "[MySQL] MySQL HAVING vs WHERE 비교"
author: Woohyun Kwon
categories: SQL
tags: [SQL, MySQL, HAVING, WHERE, 처리순서]
---

## WHERE vs HAVING

`MySQL`내에서 함수들의 내부처리 순서는 `WHERE - GROUP BY - HAVING - SELECT - ORDER BY`이다.
- `WHERE` 구로 행을 검색하는 처리가 `GROUP BY`로 그룹화하는 처리보다 순서상 앞서기 때문에 `GROUP BY`로 그룹화한 값을 사용할 수 없다. 
- `HAVING` 구는 `GROUP BY` 뒤에 위치하여 `WHERE` 구와 동일하게 조건식을 지정할 수 있으며 `GROUP BY`보다 나중에 처리하므로 `GROUP BY`로 그룹화한 값을 사용할 수 있다.

프로그래머스에서 가져온 [입양 시각 구하기(1)](https://programmers.co.kr/learn/courses/30/lessons/59412) 문제를 통해 차이를 확인해보자.

## 문제 설명

ANIMAL_OUTS 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. ANIMAL_OUTS 테이블 구조는 다음과 같으며, ANIMAL_ID, ANIMAL_TYPE, DATETIME, NAME, SEX_UPON_OUTCOME는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다.

| NAME |	TYPE |	NULLABLE |
|:----:|:-------:|:---------:|
| ANIMAL_ID	| VARCHAR(N)	| FALSE | 
| ANIMAL_TYPE	| VARCHAR(N)	| FALSE | 
| DATETIME	| DATETIME	| FALSE | 
| NAME	| VARCHAR(N)	| TRUE | 
| SEX_UPON_OUTCOME	| VARCHAR(N)	| FALSE | 

보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. 09:00부터 19:59까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.

## 결과

SQL문을 실행하면 다음과 같이 나와야 합니다.

| HOUR	| COUNT| 
|:-----:|:----:|
| 9	| 1
| 10	| 2
| 11	| 13
| 12	| 10
| 13	| 14
| 14	| 9
| 15	| 7
| 16	| 10
| 17	| 12
| 18	| 16
| 19	| 2

## 코드 1: HAVING

```mysql
SELECT 
    HOUR(DATETIME) AS HOUR, 
    COUNT(HOUR(DATETIME)) AS COUNT
FROM ANIMAL_OUTS
GROUP BY HOUR(DATETIME) # DATETIME 열의 값들을 시간별로 묶는다
HAVING HOUR > 8 AND HOUR < 20 # 9시부터 19시까지만 출력
ORDER BY HOUR(DATETIME) # 시간순으로 정렬
```

<span style="color: #2D3748; background-color:#fff5b1;">
처리 순서: FROM - GROUP BY - HAVING - SELECT - ORDER BY
</span>

- `FROM`을 통해 `ANIMAL_OUTS` 데이터를 불러온다.
- `GROUP BY`를 통해 시간만 추출한 `HOUR(DATETIME)` 열의 값들을 시간별로 묶는다.
  - `DATETIME` 열의 데이터 형태는 **DATETIME**이며, **DATETIME** 형태의 데이터에서 시간만 추출하기위해 `HOUR`를 사용한다.
- `HAVING`을 통해 `GROUP BY`로 그룹화한 `HOUR(DATETIME)`의 데이터 중 9시부터 19시까지의 시간대만 표시한다.
- `SELECT`로 `HOUR(DATETIME)`, `COUNT(HOUR(DATETIME))` 열만 선택한다.
  - `COUNT`로 `HOUR(DATETIME)`에 따른 값의 수를 계산한다.
  - `AS`로 `HOUR(DATETIME)` 열의 이름을 `HOUR`로 하며, `COUNT(HOUR(DATETIME))`열의 이름은 `COUNT`로 한다.
  - <span style="color: #2D3748; background-color:#fff5b1;">참고</span> `HAVING HOUR(DATETIME) > 8 AND HOUR(DATETIME) < 20`을 사용하면 에러가 발생한다. 이유는 앞서 처리된 `SELECT` 구에서 `HOUR(DATETIME) AS HOUR`을 통해 `HOUR(DATETIME)` 열의 이름을 `HOUR`로 바꿨기 때문에 `HAVING`이 참조할 `HOUR(DATETIME)` 열이 존재하지 않기 때문이다.
- `ORDER BY`로 `HOUR(DATETIME)` 데이터를 시간순으로 정렬한다. 기본값은 오름차순이며 `DESC`를 붙이면 내림차순이 된다.

## 코드 2 WHERE

이번 문제의 경우 `WHERE`을 사용하면 다음과 같다.

```mysql
SELECT 
    HOUR(DATETIME) AS HOUR, 
    COUNT(HOUR(DATETIME)) AS COUNT
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) > 8 AND HOUR(DATETIME) < 20
GROUP BY HOUR(DATETIME) # DATETIME 열의 값들을 시간별로 묶는다
ORDER BY HOUR(DATETIME) # 시간순으로 정렬
```

<span style="color: #2D3748; background-color:#fff5b1;">
처리 순서: FROM - WHERE - GROUP BY - SELECT - ORDER BY
</span>

- `FROM`을 통해 `ANIMAL_OUTS` 데이터를 불러온다.
- `WHERE`을 통해 시간만 추출한 `HOUR(DATETIME)` 데이터 중 9시부터 19시까지의 시간대만 표시한다.
  - <span style="color: #2D3748; background-color:#fff5b1;">참고</span> `WHERE HOUR > 8 AND HOUR < 20`을 사용하면 에러가 발생한다. 이유는 `WHERE`구가 `SELECT`보다 처리 순서가 빨라서 `SELECT`구의 `HOUR(DATETIME) AS HOUR`이 실행되기 전이기 때문에 `HOUR`가 없기 때문이다.
- `GROUP BY`를 통해 `WHERE`로 제한된(9~19시) 시간만 추출한 `HOUR(DATETIME)` 열의 값들을 시간별로 묶는다.
- `SELECT`로 전체 데이터 중 `HOUR(DATETIME)`, `COUNT(HOUR(DATETIME))` 열만 선택한다.
  - `COUNT`로 `HOUR(DATETIME)`에 따른 값의 수를 계산한다.
  - `AS`로 `HOUR(DATETIME)` 열의 이름을 `HOUR`로 하며, `COUNT(HOUR(DATETIME))`열의 이름은 `COUNT`로 한다.
- `ORDER BY`로 `HOUR(DATETIME)` 데이터를 시간순으로 정렬한다. 기본값은 오름차순이며 `DESC`를 붙이면 내림차순이 된다.




## References

- [프로그래머스, 입양 시각 구하기 1](https://programmers.co.kr/learn/courses/30/lessons/59412)
- [MySQL 기초 정리](https://woohyunkwon.github.io/sql/2021/12/27/MySQL-FS.html#h-%EC%A0%95%EB%A0%AC)
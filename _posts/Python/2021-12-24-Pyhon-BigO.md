--- 
layout: post
title: "[Python] 파이썬 주요 연산자의 시간 복잡도 (Big-O)"
subtitle: How to make title
    # 포스트의 제목을 큰 따옴표로 적어 준다. 이 title을 적어주지 않으면 .md 파일 이름으로 적어주었던 title 부분이 제목으로 업로드 된다.
excerpt: "md 파일에 마크다운 문법으로 작성하여 Github 원격 저장소에 업로드 해보자. 에디터는 Visual Studio code 사용! 로컬 서버에서 확인도 해보자. "
    # 포스트 목록에서 보여지는 블로그 소개 글로 들어가는 것 같다.
author: Woohyun Kwon
categories: Python
tags: [Python, 파이썬, Big-O, O(n), 복잡도, 시간복잡도, 알고리즘, 자료구조]

# date: 2021-12-24 # 글을 처음 작성한 날짜. yyyy-mm-dd 형식으로 작성했다.
# last_modified_at: 2021-12-24 # 이 글을 수정한 날짜.
---

## 시간 복잡도(Time Complexity)

시간 복잡도는 입력값과 연산 수행 시간의 상관관계를 나타내는 척도이다. 일반적으로 시간 복잡도는 점근 표기법을 이용하여 나타내며, 알고리즘의 시간복잡도는 주로 빅오(Big-O) 표기법을 사용하여 나타낸다.


![Time-Complexity](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbMi9Ge%2FbtqCinZoy5c%2FGBOJgXYNHcEof0UWZkVZLK%2Fimg.png)
출처: https://chancoding.tistory.com/43

## List

| Operation | Example  | Time | Notes |
| --------- | -------- | ----- | ----- |
| Index | l[i]	| O(1)	| 인덱스로 값 찾기 | 
| Store	| l[i] = 0	| O(1)	| 인덱스로 데이터 저장 |
| Length | len(l)	| O(1)	| 리스트 길이 | 
| Append | l.append(5)	| O(1)	| 리스트 뒤에 데이터 저장 | 
| Pop	| l.pop()	| O(1)	| 가장 뒤의 데이터 pop | 
| Clear	| l.clear()	| O(1)	| l = [] | 
| Slice	| l[a:b] | O(b-a) | 슬라이싱되는 요소들 수 만큼 비례 |
| Extend | l.extend(...) | O(len(...)) | 확장되는 길이만큼 | 
| Construction | list(...) | O(len(...)) | 리스트 길이만큼 | 
| check ==, != | l1 == l2 | O(n) | 전체 리스트가 동일한지 확인
| Insert | l[a:b] = ... | O(n) | 데이터 삽입
| Delete | del l[i] | O(n) | 데이터 삭제
| Containment | x in/not in l | O(n) | 포함 여부 확인
| Copy | l.copy() | O(n) | 복제
| Remove | l.remove(...) | O(n) | 제거
| Pop | l.pop(i) | O(n) | 제거된 값 이후를 전부 한칸씩 당겨줘야함
| Extreme value | min(l)/max(l) | O(n) | 전체 데이터를 확인해야함
| Reverse | l.reverse() | O(n) | 뒤집기
| Iteration | for v in l: | O(n) | 전체 데이터 확인하므로
| Sort | l.sort() | O(n Log n) | 파이썬 기본 정렬 알고리즘
| Multiply	| k*l | O(kn) | 리스트의 곱은 리스트 개수 늘어남

## Dictionary

| Operation | Example  | Time | Notes |
| --------- | -------- | ----- | ----- |
| Store | d[k] = v | O(1) | 데이터 저장 | 
| Length | len(d) | O(1) | 길이 출력 | 
| Delete | del d[k] | O(1) | 요소 제거 | 
| get/setdefault | d.get(k) | O(1) | key에 따른 value 확인 | 
| Pop | d.pop(k) | O(1) | pop | 
| Pop item | d.popitem() | O(1) | 랜덤하게 선택해서 pop | 
| Clear | d.clear() | O(1) | similar to s = {} or = dict() | 
| View | d.keys() | O(1) | same for d.values() / 키값 전체 확인 | 
| Construction | dict(...) | O(len(...)) | (key, value) 튜플 개수만큼 | 
| Iteration | for k in d: | O(N) | 전체 딕셔너리 순회 | 

## Set

| Operation | Example  | Time | Notes |
| --------- | -------- | ----- | ----- |
| Add | s.add(5) | O(1) | 집합 요소 추가
| Containment | x in/not in s | O(1) | 포함 여부 확인
| Remove | s.remove(..) | O(1) | 요소 제거
| Discard | s.discard(..) | O(1) | 특정 요소 제거
| Pop | s.pop() | O(1) | 랜덤하게 하나 pop
| Clear | s.clear() | O(1) | similar to s = set()
| Construction | set(...) | O(len(...)) | 길이만큼
| check ==, != | s != t | O(len(s)) | 전체 요소 동일 여부 확인 |
| <=/< | s <= t | O(len(s)) | 부분집합 여부 |
| >=/> | s >= t | O(len(t)) | 부분집합 여부 |
| Union | s, t | O(len(s)+len(t)) | 합집합 |
| Intersection | s & t | O(len(s)+len(t)) | 교집합
| Difference | s - t | O(len(s)+len(t)) | 차집합
| Symmetric Diff | s ^ t | O(len(s)+len(t)) | 여집합
| Iteration | for v in s: | O(N) | 전체 요소 순회
| Copy | s.copy() | O(N) | 복제

## References

- [위키백과, 시간복잡도](https://ko.wikipedia.org/wiki/%EC%8B%9C%EA%B0%84_%EB%B3%B5%EC%9E%A1%EB%8F%84)
- [파이썬 자료형 및 연산자의 시간 복잡도(Big-O) 총 정리](https://chancoding.tistory.com/43)
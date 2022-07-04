---
title: "기지국 설치"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, saw discussion]

toc: true

date: 2022-07-01
last_modified_at: 2022-07-01
---

## **문제 링크**
[Question Link](https://programmers.co.kr/learn/courses/30/lessons/12979)

<br>

---
---
 
## **CODE 1**: WA - 시간 초과!
### <u>날짜</u> 2022-07-01
#### <u>총 소요시간</u> 40m

<br>

#### <u>설계</u>
```python
'''
기지국을 최소로 설치
하나의 기지는 w+1개의 아파트에 전파를 전달할 수 있음

greedy하게 해야 하나?
16-5 = 11
11%5 = 2 + 1

현재 전파가 전달되고 있지 않은 아파트의 개수를 구하기
1. 각 station의 처음 아파트 - 끝 아파트를 구하기
2. 1을 시작점 기준으로 오름차순 정렬
스택에 첫 원소를 넣기
[3, 5] [4, 6]
[3, 6] [4, 5]
a1 b1      a2 b2
os oe(스택) ns ne (새)
ns < oe인 경우 a와 b의 일부가 겹쳐짐 -> 스택 안에 있는 원소의 b값을 새로운 원소의 b값으로 교체
ne < oe인 경우 a가 b 안에 들어감 -> 스택 안에 있는 원소를 유지하고 아무것도 넣지 않는다.
b1 < a2인 경우 전혀 관계가 없음 -> 스택에 원소를 넣는다.
3. 스택을 쭉 따라가면서 이미 전파가 있는 아파트의 개수를 구하기
4. 전파가 없는 아파트의 개수를 구하고 그 개수를 w*2+1로 나눈 몫과 나머지를 더하기
'''
```

<br>

#### <u>코드</u>
```python
def solution(n, stations, w):
    
    border = [[station-w, station+w] for station in stations]
    border.sort(key=lambda x: x[0])
    
    stack = []
    stack.append(border[0])
    border = border[1:]
    
    for ns, ne in border:
        os, oe = stack[-1]
        if oe < ns:
            stack.append([ns, ne])
        elif ns <= oe <= ne:
            stack[-1][1] = ne
        
    checked = 0
    for s, e in stack:
        checked += (e - s + 1)
    
    unchecked = n - checked
    return sum(divmod(unchecked, w*2+1)) 
        
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://deeppago.tistory.com/101)

greedy하게 푸는 방법은 맞는데
전파가 안 닿는 구간들을 구한 다음 구간별로 // (w*2+1) + 1 값을 누적해서 더해주는 방식

나는 구간을 고려하지 않아서 실패했던 것

---
---

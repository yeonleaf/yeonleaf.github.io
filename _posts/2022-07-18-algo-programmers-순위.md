---
title: "순위"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, complete success]

toc: true

date: 2022-07-18
last_modified_at: 2022-07-18
---

## **문제 링크**
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/49191)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-07-18
#### <u>총 소요시간</u> 40m

<br>

#### <u>설계</u>
```python
'''
연결 행렬
ij ji 기록하기 (ij는 1, ji는 -1)
ij가 없을 때
i k이 있고 k j가 있을 때 (k의 범위는 1, n+1로 잡되 i == k or k == j인 경우 continue)
ik == -1 and kj == -1 -> ij = -1
ik == 1 and kj == 1 -> ij = 1
이렇게 두 가지 경우에만 확정지을 수 있음

저걸 다 하고 adj[i]에 0이 하나만 있는 경우 순위를 확정지음 -> 카운트 1
'''
```

<br>

#### <u>코드</u>
```python
def solution(n, results):
    
    adj = [[0]*(n+1) for _ in range(n+1)]
    
    for w, l in results:
        adj[w][l] = 1
        adj[l][w] = -1
    
    for i in range(1, n+1):
        for j in range(1, n+1):
            if i == j:
                continue
            if not adj[i][j] or not adj[j][i]:
                for k in range(1, n+1):
                    if i == k or k == j:
                        continue
                    if adj[i][k] == -1 and adj[k][j] == -1:
                        adj[i][j] = -1
                        adj[j][i] = 1
                    elif adj[i][k] == 1 and adj[k][j] == 1:
                        adj[i][j] = 1
                        adj[j][i] = -1
                        
    answer = 0                       
    for i in range(1, n+1):
        zero = 0
        for j in range(1, n+1):
            if adj[i][j] == 0:
                zero += 1
        if zero == 1:
            answer += 1
    return answer
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://it-garden.tistory.com/247)

플로이드 워셜 알고리즘 복습

3중 for문을 사용해서 i에서 k를 거치고 k에서 j을 거치는 경로가 이전에 구했던 ij보다 작은 경우에만 값을 갱신한다.

---
---

<br>

#### <b> ✅ 최종 comment </b>
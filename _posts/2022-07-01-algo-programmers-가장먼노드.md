---
title: "가장 먼 노드"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, need practice]

toc: true

date: 2022-07-01
last_modified_at: 2022-07-01
---

## **문제 링크**
[Question Link](https://programmers.co.kr/learn/courses/30/lessons/49189)

<br>

---
---
 
## **CODE 1**: 통과
### <u>날짜</u> 2022-07-01
#### <u>총 소요시간</u> 50m

<br>

#### <u>설계</u>
```python
'''
연결 행렬을 그린다.
1번 노드를 시작으로 방문 체크를 하면서 bfs한다.
더 이상 갈 노드가 없으면 카운팅한다.
''' 
```

<br>

#### <u>코드</u> -> 시간 초과
```python
from collections import deque
def solution(n, edge):
    
    graph = [[0]*n for _ in range(n)]
    
    for sn, en in edge:
        sn, en = sn-1, en-1
        graph[sn][en] = 1
        graph[en][sn] = 1
    
    v = [[0]*n for _ in range(n)]
    q = deque()
    q.append((0, 0))
    v[0][0] = 1
    
    dic = dict()

    while q:
        node, ecnt = q.popleft()
        
        if node in dic:
            dic[node] = min(dic[node], ecnt)
        else:
            dic[node] = ecnt
            
        for nxt in range(n):
            if graph[node][nxt] and not v[node][nxt]:
                v[node][nxt] = 1
                v[nxt][node] = 1
                q.append((nxt, ecnt+1))
                
    res = 0
    maxEdge = max(dic.values())
    for v in dic.values():
        if v == maxEdge:
            res += 1
        
    return res
```

#### <u>코드</u> -> 통과

[document](https://programmers.co.kr/questions/21417)

인접 행렬이 아니라 리스트를 쓰는 것이 시간을 절약할 수 있다.
인접 행렬은 특정 값에 대한 접근 속도가 빠르지만 어떤 정점에서 이어진 모든 정점을 탐색하려면 한 줄의 배열을 모두 탐색해야 한다.
인접리스트는 어떤 정점에서 이어진 모든 정점을 빠르게 탐색할 수 있지만 특정 값에 접근하기 위해서는 선형검색의 시간복잡도를 가진다.

```python
from collections import deque
def solution(n, edge):
    
    adj = [[] for _ in range(n+1)]
    for n1, n2 in edge:
        adj[n1].append(n2)
        adj[n2].append(n1)
    
    v = [0]*(n+1)
    v[1] = -1
    
    q = deque()
    q.append((1, 0))

    while q:
        node, ecnt = q.popleft()
            
        for nxt in adj[node]:
            if not v[nxt]:
                v[nxt] = ecnt + 1
                q.append((nxt, ecnt+1))
                
    return v[2:].count(max(v[2:]))         

```


---
---

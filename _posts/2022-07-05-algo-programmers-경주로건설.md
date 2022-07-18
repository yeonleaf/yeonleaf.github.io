---
title: "경주로건설"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, practice finished]

toc: true

date: 2022-07-05
last_modified_at: 2022-07-08
---

## **문제 링크**
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/67259)

<br>

---
---
 
## **CODE 1**: 테케 통과 못함
### <u>날짜</u> 2022-07-05
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
좌표, 진행 방향, 현재까지의 cost 저장

(i, j, d, cost)
bfs로 진행하고 n-1 n-1칸에 도착하면 res와 비교
위 왼 아래 오
0 1 2 3
진행방향이 없는 경우 ( (0,0)에서 진행방향이 -1 ) nd를 진행 방향으로 정하고 cost는 cost를 계승
(not d%2 and nd%2) or (d%2 and not nd%2) 인 경우 코너 -> cost + 500
아닌 경우 직선 -> cost + 100
방문했던 구역을 다시 방문할 수 없음

벽이 있는 경우 갈 수 없음
'''
'''
greedy하게 푸는 건가..? 코너를 최소한으로 만들어야 하니까...
현재 위치에서 직선 도로를 만들 수 있으면 무조건 직선 도로를 만들기
'''
```

<br>

#### <u>코드</u>
```python

from collections import deque
def solution(board):
    res = int(1e9)
    
    n = len(board)
    v = [[0]*n for _ in range(n)]
    v[0][0] = 1
    
    q = deque()
    q.append((0, 0, -1, 0, v))
    
    di = [(-1, 0), (0, -1), (1, 0), (0, 1)]
    
    while q:
        ci, cj, cd, ccost, cv = q.popleft()

        if ci == n-1 and cj == n-1:
            res = min(res, ccost)
        
        for nd in range(4):
            ni, nj = ci+di[nd][0], cj+di[nd][1]
            nv = [row[:] for row in cv]

            # 격자를 벗어날 경우
            if 0 > ni or 0 > nj or n <= ni or n <= nj:
                continue
            # 진행 방향에 벽이 있는 경우
            if board[ni][nj] == 1:
                continue
            # 이미 방문한 점인 경우
            if cv[ni][nj]:
                continue
            # 진행방향이 아직 없는 경우
            if cd == -1:
                nv[ni][nj] = 1
                q.append((ni, nj, nd, ccost+100, nv))
                continue
            # 코너를 형성하는 경우
            if (not cd%2 and nd%2) or (cd%2 and not nd%2):
                nv[ni][nj] = 1
                q.append((ni, nj, nd, ccost+600, nv))
                continue
            # 단순 직선 도로 만들기
            nv[ni][nj] = 1
            q.append((ni, nj, nd, ccost+100, nv))
            
    return res
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://school.programmers.co.kr/questions/30355)

DP로 풀어야 하고 3차원 배열을 사용해서 풀어야 한다고 한다.

---
---

<br>

---
---
 
## **CODE 2**: 실패!
### <u>날짜</u> 2022-07-05
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>

BFS + DP

<br>

#### <u>코드</u>
```python
from collections import deque
def solution(board):
    res = int(1e9)
    
    n = len(board)
    v = [[[int(1e9)]*4 for _ in range(n)] for _ in range(n)]
    v[0][0] = [0, 0, 0, 0]

    rec = [[0]*n for _ in range(n)]
    rec[0][0] = 1
    q = deque()
    q.append((0, 0, -1, rec))
    
    di = [(-1, 0), (0, -1), (1, 0), (0, 1)]
    
    while q:
        ci, cj, cd, crec = q.popleft()
        
        for nd in range(4):
            ni, nj = ci+di[nd][0], cj+di[nd][1]

            # 격자를 벗어날 경우
            if 0 > ni or 0 > nj or n <= ni or n <= nj:
                continue
            # 진행 방향에 벽이 있는 경우
            if board[ni][nj] == 1:
                continue
            if crec[ni][nj]:
                continue
            nrec = [row[:] for row in crec]
            # 코너를 형성하는 경우
            if cd != -1 and ((not cd%2 and nd%2) or (cd%2 and not nd%2)):
                if v[ci][cj][cd]+600 <= v[ni][nj][nd]:
                    nrec[ni][nj] = 1
                    v[ni][nj][nd] = v[ci][cj][cd]+600
                    q.append((ni, nj, nd, nrec))
                    continue
            # 단순 직선 도로 만들기
            if v[ci][cj][cd]+100 <= v[ni][nj][nd]:
                nrec[ni][nj] = 1
                v[ni][nj][nd] = v[ci][cj][cd]+100
                q.append((ni, nj, nd, nrec))
    return min(v[-1][-1])
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://school.programmers.co.kr/questions/25392)
```python
from collections import deque

def solution(board):
    result = 10000
    N = len(board)
    direction = [[0, 1, 0], [1, 0, 1], [0, -1, 2], [-1, 0, 3]]
    dp = [[[10000] * N for i in range(N)] for j in range(4)]
    queue = deque()
    queue.append([0, 0, 0, 0])
    queue.append([0, 0, 0, 1])
    while queue:
        x, y, m, d = queue.popleft()
        for i in range(4):
            new_x = x + direction[i][0]
            new_y = y + direction[i][1]
            if -1 < new_x < N and -1 < new_y < N and board[new_x][new_y] == 0:
                new_m = m + 1
                if not d == direction[i][2]:
                    new_m += 5
                if new_m < dp[direction[i][2]][new_x][new_y]:
                    dp[direction[i][2]][new_x][new_y] = new_m
                    if new_x == N-1 and new_y == N-1:
                        continue
                    queue.append([new_x, new_y, new_m, direction[i][2]])
    for i in range(4):
        result = min([result, dp[i][N-1][N-1]])
    return result * 100
```

---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-07-08
#### <u>총 소요시간</u> 30m

<br>

#### <u>설계</u>
```python
'''
bfs는 방문했던 곳을 다시 방문할 수 없음
dp[i][j][d] : 현재 i, j에 있고 방향은 d를 바라보고 있을 때 minimum cost (기본값은 int(1e9))

ci, cj, cd

cost = dp[ci][cj][cd]
for nd in 4방향
    ni nj가 격자를 벗어나거나 벽이 있으면 continue

    ncost = ccost + 1
    d != nd이면 ncost = ncost += 5
    
    ncost < ccost:
        dp[ni][nj][nd] = ncost
        q.append((ni, nj, nd))
'''
```

<br>

#### <u>코드</u>
```python
from collections import deque
def solution(board):
    
    dirs = [(0, 1), (1, 0), (0, -1), (-1, 0)]
    
    n = len(board)
    dp = [[[int(1e9)]*4 for _ in range(n)] for _ in range(n)]
    
    dp[0][0][0] = 0
    dp[0][0][1] = 0
    
    q = deque()
    q.append((0, 0, 0))
    q.append((0, 0, 1))
    
    while q:
        ci, cj, cd = q.popleft()
        for nd in range(4):
            ni, nj = ci + dirs[nd][0], cj + dirs[nd][1]
            if 0 <= ni < n and 0 <= nj < n and not board[ni][nj]:
                ncost = dp[ci][cj][cd] + 1
                if cd != nd:
                    ncost += 5
                if ncost < dp[ni][nj][nd]:
                    dp[ni][nj][nd] = ncost
                    if ni == n-1 and nj == n-1:
                        continue
                    q.append((ni, nj, nd))
                    
    return min(dp[-1][-1])*100
```

---
---


<br>

#### <b> ✅ 최종 comment </b>

bfs + dp 방법 잘 기억해 놓기 (최소값을 갱신할 수 있을 때만 한 번 방문한 곳에 다시 방문하도록)
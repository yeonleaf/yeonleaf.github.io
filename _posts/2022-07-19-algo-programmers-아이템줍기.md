---
title: "아이템 줍기"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, saw discussion]

toc: true

date: 2022-07-19
last_modified_at: 2022-07-19
---

## **문제 링크**
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/87694)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-07-19
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
rectangle, charx, chary, itemx, itemy에 각각 2를 곱하기
2*2 행렬 매트릭스에 rectangle의 합집합 구하기 (초기값 101*101)
dfs/bfs로 테두리 판별하면서 최소 거리 구하기
테두리란 무엇? 현재 점을 기준으로 사방의 점을 확인했을 때 빈칸이 하나 이상 있는 칸을 테두리라고 한다.
'''
```

<br>

#### <u>코드</u>
```python
from collections import deque
def solution(rectangles, chary, charx, itemy, itemx):
    
    rect = [[e*2 for e in box] for box in rectangles]
    
    chary, charx, itemy, itemx = chary*2, charx*2, itemy*2, itemx*2
    
    graph = [[0]*31 for _ in range(31)]
    
    for ly, lx, ry, rx in rect:
        for y in range(ly, ry+1):
            for x in range(lx, rx+1):
                graph[y][x] = 1
                
    visited = [row[:] for row in graph]

    q = deque()
    q.append((chary, charx, 0))
    
    res = int(1e9)
       
    def check(y, x):
        nonlocal graph
        res = 0
        for dy, dx in (-1, 0), (1, 0), (0, -1), (0, 1):
            ny, nx = y+dy, x+dx
            if ny < 0 or nx < 0 or ny >= 101 or nx >= 101:
                continue
            if not graph[ny][nx]:
                res += 1
        if not res:
            return False
        return True
    
    visited[chary][charx] = 0
    
    while q:
        # itemy, itemx에 도착하면 거리 비교
        cy, cx, count = q.popleft()
        if cy == itemy and cx == itemx:
            visited[itemy][itemx] = 1
            res = min(res, count)
        
        for dy, dx in (-1, 0), (1, 0), (0, -1), (0, 1):
            ny, nx = cy+dy, cx+dx
            if cy == 4 and cx == 8:
                print(ny, nx)
            if ny < 0 or nx < 0 or ny >= 101 or nx >= 101:
                continue
            # 방문했던 점 제외
            if not visited[ny][nx]:
                continue
            # 아예 범위가 아닌 경우 제외
            if not graph[ny][nx]:
                continue
            # 테두리인지 확인
            if not check(ny, nx):
                continue
            if cy == 13 and cx == 8:
                print(ny, nx)
                print("***" + str(graph[ny][nx]))
            visited[ny][nx] = 0
            q.append((ny, nx, count+1))

    return res // 2
```

중간에 점이 자꾸 유실된다... 어디서 유실되는지 모르겠다.
처음부터 다시 한 번 풀어보고 그래도 안 되면 해답 보기

---
---

<br>

#### <b> ✅ 최종 comment </b>
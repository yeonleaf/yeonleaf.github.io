---
title: "퍼즐 조각 채우기"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3]

toc: true

date: 2022-07-15
last_modified_at: 2022-07-15
---

## **문제 링크**
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/84021)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-07-15
#### <u>총 소요시간</u> 2시간

<br>

다음에 다시 한 번 시도해 볼 것

<br>

#### <u>설계</u>
```python
'''
table을 dfs탐색한다.
vt

game_board를 dfs탐색한다.

gt

special 탐색 함수

special = []
ㅗ나 ㅜ형태의 블록이 있는지 확인한다.
어떤 칸을 중심으로 세 방향 이상 연결된 칸이 있는 경우
    해당 칸을 중심으로 몇 번 이동하는지 각각 기록한다. ex) 111, 112, 1112
    visited에 블록이 있는 자리를 방문 처리한다.


normal
table을 dfs탐색한다.

(i, j, rec)
ㅗ나 ㅜ가 아니면 이동 방향을 기록한다.
같은 방향이면 1, 다른 방향이면 0
예시의 2번 블록의 경우 1010 
visited에 방문을 기록하면서 탐색 진행
더 이상 방문할 칸이 없으면 rec을 저장하고 리턴

table 탐색 결과와 game_board 탐색 결과를 대조한다.
1. table_special와 game_special 탐색 결과를 대조한다.

2. table_normal과 game_normal 탐색 결과를 대조한다.
'''
```

<br>

#### <u>코드</u>
```python


def solution(game_board, table):
    n = len(table)
    dirs = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    
    # ㅗ, ㅜ같은 특수한 경우
    def isSpecial(i, j, test):
        nonlocal dirs, n
        path = []
        for di, dj in dirs:
            cnt = 0
            for k in range(1, 3):
                ni, nj = i+di*k, j+dj*k
                if ni < 0 or nj < 0 or ni >= n or nj >= n or test[ni][nj]:
                    break
                cnt += 1
            if cnt: path.append(cnt)
        return path if len(path) >= 3 else []
    
    # 일반적인 경우
    def nor(i, j, pd, board, path, results, v):
        
        cnt = 0
        
        for nd in range(4):
            ni, nj = i + dirs[nd][0], j + dirs[nd][1]
            if ni < 0 or nj < 0 or ni >= n or nj >= n or not board[ni][nj] or v[ni][nj]:
                cnt += 1
                continue
            v[ni][nj] = 1
            if pd == -1 or pd == nd:
                nor(ni, nj, nd, board, path+[1], results, v)
                v[ni][nj] = 0
            else:
                nor(ni, nj, nd, board, path+[0], results, v)
                v[ni][nj] = 0
        
        # 이동할 수 있는 장소가 없는 경우
        if cnt == 4:
            print(i, j)
            results.append(path)
            return
    
    
    table_spe = []
    table_nor = []
    
    for i in range(n):
        for j in range(n):
            if table[i][j]:
                v = [[0]*n for _ in range(n)]
                stest = isSpecial(i, j, table)
                if stest: table_spe.append(stest)
                nor(i, j, -1, table, [], table_nor, v)
    print(table_spe)
    print(table_nor)

```
---
---

<br>

#### <b> ✅ 최종 comment </b>
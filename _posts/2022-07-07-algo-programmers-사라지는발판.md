---
title: "사라지는 발판"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, saw discussion]

toc: true

date: 2022-07-07
last_modified_at: 2022-07-08
---

## **문제 링크**
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/92345)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-07-07
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
승리를 보장할 수 없다..?
A는 이번 턴에 B플레이어가 올 가능성이 있는 좌표로 이동한다.

B는 다음 턴에 A플레이어가 올 가능성이 있는 좌표를 피한다.

캐릭터의 이동 횟수의 합을 구하시오

완탐..

a, b
next_a = 현재 턴에서 a의 예상 이동 좌표 (발판이 없거나 보드 밖인 경우를 제외)
next_b = 현재 턴에서 b의 예상 이동 좌표 (발판이 없거나 보드 밖인 경우를 제외)

# 어떤 캐릭터가 더 이상 이동할 곳이 없는 경우
not next_a or not next_b:
    return a + b

# 두 캐릭터가 같은 발판 위에 있는 경우
a의 좌표 == b의 좌표
    return a + b
    
# 다음 턴의 경우의 수를 만들어줌
for na in next_b:
    for nb in next_a:
        a의 현재 위치, b의 현재 위치에 있는 발판을 지우고 해당 위치로 이동
        보드판을 복구해주기
        
다음 턴으로 넘어가기
'''
```

<br>

#### <u>코드</u>
```python
def solution(board, aloc, bloc):

    n = len(board)
    
    res = 0
    
    def game(a, b):
        nonlocal n, res, aloc, bloc, board
        
        print(aloc, a, bloc, b)
        for row in board:
            print(*row)
        
        if aloc == bloc:
            res = max(res, a+b)
            return 
        
        next_a, next_b = [], []
        cai, caj = aloc
        cbi, cbj = bloc
        for di, dj in (1, 0), (0, 1), (-1, 0), (0, -1):
            nai, naj = cai + di, caj + dj
            nbi, nbj = cbi + di, cbj + dj
            if 0 <= nai < n and 0 <= naj < n and board[nai][naj]:
                next_a.append((nai, naj))
            if 0 <= nbi < n and 0 <= nbj < n and board[nbi][nbj]:
                next_b.append((nbi, nbj))
        
        print(next_a)
        print(next_b)
        
        if not next_a or not next_b:
            res = max(res, a+b)
            return
        
        old = [row[:] for row in board]
        # b는 next_b에 있는 좌표 중 next_a에 없는 좌표로 이동해야 하고
        # a는 next_b에 있는 좌표 중 next_a에 있는 좌표로 이동해야 함
        # 단 b에게 선택지가 딱 하나 있다면 해당 좌표로 이동
        # next_b에 있는 좌표 중 next_a에 있는 좌표가 없다면 next_a에 있는 좌표로 이동
        for nai, naj in next_b:
            for nbi, nbj in next_b:
                # nai, naj가 next_a에 있는지 확인 & nbi, nbj가 next_a에 없는지 확인
                if (nai, naj) in next_a:
                    if len(next_b) == 1 or (nbi, nbj) not in next_a:
                        board[cai][caj] = 0
                        aloc = [nai, naj]

                        board[cbi][cbj] = 0
                        bloc = [nbi, nbj]
                        game(a+1, b+1)
                        board = [row[:] for row in old]
    game(0, 0)
    return res
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://school.programmers.co.kr/questions/32399)
```python
A와 B를 번갈아가면서 DFS
한 번에 두 명을 처리하려고 해서 경우의 수가 복잡해진 듯

현재의 기준으로 다음 차례에 다음 플레이어가 이겼다면 현재 플레이어는 패배

현재 사용자가 패배할 경우 이동 거리가 최대가 되는 값을 고름
현재 사용자가 승리할 경우 이동 거리가 최소가 되는 값을 고름
```

---
---

<br>

---
---
 
## **CODE 2**: 
### <u>날짜</u> 2022-07-08
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
move = [0, 0]
loc = [aloc, bloc]
차례 
(차례+1)%2

unable = 0
상하좌우 칸 확인
    이동하려고 하는 칸에 다른 플레이어가 있는 경우 현재 플레이어가 패배 return sum(move)
    이동하려고 하는 칸이 보드 밖이거나 발판이 없는 경우 unable += 1 continue
    해당 칸으로 이동 loc[차례] = [ni, nj] move[차례] += 1
상하좌우 모두 발판이 없거나 보드 밖이라서 이동할 수 없는 경우 (unable == 4) return sum(move)
'''
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://tech.kakao.com/2022/01/14/2022-kakao-recruitment-round-1/)
[Discussion Link](https://school.programmers.co.kr/questions/25678)
```python
미니맥스 알고리즘을 공부하고 위의 글들을 다시 읽어보자.
```

---
---


<br>

#### <b> ✅ 최종 comment </b>
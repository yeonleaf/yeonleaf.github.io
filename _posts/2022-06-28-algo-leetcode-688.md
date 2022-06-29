---
title: "(688) Knight Probability in Chessboard"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, practice finished]

toc: true

date: 2022-06-28
last_modified_at: 2022-06-29
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/knight-probability-in-chessboard/)

<br>

---
---
 
## **CODE 1**: 실패
### <u>날짜</u> 2022-06-28
#### <u>총 소요시간</u> 50m

<br>

#### <u>설계</u>
```python
'''
ij가 칸을 벗어나는 경우 return 0 칸에 있는 경우 return 1
res
di, dj in eight
    res += 1/8*rec(ni nj)
return res
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        
        eight = [(-2, -1), (-1, -2), (1, -2), (2, -1), (2, 1), (2, 2), (-1, 2), (-2, 1)]
        
        def rec(i, j, k):
            if i < 0 or j < 0 or i >= n or j >= n:
                return 0
            if not k:
                return 1
            res = 0
            for di, dj in eight:
                ni, nj = i+di, j+dj
                res += (1/8 * rec(ni, nj, k-1))
            
            return res
        
        return rec(row, column, k)
            
```
```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        self.memo = dict()
        eight = [(-2, -1), (-1, -2), (1, -2), (2, -2), (2, 1), (1, 2), (-2, 1), (-1, 2)]
        
        def knight(i, j, move):
            nonlocal k, eight

            if move == k+1:
                return 1
            if i < 0 or j < 0 or i >= n or j >= n:
                return 0
            if (i, j, move) in self.memo:
                return self.memo[(i, j, move)]
            
            cur = 0
            for di, dj in eight:
                cur += (0.125 * knight(i+di, j+dj, move+1))

            self.memo[(i, j, move)] = cur
            return cur
            
        return knight(row, column, 0)
```
<br>

#### <u>디버깅</u>
```python
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/knight-probability-in-chessboard/discuss/113954/Evolve-from-recursive-to-dpbeats-94)
왜 안 되는지 이해가 안 되는데...? 다시 처음부터 풀어 볼 것

---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-29
#### <u>총 소요시간</u> 30m

<br>

#### <u>설계</u>
```python
'''
k move를 하거나 chessboard 밖으로 벗어날 때까지 움직인다.
knight가 체스판에 남아 있을 확률

체스판 밖으로 넘어갔다면 return 0
k번 다 움직였다면 return 1

체스판 안에 있고 k번 다 움직이지 않았다면 다음 이동
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        # eight에 문제가 있었음
        eight = [(-2,-1),(-1,-2),(1,-2),(2,-1),(2,1),(1,2),(-1,2),(-2,1)]
        
        self.dp = {}
        
        def move(i, j, cnt):
            
            if (i, j, cnt) in self.dp:
                return self.dp[(i, j, cnt)]
            
            if i < 0 or j < 0 or i >= n or j >= n:
                return 0
            
            if cnt == 0:
                return 1
            
            poss = 0
            for di, dj in eight:
                ni, nj = i+di, j+dj

                poss += (0.125 * move(ni, nj, cnt-1))
            self.dp[(i, j, cnt)] = poss
            return self.dp[(i, j, cnt)]
        
        return move(row, column, k)
```
<br>

#### <u>디버깅</u>
```python
3
10
0
0
expected == result

5
10
0
0
expected == result
```
---
---

---
title: "(174) Dungeon Game"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, hard, DP, saw discussion]

toc: true

date: 2022-06-09
last_modified_at: 2022-06-11
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/dungeon-game/)

<br>

---
---
 
## **CODE 1**:
### <u>날짜</u> 2022-06-09
#### <u>총 소요시간</u> 50m + alpha (디버깅중) => 시간 초과!

<br>

#### <u>설계</u>
```python
'''
room의 종류 마이너스 / 0 / 플러스
마이너스와 플러스는 기사의 체력을 깎는다.
오른쪽, 아래쪽으로만 이동

princess를 구출할 수 있는 minimum initial health 구하기

DP인듯?

ci, cj, cp, cm

dungeon[ci][cj]가 마이너스이면
res 갱신 max(res, abs(cp + cm) + 1)

오른쪽, 아래쪽 이동
    ni, nj가 플러스인 경우 / 마이너스인 경우
    큐에 집어넣기

return res
'''
```

<br>

#### <u>코드</u>
```python
from collections import deque

class Solution:
    def calculateMinimumHP(self, dungeon: List[List[int]]) -> int:
        
        m, n = len(dungeon), len(dungeon[0])
        if m == 1 and n == 1:
            return dungeon[m-1][n-1] + 1
        
        q = deque()
        # i, j, p(plus), m(minus)
        q.append((0, 0, dungeon[0][0] if dungeon[0][0] > 0 else 0, dungeon[0][0] if dungeon[0][0] < 0 else 0, dungeon[0][0] + 1))
                
        res = int(1e9)    
        
        while q:
            ci, cj, cp, cm, cr = q.popleft()
            if ci == m-1 and cj == n-1:
                res = min(res, cr)
            
            for di, dj in (0, 1), (1, 0):
                ni, nj = ci + di, cj + dj
                if 0 > ni or 0 > nj or m <= ni or n <= nj:
                    continue
                if dungeon[ni][nj] > 0:
                    q.append((ni, nj, cp+dungeon[ni][nj], cm, cr))
                else:
                    nm = cm + dungeon[ni][nj]
                    q.append((ni, nj, cp, nm, abs(cp + nm) + 1))
        return res
```
<br>

#### <u>디버깅</u>
```python
[[3]]
expected 1 != result 4 -> fix

[[3, 1], [3, 4]]
expected == result

[[-3, -1], [-3, -4]]
expected == result

[[-200]]
expected(201) != result(-199) -> fix

[[2, 1], [3, -4]]
expected(1) != result(2)

```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/dungeon-game/discuss/745340/post-Dedicated-to-beginners-of-DP-or-have-no-clue-how-to-start)

DP 문제였다..ㅎ

TOP-DOWN DP로 다시 풀어보기

---
---

<br>

---
---
 
## **CODE 2**: 시간 초과
### <u>날짜</u> 2022-06-10
#### <u>총 소요시간</u> 25 + 14m

<br>

#### <u>설계</u>
```python
'''
ij가 0이나 양수인 경우 필요한 체력 : 1
ij가 음수인 경우 필요한 체력 : -(ij) + 1

dp[i][j] = 00에서 ij까지 가기 위해 필요한 minimum 체력
dp[0][0]은 초기화 필요 (0이나 양수이면 1, 음수이면 -(ij)+1)

rec(i, j)

base case
i, j가 m-1, n-1인 경우
    return 0

dp[i][j]가 있으면 return

dp[i][j] = int(1e9)
오른쪽, 아래로 이동
    ni, nj가 0이나 양수인 경우
        dp[i][j] = min(dp[i][j], rec(ni, nj))
    ni, nj가 음수인 경우
        dp[i][j] = min(dp[i][j], -dungeon[ni][nj] + 1 + rec(ni, nj))
        
return dp[i][j]

'''
```

---
---


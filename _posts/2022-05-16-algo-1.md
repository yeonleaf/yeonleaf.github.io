---
title: "(688) Knight Probability in Chessboard"
excerpt: "Multi-Dimensions DP"
categories:
    - algorithm
tags:
    - [leetcode, DP, Multi Dimensions DP, complete success]

toc: true

date: 2022-05-16
last_modified_at: 2022-05-16
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/knight-probability-in-chessboard/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u>  2022-05-16
#### <u>총 소요시간</u>  40m

<br>

#### <u>설계</u>
```python
'''
case 1 : 1/8*2*1/8*2

i, j, move

move가 0이면 더 이상 움직일 수 없음 -> return 1

poss 0
8방향 di, dj -> ni, nj
poss += (1/8) * ni, nj가 보드를 벗어나지 않는 경우에만 재귀 호출

return poss

(0, 0)
1/8 * 2

(1, 2)
1/8 * 2
1/4
(2, 1)
1/8 * 2
1/4

1/8 * 1/8 * 2
+ 1/8 * 1/8 * 2
'''
```

#### <u>코드</u>
```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        
        self.dp = {}
        eight = [(-2, -1), (-1, -2), (1, -2), (2, -1), (2, 1), (1, 2), (-1, 2), (-2, 1)]
        
        def makePoss(i, j, move):
            if move == 0:
                return 1
            if (i, j, move) in self.dp:
                return self.dp[(i, j, move)]
            poss = 0
            for di, dj in eight:
                ni, nj = i+di, j+dj
                if ni < 0 or nj < 0 or ni >= n or nj >= n:
                    continue
                poss += ((1/8)*makePoss(ni, nj, move-1))
            self.dp[(i, j, move)] = poss
            return poss
        
        return makePoss(row, column, k)
```

#### <u>디버깅</u>
```python
## n & k maximum case
25
100
0
0
# expected == result

25
100
24
24
# expected == result

## random case
18
54
5
5
# expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/knight-probability-in-chessboard/discuss/115213/C%2B%2B-memoization-easy-to-understand)
```cpp
class Solution {
private:
    unordered_map<int, unordered_map<int, unordered_map<int, double>>>dp;
public:
    double knightProbability(int N, int K, int r, int c) {
        if(dp.count(r) && dp[r].count(c) && dp[r][c].count(K)) return dp[r][c][K];
        if(r < 0 || r >= N || c < 0 || c >= N) return 0;
        if(K == 0) return 1;
        double total = knightProbability(N, K - 1, r - 1, c - 2) + knightProbability(N, K - 1, r - 2, c - 1) 
                     + knightProbability(N, K - 1, r - 1, c + 2) + knightProbability(N, K - 1, r - 2, c + 1) 
                     + knightProbability(N, K - 1, r + 1, c + 2) + knightProbability(N, K - 1, r + 2, c + 1) 
                     + knightProbability(N, K - 1, r + 1, c - 2) + knightProbability(N, K - 1, r + 2, c - 1);
        double res = total / 8;
        dp[r][c][K] = res;
        return res;
    }
};
```
---
---


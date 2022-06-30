---
title: "(799) Champagne Tower"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, saw discussion]

toc: true

date: 2022-06-30
last_modified_at: 2022-06-30
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/champagne-tower/)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-06-30
#### <u>총 소요시간</u> 45m + alpha 

<br>

#### <u>설계</u>
```python
'''
ij
101 * 101

dp[0][0] = poured-1


i 1 ~ 101
j = 1 ~ i+1

j가 0 -> dp[i][j] += dp[i-1][j] // 2
j가 i -> dp[i][j] += dp[i-1][j-1] // 2
이외 -> dp[i][j] = (dp[i-1][j] // 2) + (dp[i-1][j-1] // 2)

'''
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/champagne-tower/discuss/118711/JavaC%2B%2BPython-1D-DP-O(R)-space)

방향 자체는 맞다. 다시 한 번 풀어볼 것

```python
def champagneTower(self, poured, query_row, query_glass):
    res = [poured] + [0] * query_row
    for row in range(1, query_row + 1):
        for i in range(row, -1, -1):
            res[i] = max(res[i] - 1, 0) / 2.0 + max(res[i - 1] - 1, 0) / 2.0
    return min(res[query_glass], 1)
```

---
---

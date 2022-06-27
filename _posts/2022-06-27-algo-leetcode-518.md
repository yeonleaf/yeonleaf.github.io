---
title: "(518) Coin Change 2"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, saw discussion, ⭐]

toc: true

date: 2022-06-27
last_modified_at: 2022-06-27
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/coin-change-2/description/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-27
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
dp = 1 ~ amount
c in coins
    for i in range(n+1):
        i-c >= 0? 
            dp[i] += dp[i-c]

1 1 1 1
2 2

1 2 5
    1 2 3 4 5
    1 1 1 1 1 1
    1 1 2 2 2 1
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:

        dp = [0]*(amount+1)
        dp[0] = 1
        
        for c in coins:
            for i in range(1, amount+1):
                if i-c >= 0:
                    dp[i] += dp[i-c]
        
        return dp[-1]
```

---
---

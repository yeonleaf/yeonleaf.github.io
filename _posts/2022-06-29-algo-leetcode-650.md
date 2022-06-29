---
title: "(650) 2 Keys Keyboard"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need optimization]

toc: true

date: 2022-06-29
last_modified_at: 2022-06-29
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/2-keys-keyboard/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-29
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
A
1 2 3 4 5 6 7
0 2 3 4 5 5 7
i vs (not i%2인 경우) dp[i//2]+2
paste           copy + paste
5 vs
'''
'''
dp[i]
j 1부터 i-1까지 i의 약수를 찾기
dp[i] = min(dp[i], dp[j] + (i // j))
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def minSteps(self, n: int) -> int:
        
        dp = [int(1e9)]*(n+1)
        dp[0] = 0
        dp[1] = 0
        dp[2] = 2
        
        if n <= 2:
            return dp[n]
        
        for i in range(3, n+1):
            for j in range(1, i-1):
                if not i % j:
                    dp[i] = min(dp[i], dp[j] + (i // j))
        
        return dp[-1]
            
```
<br>

#### <u>디버깅</u>
```python
1000
expected == result

25
expected == result

17
expected == result

516
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/2-keys-keyboard/discuss/360551/C%2B%2B-(-Recursion-%2B-Memoization-)-(-Different-approach-(-without-prime-factorization-)-))

recursive하게 풀어보기

---
---

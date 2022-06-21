---
title: "(5) Longest Palindromic Substring"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, dp, practice finished]

toc: true

date: 2022-06-20
last_modified_at: 2022-06-20
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/longest-palindromic-substring/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-20
#### <u>총 소요시간</u> 25m

<br>

#### <u>설계</u>
```python
'''
dp ij : i부터 j까지가 palindromic한지?
i == j인 칸은 모두 True (longest = ij)

for i in range(n)
    for j in range(i+1, n)
        s[i]==s[j]인 경우
            j-i+1 == 2거나 dp[i+1][j-1]이 true인 경우 (palindromic word 연장 가능)
                res를 갱신한다.
return res
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        
        if n == 1:
            return s[0]
        
        dp = [[False]*n for _ in range(n)]
        
        res = ""
        
        for i in range(n):
            dp[i][i] = True
            res = s[i]
        
        for i in range(n-1, -1, -1):
            for j in range(i+1, n):
                if s[i] == s[j]:
                    if j-i+1 == 2 or dp[i+1][j-1]:
                        dp[i][j] = True # 이 부분 빼먹지 않게 주의!
                        if len(res) < len(s[i:j+1]):
                            res = s[i:j+1]
        
        return res
```
<br>

#### <u>디버깅</u>
```python
"abccba"
expected != result
```

---
---

---
title: "(516) Longest Palindromic Subsequence"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need practice]

toc: true

date: 2022-06-28
last_modified_at: 2022-06-29
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/longest-palindromic-subsequence/)

<br>

---
---
 
## **CODE 1**: 실패!
### <u>날짜</u> 2022-06-28
#### <u>총 소요시간</u> 50m

<br>

#### <u>설계</u>
```python
'''
dp문제

ijk i부터 j까지 k개 지운 상태에서 longest palindromic subsequence

ijk = max([i][j][k-1], [i][j-1][k], [i-1][j][k])

ij가 palindromic word이면 ijk와 ij의 길이를 비교해서 더 큰 쪽을 저장
'''
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/longest-palindromic-subsequence/discuss/99101/Straight-forward-Java-DP-solution)

k까지 필요 없는데 너무 생각을 많이 한 것 같다.

dp[i][j]: the longest palindromic subsequence's length of substring(i, j), here i, j represent left, right indexes in the string

State transition:

dp[i][j] = dp[i+1][j-1] + 2 if s.charAt(i) == s.charAt(j)

otherwise, dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1])

Initialization: dp[i][i] = 1


---
---


<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-29
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
i == j이면 dp[i][j] = 1
ij = i부터 j까지의 longest palindromic subsequence의 길이
s[i] == s[j]이면
j-i+1 == 2인 경우 dp[i][j] = 2
else dp[i][j] = dp[i+1][j-1] + 2

'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:

        n = len(s)
        dp = [[0]*n for _ in range(n)]
        
        for i in range(n):
            dp[i][i] = 1
            
        for i in range(n-1, -1, -1):
            for j in range(i+1, n):
                if s[i] == s[j]:
                    if j-i+1 == 2:
                        dp[i][j] = 2
                    else:
                        dp[i][j] = dp[i+1][j-1] + 2
                else:
                    dp[i][j] = max(dp[i+1][j], dp[i][j-1])
            
        return dp[0][-1]
```
<br>

#### <u>디버깅</u>
```python
"abccba"
expected == result

"a"
expected == result

"aaaa"
expected == result

"abcabc"
expected == result

"xyzabc"
expected == result

"aabdefaa"
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link]()
```python
```

---
---

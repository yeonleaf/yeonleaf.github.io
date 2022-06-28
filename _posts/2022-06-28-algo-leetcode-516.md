---
title: "(516) Longest Palindromic Subsequence"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, saw discussion]

toc: true

date: 2022-06-28
last_modified_at: 2022-06-28
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

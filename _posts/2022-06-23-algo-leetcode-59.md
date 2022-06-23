---
title: "(59) Spiral Matrix II"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, practice finished]

toc: true

date: 2022-06-23
last_modified_at: 2022-06-23
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/spiral-matrix-ii/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-23
#### <u>총 소요시간</u> 20m

<br>

#### <u>설계</u>
```python
'''
i, j = 0, 0
di, dj = 0, 1

for num in range(1, n*n+1):
    ij에 num을 넣는다.
        ij + didj가 격자를 넘어가면 di, dj를 갱신한다.
        ij를 갱신한다. (ij -> ji -> j에 *-1)
    0 1 -> 1 0 -> 0 -1 -> -1 0
    
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        
        matrix = [[0]*n for _ in range(n)]
        
        i, j, di, dj = 0, 0, 0, 1
        for num in range(1, n*n+1):
            matrix[i][j] = num
            
            if i+di < 0 or i+di >= n or j+dj < 0 or j+dj >= n or matrix[i+di][j+dj] != 0:
                di, dj = dj, -di
            
            i, j = i+di, j+dj
            
        return matrix
```
<br>

#### <u>디버깅</u>
```python
20
expected == result

5
expected == result
```
<br>

---
---

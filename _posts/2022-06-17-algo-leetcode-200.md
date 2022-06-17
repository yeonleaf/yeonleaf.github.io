---
title: "(200) Number of Islands"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, dfs, bfs, complete success]

toc: true

date: 2022-06-17
last_modified_at: 2022-06-17
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/number-of-islands/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-17
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
bfs
밖에서 섬 찾기 시작. 하나 찾을 때마다 count
visited배열은 공유

'''
```

<br>

#### <u>코드</u>
```python
from collections import deque
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        

        
        m, n = len(grid), len(grid[0])
        
        self.v = [[0]*n for _ in range(m)]
        
        def bfs(i, j):
            q = deque()
            self.v[i][j] = 1
            q.append((i, j))
            
            while q:
                ci, cj = q.popleft()
                for di, dj in (-1, 0), (1, 0), (0, 1), (0, -1):
                    ni, nj = ci+di, cj+dj
                    if ni < 0 or nj < 0 or ni >= m or nj >= n:
                        continue
                    if self.v[ni][nj]:
                        continue
                    if grid[ni][nj] == "0":
                        continue
                    self.v[ni][nj] = 1
                    q.append((ni, nj))
        
        res = 0
        
        for i in range(m):
            for j in range(n):
                if grid[i][j] == "1" and not self.v[i][j]:
                    res += 1
                    bfs(i, j)
        
        return res
```
<br>

#### <u>디버깅</u>
```python
[["0","0","0","0","0"],["0","0","0","0","0"],["0","0","0","0","0"],["0","0","0","0","0"]]
expected == result

[["0"]]
expected == result

[["1"]]
expected == result

[["1","1","1","1","1"],["1","1","1","1","1"],["1","1","1","1","1"],["1","1","1","1","1"]]
expected == result
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/number-of-islands/discuss/56359/Very-concise-Java-AC-solution)

DFS로 위, 아래, 옆, 왼 원소를 지워버리는 방식의 풀이
(이런 방식이 있구만 하고 기억해 두기)

```JAVA
public class Solution {

private int n;
private int m;

public int numIslands(char[][] grid) {
    int count = 0;
    n = grid.length;
    if (n == 0) return 0;
    m = grid[0].length;
    for (int i = 0; i < n; i++){
        for (int j = 0; j < m; j++)
            if (grid[i][j] == '1') {
                DFSMarking(grid, i, j);
                ++count;
            }
    }    
    return count;
}

private void DFSMarking(char[][] grid, int i, int j) {
    if (i < 0 || j < 0 || i >= n || j >= m || grid[i][j] != '1') return;
    grid[i][j] = '0';
    DFSMarking(grid, i + 1, j);
    DFSMarking(grid, i - 1, j);
    DFSMarking(grid, i, j + 1);
    DFSMarking(grid, i, j - 1);
}
```

---
---

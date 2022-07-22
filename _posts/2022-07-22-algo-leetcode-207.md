---
title: "(207) Course Schedule"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need practice]

toc: true

date: 2022-07-22
last_modified_at: 2022-07-22
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/course-schedule/)

<br>

---
---
 
## **CODE 1**: 시간 초과!
### <u>날짜</u> 2022-07-22
#### <u>총 소요시간</u> 

<br>

union find로 해 보려고 했는데 잘 되지 않았다.
union find는 어떤 원소가 어떤 그룹에 속하는지 알고 싶을 때 사용한다.
a노드와 b노드가 같은 부모를 가지고 있다면 두 노드를 연결했을 때 cycle이 발생하기 때문에 연결할 수 없다는 원리를 이용한다.

#### <u>설계</u>
```python
'''
0부터 n-1까지 확인
중간에 cycle이 하나라도 생기면 false
cycle이 없는 것을 확인했으면 true
union find?

dat []

union(a, b)
    b의 부모를 찾는다. par = find(b) # 최상위 부모를 찾기
    par가 0이면 (부모의 부모가 없음) dat[a] = b & return True
    
    par가 0이 아니면 (부모의 부모가 이미 있음) return False
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def canFinish(self, n: int, prerequisites: List[List[int]]) -> bool:
        
        prerequisites.sort()
        
        dat = [-1]*n
        
        def union(a, b):
            if dat[b] == -1:
                dat[a] = b
                return True
            return False
        
        for a, b in prerequisites:
            if not union(a, b):
                return False
                
        return True
```
<br>

#### <u>디버깅</u>
```python
3
[[0, 1], [1, 2], [2, 1]]
expected == result

4
[[0, 3], [1, 3], [2, 3]]
expected == result

4
[[0, 1], [2, 3], [1, 2]]
expected != result

# 순서를 바꾸면 문제가 생긴다.

5
[[1,0], [2, 0], [3, 1], [4, 1], [4, 0]]
expected != result
```
<br>

#### <u>다른 방식</u>

Topological sorting

[Discusstion Link](https://leetcode.com/problems/course-schedule/discuss/58586/Python-20-lines-DFS-solution-sharing-with-explanation)
```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        graph = [[] for _ in range(numCourses)]
        visited = [0 for _ in range(numCourses)]
        # create graph
        for pair in prerequisites:
            x, y = pair
            graph[x].append(y)
        # visit each node
        for i in range(numCourses):
            if not self.dfs(graph, visited, i):
                return False
        return True
    
    def dfs(self, graph, visited, i):
        # if ith node is marked as being visited, then a cycle is found
        if visited[i] == -1:
            return False
        # if it is done visted, then do not visit again
        if visited[i] == 1:
            return True
        # mark as being visited
        visited[i] = -1
        # visit all the neighbours
        for j in graph[i]:
            if not self.dfs(graph, visited, j):
                return False
        # after visit all the neighbours, mark it as done visited
        visited[i] = 1
        return True

```

---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-07-22
#### <u>총 소요시간</u> 

<br>

### **위상 정렬**
1. 각 노드의 진입계수와 진출계수를 저장한다. 
2. 진입계수가 0인 노드를 큐에 넣는다.
3. 큐에서 노드를 빼고 해당 노드에 연결되어 있는 간선을 삭제한다.
4. 새로 진입계수가 0이 된 노드를 큐에 넣는다.
5. 만약 노드를 모두 탐색하지 못했는데 넣을 노드가 없다면 cycle이 발생한 것이다. 정상적으로 위상 정렬을 마치기 위해서는 사이클이 없는 그래프(DAG)여야 한다.
6. 시간 복잡도는 간선과 노드를 모두 탐색해야 하기 때문에 O(V+E)


#### <u>코드</u>
```python
from collections import deque
class Solution:
    def canFinish(self, n: int, prerequisites: List[List[int]]) -> bool:
        
        inarr = [0]*n
        outarr = [0]*n
        
        adj = [[] for _ in range(n)]
        
        for a, b in prerequisites:
            adj[a].append(b)
            inarr[b] += 1
            outarr[a] += 1
        
        q = deque()
        
        # 진입계수가 0인 인덱스를 큐에 집어넣는다.
        for i in range(n):
            if not inarr[i]:
                q.append(i)
        
        while q:
            n1 = q.popleft()
            # 노드와 연결된 간선을 제거한다.
            for n2 in adj[n1]:
                outarr[n1] -= 1
                inarr[n2] -= 1
                if not inarr[n2]:
                    q.append(n2)
        print(inarr)
        print(outarr)
        # 아직 간선이 남아 있는데 while문이 종료된 경우 return False
        if sum(inarr) != 0 or sum(outarr) != 0:
            return False
        return True
```
<br>

#### <u>디버깅</u>
```python
4
[[0, 1], [1, 2], [2, 3], [3, 2]]
expected == result

4
[[0, 1], [1, 2], [3, 2], [2, 3]]
expected == result #위의 케이스에서 순서만 바꿈

4
[[0, 1], [1, 2], [2, 1], [2, 3]]
expected == result

4
[[0, 1], [2, 3], [1, 2]]
expected == result

4
[[0, 3], [2, 1], [3, 2]]
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link]()
```python
```

---
---


#### <b> ✅ 최종 comment </b>
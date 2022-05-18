---
title: "(638) Shopping Offers
"
excerpt: "DFS, BT"

categories:
    - algorithm
tags:
    - [leetcode, BT, DFS/BFS, complete success]

toc: true

date: 2022-05-17
last_modified_at: 2022-05-17
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/shopping-offers/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-05-17
#### <u>총 소요시간</u> 45m(설계~1차디버깅) + 5m (2차 디버깅)

<br>

#### <u>설계</u>

```python
'''
dfs with memoization
needs, lowest

for case in special:
    able = True
    for i in range(len(needs)):
        needs[i] < case[i]:
            able = False
            break
    if not able:
        break
    
    재귀호출 : needs에서 case를 빼고 lowest에 case[-1]을 더함

어떤 special case도 가질 수 없는 경우
needs * price를 lowest에 더함
self.res와 lowest를 비교해서 더 작은 값을 가져가기

'''
```

#### <u>코드</u>
```python
from functools import reduce

class Solution:
    def shoppingOffers(self, price: List[int], special: List[List[int]], needs: List[int]) -> int:
        
        n = len(needs)
        
        self.res = int(1e9)
        
        def dfs(needs, lowest):
            
            for case in special:
                able = True
                for i in range(n):
                    if needs[i] < case[i]:
                        able = False
                        break
                if not able:
                    continue # ★
                
                old = needs[::]
                new = [needs[i] - case[i] for i in range(n)]
                dfs(new, lowest + case[-1])
                needs = old[::]
                
            lowest += reduce(lambda acc, i : acc + (needs[i]*price[i]), range(n), 0)
            self.res = min(self.res, lowest)
            return 
        
        dfs(needs, 0)
        return self.res
```

#### <u>디버깅</u>
```python
## all needs are zero
[2,3,4]
[[1,1,0,4],[2,2,1,9]]
[0, 0, 0]
# expected == result

## cannot take special offer
[2,5]
[[3,0,5],[1,2,10]]
[2,1]
# expected == result

## can take a special offer multiple times
[2,5]
[[3,0,5],[1,2,10]]
[6, 2]
# expected == result

## random case
[6,3,6,9,4,7]
[[1,2,5,3,0,4,29],[3,1,3,0,2,2,19]]
[4,1,5,2,2,4]
# ★ expected != result
```
<br>

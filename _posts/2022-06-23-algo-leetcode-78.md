---
title: "(78) Subsets"
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
[Question Link](https://leetcode.com/problems/subsets/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-23
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
res [[]]

for num in nums
    res에 있는 것들을 돌면서 append num한 결과를 다시 res에 append

'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        
        res = [[]]
        
        for num in nums:
            new = []
            for r in res:
                new.append(r + [num])
            res.extend(new)
        return res
```
<br>

#### <u>디버깅</u>
```python
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
expected == result
```

---
---

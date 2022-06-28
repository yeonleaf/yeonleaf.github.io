---
title: "(95) Unique Binary Search Trees II"
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
[Question Link](https://leetcode.com/problems/unique-binary-search-trees-ii/)

<br>

---
---
 
## **CODE 1**: 실패!
### <u>날짜</u> 2022-06-28
#### <u>총 소요시간</u> 

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/unique-binary-search-trees-ii/discuss/929000/Recursive-solution-long-explanation)
```python
binary search tree의 규칙 (왼쪽은 node보다 작은 값, 오른쪽은 node보다 큰 값)을 지켜야 함
start, end
for cur in range(start, end+1):
    left = rec(start, cur-1)
    right = rec(cur+1, end)
```

---
---

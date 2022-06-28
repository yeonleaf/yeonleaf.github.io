---
title: "(103) Binary Tree Zigzag Level Order Traversal"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need optimization]

toc: true

date: 2022-06-28
last_modified_at: 2022-06-28
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-28
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
res []

rec(루트, 레벨)
    len(res) <= lev:
        res.append([])
    res[lev].append(root.val)
    rec(root.left, lev+1)
    rec(root.right, lev+1)

res의 짝수 원소를 뒤집기
return res
'''
```

<br>

#### <u>코드</u>
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        
        res = []
        
        def rec(root, lev):
            if not root:
                return
            
            if len(res) <= lev:
                res.append([])
            
            res[lev].append(root.val)
            rec(root.left, lev+1)
            rec(root.right, lev+1)
        
        rec(root, 0)
        
        for i, _ in enumerate(res):
            if i%2:
                res[i] = reversed(res[i])
        
        return res
```
<br>

#### <u>디버깅</u>
```python
[2, 1]
expected == result

[2, 1, null, 3, null, 4, null, 6, null]
expected == result

[2, 1, null, 3, 4, null, 5, 6]
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/discuss/33815/My-accepted-JAVA-solution)
reversed 함수 없이 풀어보기

---
---

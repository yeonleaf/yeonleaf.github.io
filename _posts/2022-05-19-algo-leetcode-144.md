---
title: "(144) Binary Tree Preorder Traversal"
excerpt: "binary tree"

categories:
    - algorithm
tags:
    - [leetcode, easy, binary tree, need optimization]

toc: true

date: 2022-05-19
last_modified_at: 2022-05-19
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/binary-tree-preorder-traversal/)

<br>

---
---
 
## **CODE 1**:
### <u>날짜</u> 2022-05-19
#### <u>총 소요시간</u> 1h

<br>

#### <u>설계</u>
```python
'''
루트 - 왼 - 오
'''
```

#### <u>코드</u>
```python
from collections import deque
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        
        if not root:
            return
        
        node = deque()
        node.append(root)
        other = deque()
        
        res = []
        
        while node:
        
            while node:
                cnode = node.popleft()
                res.append(cnode.val)
                if cnode.left:
                    node.appendleft(cnode.left)
                if cnode.right:
                    other.appendleft(cnode.right)
            if other:
                node.append(other.popleft())
        return res
```

#### <u>디버깅</u>
```python
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/binary-tree-preorder-traversal/discuss/45290/Python-solutions-(recursively-and-iteratively).)

오.... 루트 -> 왼 -> 오를 루트 -> 오 -> 왼으로 거꾸로 탐색하는 방법
```python
def preorderTraversal(self, root):
    stack, res = [root], []
    while stack:
        node = stack.pop()
        if node:
            res.append(node.val)
            stack.append(node.right)
            stack.append(node.left)
    return res
```
---
---

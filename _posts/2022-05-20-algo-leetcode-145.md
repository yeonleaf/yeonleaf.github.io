---
title: "(145) Binary Tree Postorder Traversal"
excerpt: " "

categories:
    - algorithm
tags:
    - [leetcode, medium, binary tree, need optimization]

toc: true

date: 2022-05-20
last_modified_at: 2022-05-20
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/binary-tree-postorder-traversal/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-05-20
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''
루트 -> 오 -> 왼 탐색 후 res를 뒤집기
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
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        
        node = deque()
        
        if root:
            node.append(root)
        
        res = []
        
        while node:
            cnode = node.popleft()
            res = [cnode.val] + res

            if cnode.left:
                node.appendleft(cnode.left)
            if cnode.right:
                node.appendleft(cnode.right)
        
        return res
```

#### <u>디버깅</u>
```python
[1, 2, null, null, 3, 4, 5]
expected == result

[1, 2, null, 3, null, 4, null, 5]
expected == result


```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/binary-tree-postorder-traversal/discuss/45582/A-real-Postorder-Traversal-.without-reverse-or-insert-4ms)

하나씩 넣고 두 개씩 append하는 부분 잘 봐두기

```python
def postorderTraversal(self, root: TreeNode) -> List[int]:
    ret = []
    if not root: return ret
    st = [root] * 2
    while st:
        cur = st.pop()
        if st and st[-1] is cur:
            if cur.right:
                st += [cur.right] * 2
            if cur.left:
                st += [cur.left] * 2
        else:
            ret.append(cur.val)
    return ret
```
---
---

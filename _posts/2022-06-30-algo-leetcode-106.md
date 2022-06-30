---
title: "(106) Construct Binary Tree from Inorder and Postorder Traversal"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, complete success]

toc: true

date: 2022-06-30
last_modified_at: 2022-06-30
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-30
#### <u>총 소요시간</u> 45m

<br>

#### <u>설계</u>
```python
'''
왼 루트 오
왼 오 루트

makeTree(inorder, postorder)
if postorder:
    root postorder에서 pop()
    
    ridx inorder에서 root의 위치 찾기
    
    root.right = makeTree(inorder[ridx+1:])
    root.left = makeTree(inorder[:ridx])
    
    return root

'''
```

<br>

#### <u>코드</u>

postorder는 nonlocal 범위에 두어야 함
postorder는 왼 오 루트 -> 루트 오 왼 순으로 탐색

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> Optional[TreeNode]:

        self.pos = postorder
        
        def makeTree(ino):
            if ino:
                rval = self.pos.pop()
                root = TreeNode(rval)

                ridx = ino.index(rval)
                
                root.right = makeTree(ino[ridx+1:])
                root.left = makeTree(ino[:ridx])
                
                return root
        
        return makeTree(inorder)
```
<br>

---
---

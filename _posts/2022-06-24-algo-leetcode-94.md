---
title: "(94) Binary Tree Inorder Traversal"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, need optimization, ⭐]

toc: true

date: 2022-06-24
last_modified_at: 2022-06-27
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/binary-tree-inorder-traversal/)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-06-24
#### <u>총 소요시간</u> 

iterative solution 어렵네...
<br>

#### <u>다른 방식</u>
[Discusstion Link]()
```python
# iteratively       
def inorderTraversal(self, root):
    res, stack = [], []
    while True:
        while root:
            stack.append(root)
            root = root.left
        if not stack:
            return res
        node = stack.pop()
        res.append(node.val)
        root = node.right
```

---
---


<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-27
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
stack []
res []
        
not root일때까지 stack에 저장 -> 왼쪽으로 이동을 반복한다.

n1 stack.pop()한 뒤 n1.val을 방문한다. (res에 넣기)
n1의 오른쪽 노드가 있다면 root = n1.right
오른쪽 노드가 없고 스택에 원소가 들어 있으면 root = stack.pop()
루트 - 왼 - 오

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
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        
        stack, res = [], []
        
        while True:
            while root:
                stack.append(root)
                root = root.left
            if not stack:
                break
            mid = stack.pop()
            res.append(mid.val)
            if mid.right:
                root = mid.right
            else:
                if stack:
                    root = stack.pop()
                    root.left = None
                else:
                    break
        return res
```
<br>

#### <u>디버깅</u>
```python
[1,2,3,4,5,6,7]
expected == result

[1,null,2,null,3,null,4]
expected == result

[1,null,2,3,4,null,5]
expected == result

[1, 2]
expected == result

[1, null, 2]
expected == result
```
<br>

---
---

---
title: "(94) Binary Tree Inorder Traversal"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, saw discussion, ⭐]

toc: true

date: 2022-06-24
last_modified_at: 2022-06-24
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

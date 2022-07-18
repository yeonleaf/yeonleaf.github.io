---
title: "(114) Flatten Binary Tree to Linked List"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need optimization]

toc: true

date: 2022-07-18
last_modified_at: 2022-07-18
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-07-18
#### <u>총 소요시간</u> 50m

<br>

#### <u>설계</u>
```python
'''
root
left, right

if not left:
    return root

fleft = root의 left을 flatten한다.
fright = root의 right을 flatten한다.
fleft.right = fright
root.right = fleft
return root

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
    def flatten(self, root: Optional[TreeNode]) -> None:

        def flat(root):
            if not root:
                return 
            
            if not root.left:
                return root

            fleft = flat(root.left)
            fright = flat(root.right)
            
            cur = fleft
            while cur.right:
                cur = cur.right
            
            cur.right = fright
            
            root.left = None
            root.right = fleft
            return root
        flat(root)   
```
<br>

#### <u>디버깅</u>
```python
[1,2,5,3,null,null,6]
expected == result

[1, 2]
expected == result

[1,2,5,3,4,6]
expected == result

[1,null,2,null,3,null,4,null,5,null,6]
expected == result

[1, null, 2, 3]
expected != result
```
<br>

#### <u>코드2</u>
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def flatten(self, root: Optional[TreeNode]) -> None:

        def flat(root):
            if not root:
                return

            fleft = flat(root.left)
            fright = flat(root.right)
            
            cur = fleft
            while cur and cur.right:
                cur = cur.right
            
            if cur:
                cur.right = fright
                root.left = None
                root.right = fleft
                return root
            else:
                root.right = fright
                return root
        flat(root) 
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/discuss/36977/My-short-post-order-traversal-Java-solution-for-share)

reversed tree-order traversal

```java
private TreeNode prev = null;

public void flatten(TreeNode root) {
    if (root == null)
        return;
    flatten(root.right);
    flatten(root.left);
    root.right = prev;
    root.left = null;
    prev = root;
}
```
---
---

<br>

#### <b> ✅ 최종 comment </b>
---
title: "(173) Binary Search Tree Iterator"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, binary search, binary tree, saw discussion]

toc: true

date: 2022-06-08
last_modified_at: 2022-06-09
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/binary-search-tree-iterator/)

<br>

---
---
 
## **CODE 1**: 시간 초과 (풀이 생각이 안 남)
### <u>날짜</u> 2022-06-08
#### <u>총 소요시간</u>

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/binary-search-tree-iterator/discuss/52526/Ideal-Solution-using-Stack-(Java))
```python

```

---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-09
#### <u>총 소요시간</u> 38m

<br>

#### <u>설계</u>
```python
# 초기화
# inorder traversal 그대로 왼쪽 노드를 쭉 탐색해서 내려가기
# node.left가 없을 때까지 탐색, 탐색하면서 각 노드를 저장해 주기 (father)

# next() 호출 시 현재 커서를 반환
# node.right가 있는지 확인, 있으면 node = node.right
# node.right가 없으면 father에서 노드를 꺼내서 반환하기 node = father
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
class BSTIterator:

    def __init__(self, root: Optional[TreeNode]):
         
        self.stack = []
        self.pointer = root
        
        while self.pointer.left:
            self.stack.append(self.pointer)
            self.pointer = self.pointer.left

    def next(self) -> int:
        res = self.pointer.val
        if self.pointer.right:
            self.pointer = self.pointer.right
            while self.pointer.left:
                self.stack.append(self.pointer)
                self.pointer = self.pointer.left
        else:
            if self.stack:
                self.pointer = self.stack.pop()
            else:
                self.pointer = self.pointer.right
        return res
    
    def hasNext(self) -> bool:
        if self.stack or self.pointer:
            return True
        return False


# Your BSTIterator object will be instantiated and called as such:
# obj = BSTIterator(root)
# param_1 = obj.next()
# param_2 = obj.hasNext()
```
<br>

#### <u>디버깅</u>
```python
["BSTIterator","next","next","hasNext","next","hasNext","next","hasNext","next","hasNext"]
[[[7, 3, 15, 1, 4, 9, 20]],[],[],[],[],[],[],[],[],[]]
expected == result

["BSTIterator","next","hasNext"]
[[[7]],[],[]]
expected == result
```
---
---

---
title: "(95) Unique Binary Search Trees II"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, saw discussion, ⭐]

toc: true

date: 2022-06-28
last_modified_at: 2022-06-29
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

<br>

---
---
 
## **CODE 2**: 실패!
### <u>날짜</u> 2022-06-29
#### <u>총 소요시간</u> 34m

<br>

#### <u>설계</u>
```python
'''
1, n

start > end
    return None

start == end:
    return TreeNode(start)

cur in start, end+1
    root = TreeNode(cur)
    left = rec(start, cur-1)
    right = rec(cur+1, end)
    root.left = left
    root.right = right
    self.res.append(root)
    
'''
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/unique-binary-search-trees-ii/discuss/929000/Recursive-solution-long-explanation)
```python
for left_subtree in all_left_subtrees:   # get each possible left subtree
    for right_subtree in all_right_subtrees: # get each possible right subtree
        # create root node with each combination of left and right subtrees
        curRoot = TreeNode(curRootVal) 
        curRoot.left = left_subtree
        curRoot.right = right_subtree
```

---
---

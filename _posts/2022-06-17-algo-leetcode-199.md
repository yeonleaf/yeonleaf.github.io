---
title: "(199) Binary Tree Right Side View"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, binary tree, bfs, dfs, need optimization]

toc: true

date: 2022-06-17
last_modified_at: 2022-06-17
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/binary-tree-right-side-view/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-17
#### <u>총 소요시간</u> 40m

<br>

#### <u>설계</u>
```python
'''
stack = []
(node, lev) 형태로 저장
만약 right side가 없으면???
노드를 스택에 저장하면서 내려가야 함

현재 노드를 저장
    현재 노드가 res에 있으면 저장하지 않음
right가 있으면
    right를 None으로 바꾼 노드를 stack에 저장
    right로 이동
right가 없으면
    left가 있는지 확인
        left가 있으면
            left를 None으로 바꾼 노드를 stack에 저장
            left로 이동
        left가 없으면
            stack에서 이전 레벨의 노드를 가져옴
            
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
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        
        cur = []

        if root:
            cur.append((root, 0))

        par = []
        
        res = []
        
        while cur or par:
            croot, clev = cur.pop()
            if len(res) <= clev:
                res.append(croot.val)
            
            if croot.right:
                cur.append((croot.right, clev+1))
                croot.right = None
                par.append((croot, clev))
            else:
                if croot.left:
                    cur.append((croot.left, clev+1))
                else:
                    if par:
                        cur.append(par.pop())
        
        return res
```
<br>

#### <u>디버깅</u>
```python
[1, 2, 3, 4, null, null, null]
expected == result

[1, 2, 3, null, null, 4, null]
expected == result

[1, 2, null, null, 3, 4, null]
expected == result

[1, 2, null, 3, null, 4]
expected == result

[1, null, 2, null, 3, null, 4]
expected == result

# base case 수정 (root가 None인 경우)
before
cur = [(root, 0)]

after
cur = []
if root:
    cur.append((root, 0))
```

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/binary-tree-right-side-view/discuss/56012/My-simple-accepted-solution(JAVA))

오 - 왼 순으로 방문하되
currDepth == result.size()일 때만 add해주기

* DFS
```java
public class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        rightView(root, result, 0);
        return result;
    }
    
    public void rightView(TreeNode curr, List<Integer> result, int currDepth){
        if(curr == null){
            return;
        }
        if(currDepth == result.size()){
            result.add(curr.val);
        }
        
        rightView(curr.right, result, currDepth + 1);
        rightView(curr.left, result, currDepth + 1);
        
    }
}
```

* BFS
```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        if (root == null)
            return new ArrayList();
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(root);
        List<Integer> res = new ArrayList();
        
        while(!queue.isEmpty()){
            int size = queue.size();
            
            while (size -- > 0){
                TreeNode cur = queue.poll();
                if (size == 0)
                    res.add(cur.val);
                
                if (cur.left != null)
                    queue.offer(cur.left);
                if (cur.right != null)
                    queue.offer(cur.right);
            }
        }
        
        return res;
    }
}
```

---
---

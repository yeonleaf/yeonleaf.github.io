---
title: "(138) Copy List with Random Pointer
"
excerpt: "linked-list"

categories:
    - algorithm
tags:
    - [leetcode, linked-list(single), DFS, need optimization]

toc: true

date: 2022-05-16
last_modified_at: 2022-05-16
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/copy-list-with-random-pointer/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-05-16
#### <u>총 소요시간</u> 30m

<br>

#### <u>설계</u>
```python
'''
hash {}
node: clone 형식으로 저장
dfs node
if not node:
    return
if node in hash:
    return node
    
hash[node] = Node(node.val)
if node.random:
    hash[node].random = hash[dfs(node.random)]
else:
    hash[node].random = null
hash[node].next = hash[dfs(node.next)]
return hash[node]
'''
```

#### <u>코드</u>
```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        
        if not head:
            return 
        
        dic = {}
        
        def dfs(node):
            if not node:
                return 
            if node in dic:
                return dic[node]
            
            dic[node] = Node(node.val)
            dic[node].random = dfs(node.random)
            dic[node].next = dfs(node.next)
            return dic[node]
        
        dfs(head)
        return dic[head]
```

#### <u>디버깅</u>
```python
## n == 0
[]
# expected != result (fix)

## all node.random values are null
[[3,null],[3,null],[3,null]]
# expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/copy-list-with-random-pointer/discuss/1842579/Python-or-With-and-Without-Hashmap-or-Simple-and-Elegant-Solutions-With-Explanation)
```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head:
            return None
        
        # Add the copied node without random pointer just after its corresponding original node.
        node = head
        while node:
            copiedNode = Node(node.val, node.next)
            node.next = copiedNode
            node = copiedNode.next
        
        """
            Update the random pointer of each copied node by using the below logic-
                Let's say the copied node is c_node and it's original node is o_node then the random pointer of c_node would be the next node of random pointer of o_node because we have placed each copied node just after it's original node. 
        """
        node = head
        while node:
            copiedNode = node.next
            if node.random:
                copiedNode.random = node.random.next
            node = copiedNode.next
        
        # Now just remove the original nodes from the list and return the remaining list as the remaining nodes of the list would make the deep copied list of original list.
        copiedHead = head.next
        node = head
        while node:
            copiedNode = node.next
            node.next = copiedNode.next
            node = node.next
            if copiedNode.next:
                copiedNode.next = copiedNode.next.next
                copiedNode = copiedNode.next
        return copiedHead
```
---
---

<br>


---
title: "(203) Remove Linked List Elements"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, complete success]

toc: true

date: 2022-07-20
last_modified_at: 2022-07-20
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/remove-linked-list-elements/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-07-20
#### <u>총 소요시간</u> 20m

<br>

#### <u>코드</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        
        dummy = ListNode()
        dummy.next = head
        
        pre = cur = dummy
        cur = cur.next
        
        while cur:
            if cur.val == val:
                cur = cur.next
                pre.next = cur
            else:
                pre = pre.next
                cur = cur.next
        
        return dummy.next    
```
<br>

#### <u>디버깅</u>
```python
[3, 1, 2, 4, 5, 3]
3
expected == result

[1, 2, 3, 4, 5, 6]
7
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/remove-linked-list-elements/discuss/158651/Simple-Python-solution-with-explanation-(single-pointer-dummy-head).)

굳이 pre, cur 두 개의 포인터를 쓸 필요도 없다.
cur.val == val이면 cur.next = cur.next.next

```python
class Solution:
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        
        dummy_head = ListNode(-1)
        dummy_head.next = head
        
        current_node = dummy_head
        while current_node.next != None:
            if current_node.next.val == val:
                current_node.next = current_node.next.next
            else:
                current_node = current_node.next
                
        return dummy_head.next
```

---
---

<br>

#### <b> ✅ 최종 comment </b>
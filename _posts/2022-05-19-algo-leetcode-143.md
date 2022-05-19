---
title: "(143) Reorder List"
excerpt: "linked-list"

categories:
    - algorithm
tags:
    - [leetcode, medium, linked-list(single), saw discussion]

toc: true

date: 2022-05-19
last_modified_at: 2022-05-19
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/reorder-list/)

<br>

---
---
 
## **CODE 1**: TLE
### <u>날짜</u> 2022-05-19
#### <u>총 소요시간</u> 설계~코드작성 (30m) + 20m (시간 초과)

<br>

#### <u>설계</u>
```python
'''
head
cur

cur = head
while문 돌려서 head의 마지막 노드를 찾기
left = head.next
cur.next = recursion(left)
head.next = cur
return head
'''
```

#### <u>코드</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        
        def recursion(head):
            if not head:
                return 
            if not head.next:
                return head
            
            pre = head
            cur = head
            while cur.next:
                pre = cur
                cur = cur.next
            pre.next = None
            left = head.next

            cur.next = recursion(left)
            head.next = cur

            return head
        
        return recursion(head)
```

#### <u>디버깅</u>
```python
## number of the node of the list == 1
[1]
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/reorder-list/discuss/801883/Python-3-steps-to-success-explained)
```python
class Solution:
    def reorderList(self, head):
        #step 1: find middle
        if not head: return []
        slow, fast = head, head
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
        
        #step 2: reverse second half
        prev, curr = None, slow.next
        while curr:
            nextt = curr.next
            curr.next = prev
            prev = curr
            curr = nextt    
        slow.next = None
        
        #step 3: merge lists
        head1, head2 = head, prev
        while head2:
            nextt = head1.next
            head1.next = head2
            head1 = head2
            head2 = nextt
```
---
---

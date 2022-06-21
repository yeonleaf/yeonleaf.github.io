---
title: "(21) Merge Two Sorted Lists"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, linked-list(single), sorting, practice finished]

toc: true

date: 2022-06-20
last_modified_at: 2022-06-20
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/merge-two-sorted-lists/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-20
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
l1, l2
l1.val <= l2.val인 경우
    l1.next = rec(l1.next, l2)
    return l1
아닌 경우
    l2.next = rec(l1, l2.next)
    return l2
    
'''
```

<br>

#### <u>코드</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        
        def rec(l1, l2):
            if not l1 or not l2:
                return l1 or l2
            if l1.val <= l2.val:
                l1.next = rec(l1.next, l2)
                return l1
            else:
                l2.next = rec(l1, l2.next)
                return l2
        
        return rec(l1, l2)
```
<br>

#### <u>디버깅</u>
```python
[1]
[1]
expected == result

[1, 2, 3]
[4, 5, 6]
expected == result
```
<br>

---
---

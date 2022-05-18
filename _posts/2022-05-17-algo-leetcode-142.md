---
title: "(142) Linked List Cycle II
"
excerpt: "linked-list(single) floyd's algorithm"

categories:
    - algorithm
tags:
    - [leetcode, normal, linked-list(single), floyd]

toc: true

date: 2022-05-17
last_modified_at: 2022-05-18
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/linked-list-cycle-ii/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-05-17
#### <u>총 소요시간</u> 25m

<br>

#### <u>코드</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        
        dic = {}
        
        while head:
            if head.next in dic:
                return head.next
            dic[head] = True
            head = head.next
        
        return head
```

#### <u>디버깅</u>
```python
## random debug
[1, 2, 3, 0, 4, 7, 8, 3, -3, 2, 1, 7, 5, -10, -11, 44, 2, 199, 45, 28, 19]
3
# expected == result
```
<br>


#### <u>다른 방식</u>
[Discusstion Link](https://www.youtube.com/watch?v=zbozWoMgKW0&t=2s)

영상 보지 않고 코드로 작성하기

---

<br>

---
title: "(92) Reverse Linked List II"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need optimization]  


toc: true

date: 2022-06-24
last_modified_at: 2022-06-24
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/reverse-linked-list-ii/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-24
#### <u>총 소요시간</u> 50m

<br>

#### <u>설계</u>
```python
'''
pl, l, pr, r

r은 항상 같은 위치에 고정
left-2만큼 움직여서 pl을 찾는다.
right-2만큼 움직여서 pr을 찾는다.

while right - left:
    l = pl.next
    r = pr.next

    pr.next = r.next
    pl.next = r
    r.next = l

    pl = pl.next
    r, pr = pr, r
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
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        
        if left == right:
            return head
        dummy = ListNode()
        dummy.next = head
        pl = dummy
        pr = dummy.next
        
        lmove = left-1 if left-1 >= 0 else 0
        for _ in range(lmove):
            pl = pl.next
        
        rmove = right-2 if right-2 >= 0 else 0
        for _ in range(rmove):
            pr = pr.next
            
        cnt = right - left
        while cnt:
            l = pl.next
            r = pr.next
            
            pr.next = r.next
            pl.next = r
            r.next = l

            nr = pr
            pr = l
            while pr and pr.next != nr:
                pr = pr.next
            pl = pl.next
            r = nr
            cnt -= 1
        return dummy.next
```
<br>

#### <u>디버깅</u>
```python
[1,2,3,4,5]
(2, 3) (2, 4) (3, 4) (3, 5), (4, 5)
expected == result

[1,2,3,4,5]
(2, 2)
expected == result -> base case 추가

[1,2,3,4,5]
1
3
expected != result -> fix

[1, 2, 3, 4, 5]
1
2
expected == result

[1, 2, 3, 4, 5]
1
5
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/reverse-linked-list-ii/discuss/30709/Talk-is-cheap-show-me-the-code-(and-DRAWING))
```python
class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        if not head or m == n: return head
        p = dummy = ListNode(None)
        dummy.next = head
        for i in range(m-1): p = p.next
        tail = p.next

        for i in range(n-m):
            tmp = p.next                  # a)
            p.next = tail.next            # b)
            tail.next = tail.next.next    # c)
            p.next.next = tmp             # d)
        return dummy.next
```

---
---

---
title: "(206) Reverse Linked List"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, need optimization]

toc: true

date: 2022-07-22
last_modified_at: 2022-07-22
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/reverse-linked-list/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-07-22
#### <u>총 소요시간</u> 15m

<br>
iterative solution

#### <u>설계</u>
```python
'''
pre, cur, nxt None head head
nxt = cur.next
cur.next = pre
pre = cur
cur = nxt
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
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:

        pre, cur, nxt = None, head, head
        
        while cur:
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        
        return pre
```

---
---

<br>

---
---
 
## **CODE 2**: 시간 초과!
### <u>날짜</u> 2022-07-22
#### <u>총 소요시간</u> 

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/reverse-linked-list/discuss/58125/In-place-iterative-and-recursive-Java-solution)
```java
public ListNode reverseList(ListNode head) {
    /* recursive solution */
    return reverseListInt(head, null);
}

private ListNode reverseListInt(ListNode head, ListNode newHead) {
    if (head == null)
        return newHead;
    ListNode next = head.next;
    head.next = newHead;
    return reverseListInt(next, head);
}
```

---
---

<br>

#### <b> ✅ 최종 comment </b>
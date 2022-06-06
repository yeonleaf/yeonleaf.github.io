---
title: "(160) Intersection of Two Linked Lists"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, linked-list(single), need optimization]

toc: true

date: 2022-06-03
last_modified_at: 2022-06-04
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/intersection-of-two-linked-lists/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-03
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''
A를 탐색하면서 노드 하나하나를 dict에 저장한다.
B를 탐색하면서 dict에 저장되어 있는 노드들과 비교한다. 만약 A와 B에 같은 노드가 있으면 해당 노드를 반환한다.
B를 모두 탐색했는데 A와 겹치는 노드가 없다면 return 0
'''
```

<br>

#### <u>코드</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        
        Adic = {}
        
        while headA:
            Adic[headA] = True
            headA = headA.next
        
        while headB:
            if headB in Adic:
                return headB
            headB = headB.next
        
        return 0
        
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/intersection-of-two-linked-lists/discuss/49798/Concise-python-code-with-comments)
```python
class Solution:
    # @param two ListNodes
    # @return the intersected ListNode
    def getIntersectionNode(self, headA, headB):
        if headA is None or headB is None:
            return None

        pa = headA # 2 pointers
        pb = headB

        while pa is not pb:
            # if either pointer hits the end, switch head and continue the second traversal, 
            # if not hit the end, just move on to next
            pa = headB if pa is None else pa.next
            pb = headA if pb is None else pb.next

        return pa # only 2 ways to get out of the loop, they meet or the both hit the end=None

# the idea is if you switch head, the possible difference between length would be countered. 
# On the second traversal, they either hit or miss. 
# if they meet, pa or pb would be the node we are looking for, 
# if they didn't meet, they will hit the end at the same iteration, pa == pb == None, return either one of them is the same,None
```

[Discusstion Link](https://leetcode.com/problems/intersection-of-two-linked-lists/discuss/49798/Concise-python-code-with-comments)
```python
class Solution(object):
    def getIntersectionNode(self, A, B):
        if not A or not B: return None

        # Concatenate A and B
        last = A
        while last.next: last = last.next
        last.next = B

        # Find the start of the loop
        fast = slow = A
        while fast and fast.next:
            slow, fast = slow.next, fast.next.next
            if slow == fast:
                fast = A
                while fast != slow:
                    slow, fast = slow.next, fast.next
                last.next = None
                return slow

        # No loop found
        last.next = None
        return None
```
---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-04
#### <u>총 소요시간</u> 15m

<br>

#### <u>설계</u>
```python
'''
pa = headA
pb = headB
headA가 null이면 headB, 아니면 pa = pa.next
headB가 null이면 headA, 아니면 pb = pb.next
'''
```

<br>

#### <u>코드</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:

        pa = headA
        pb = headB
        
        while pa or pb:
            if pa == pb:
                return pa
            
            pa = headB if not pa else pa.next
            pb = headA if not pb else pb.next
        
        return None
```
<br>
---
---


<br>

---
---
 
## **CODE 3**: PRACTICE
### <u>날짜</u> 2022-06-04
#### <u>총 소요시간</u>

<br>

#### <u>코드</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        
        last = headA
        while last.next: last = last.next
        last.next = headB
        
        # pr, pw가 만나는 점을 찾는다.
        fast = slow = headA
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
            if slow == fast:
                fast = headA
                while fast != slow:
                    slow = slow.next
                    fast = fast.next
                last.next = None
                return slow
            
        last.next = None
        
        return None
```
<br>

---
---

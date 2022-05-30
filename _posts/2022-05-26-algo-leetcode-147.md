---
title: "(147) Insertion Sort List"
excerpt: "linked-list(single)"

categories:
    - algorithm
tags:
    - [leetcode, medium, linked-list(single), need optimization]

toc: true

date: 2022-05-26
last_modified_at: 2022-05-30
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/insertion-sort-list/)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-05-26
#### <u>총 소요시간</u> 설계 40m + 시간 초과!

<br>

#### <u>설계</u>
```python
'''
t1
t2
while t1 and t2: 
    c = head
    
    while
        c == t1?
            t1 = t1.next
            t2 = t2.next
            break
        t1.val <= c.val?
            c.next = t2
            t1.next = c
            t1 = t2
            if t2:
                t2 = t2.next
            break
        not?
            c = c.next
'''

```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/insertion-sort-list/discuss/1629811/C%2B%2BPythonJava-2-Simple-Solution-w-Explanation-or-Swap-values-%2B-Pointer-Manipulation-Approaches)

discussion 코드 읽지 않고 설명만 읽고 한 번 다시 풀어보기

---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-05-30
#### <u>총 소요시간</u> 25 + 25 + 10

<br>

#### <u>설계</u>
```python
'''
d   pe, e, pc, c
0   4   2   1   3

head = dummy(5001) - head
pc = head
while
    c = pc.next
    pc.val == 5001이면 첫 노드 (정렬이 완료되었다고 가정)
        pc = pc.next
        continue
        
    첫 노드가 아니면 (탐색 필요)
    pe = head
    e = pe.next (바꾸고 싶은 노드)
    while e.val < c.val:
        pe = pe.next
        e = e.next
    
    pe.next = c
    pc.next = c.next
    c.next = e
    
return head.next
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
    def insertionSortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        
        if not head.next:
            return head
        
        dummy = ListNode(5001)
        dummy.next = head
        
        pc = head
        
        while pc:
            if pc.val == 5001:
                pc = pc.next
                continue
            
            c = pc.next
            if not c:
                break
            
            pe = dummy
            e = pe.next
            while e != c and e.val <= c.val:
                pe = pe.next
                e = e.next
            
            if e.val > c.val:
                pe.next = c
                pc.next = c.next
                c.next = e
            else:
                pc = pc.next
        
        return dummy.next
```
<br>

#### <u>디버깅</u>
```python
[0, 4, 5, 0, 3, 1, 7]

[1]

[2, 1]
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/insertion-sort-list/discuss/1629811/C%2B%2BPythonJava-2-Simple-Solution-w-Explanation-or-Swap-values-%2B-Pointer-Manipulation-Approaches)
```python
class Solution:
    def insertionSortList(self, head):
        dummy, cur_prev, cur = ListNode(-1, head), head, head.next
        while cur:
            j_prev, j, cur_next = dummy, dummy.next, cur.next
            if cur.val > cur_prev.val:
                cur_prev = cur
            else:                
                while j.val < cur.val:
                    j_prev, j = j, j.next
                cur.next = j
                j_prev.next = cur
                cur_prev.next = cur_next
            cur = cur_next
        return dummy.next
```

---
---

---
title: "(86) Partition List"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need optimization, ⭐️]

toc: true

date: 2022-06-23
last_modified_at: 2022-06-23
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/partition-list/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-23
#### <u>총 소요시간</u> 50m

<br>

#### <u>설계</u>
```python
'''
p1
while       
while p1.next가 x보다 큰 원소가 나올 때까지 p1을 이동시킨다.
p2 = p2.next

p3 = p2
while p3.next가 x보다 작은 원소가 나올 때까지 p3을 이동시킨다.

p4 = p3.next

p1.next = p4
p4.next = p2
p3.next = p4.next

p1 = p1.next
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
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        dummy = ListNode()
        dummy.next = head
        p1 = dummy
        
        while p1.next and p1.next.val < x:
            p1 = p1.next
        
        while p1:
            p2 = p1.next
            while p2 and p2.val < x:
                p2 = p2.next
            p3 = p2
            while p3.next and p3.next.val >= x:
                p3 = p3.next

            if not p3.next:
                break
            p4 = p3.next
            
            p3.next = p4.next
            p1.next = p4
            p4.next = p2

            p1 = p1.next
        
        return dummy.next
```
<br>

#### <u>디버깅</u>
```python
# 예제 변형
[1,4,3,2,5,2]
4
expected == result

# 원소가 하나도 없는 경우
[]
0
expected == result

# 원소가 하나만 있는 경우
[1]
2
expected == result

# 모든 원소가 x보다 작은 경우
[1,4,3,2,5,2]
6
expected == result

# 모든 원소가 x보다 큰 경우
[1,4,3,2,5,2]
0
expected == result

# 기타
[2, 1, 3]
1
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/partition-list/discuss/29174/Python-concise-solution-with-dummy-nodes)

x보다 작은 값은 l1에, x보다 크거나 같은 값은 l2에 붙인 뒤 l1와 l2를 합친다.

```python
def partition(self, head, x):
    h1 = l1 = ListNode(0)
    h2 = l2 = ListNode(0)
    while head:
        if head.val < x:
            l1.next = head
            l1 = l1.next
        else:
            l2.next = head
            l2 = l2.next
        head = head.next
    l2.next = None
    l1.next = h2.next
    return h1.next
```

---
---

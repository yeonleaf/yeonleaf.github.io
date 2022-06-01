---
title: "(148) Sort List"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, linked-list(single), practice finished]

toc: true

date: 2022-05-30
last_modified_at: 2022-06-01
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/sort-list/)

<br>

---
---
 
## **CODE 1**:
### <u>날짜</u> 2022-05-30
#### <u>총 소요시간</u> 설계 50 -> 시간 초과

<br>

#### <u>설계</u>
```python
'''
for문으로 head부터 끝까지 딕셔너리에 idx : node 형태로 저장한다. (길이 세기)

quick(head)
head를 pivot으로 두고 while문을 돌린다.
l = 1 r = n-1
while l > r
    pivot보다 큰 값 찾기
    while
    dic[l] < pivot이면
        l += 1
    
    pivot보다 작은 값 찾기
    while
    dic[r] > pivot이면
        r -= 1
    
    교환
    dic[l], dic[r] = dic[r], dic[l]
dic[pivot], dic[r] = dic[r], dic[pivot]

pivot = head.right
head.right = None

return quick(head) + pivot + quick(left)


'''
```

<br>

#### <u>코드</u>
```python
```
<br>

#### <u>디버깅</u>
```python
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/sort-list/discuss/46714/Java-merge-sort-solution)
```java
public class Solution {
  
  public ListNode sortList(ListNode head) {
    if (head == null || head.next == null)
      return head;
        
    // step 1. cut the list to two halves
    ListNode prev = null, slow = head, fast = head;
    
    while (fast != null && fast.next != null) {
      prev = slow;
      slow = slow.next;
      fast = fast.next.next;
    }
    
    prev.next = null;
    
    // step 2. sort each half
    ListNode l1 = sortList(head);
    ListNode l2 = sortList(slow);
    
    // step 3. merge l1 and l2
    return merge(l1, l2);
  }
  
  ListNode merge(ListNode l1, ListNode l2) {
    ListNode l = new ListNode(0), p = l;
    
    while (l1 != null && l2 != null) {
      if (l1.val < l2.val) {
        p.next = l1;
        l1 = l1.next;
      } else {
        p.next = l2;
        l2 = l2.next;
      }
      p = p.next;
    }
    
    if (l1 != null)
      p.next = l1;
    
    if (l2 != null)
      p.next = l2;
    
    return l.next;
  }

}
```

---
---

<br>

---
---
 
## **CODE 2**: Practice
### <u>날짜</u> 2022-05-31
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''

prev null
walk head
fast head
slow, walk, fast로 중앙을 찾기

prev = walk
walk.next
fast.next.next
left, right를 정렬하기
return left, right를 merge하기

merge(left, right)
dummy 빈 리스트노드
cur = dummy

left or right
left가 right보다 작으면
cur.next = left
left = left.next
cur = cur.next

left가 right보다 크면
cur.next = right
right = right.next
cur = cur.next

left and not right이면
남은 left를 cur에 붙이기

not left and right이면
남은 right를 cur에 붙이기
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
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        
        
        def divide(head):
            
            if not head or not head.next:
                return head
            
            prev = None
            walk = head
            fast = head
            
            while fast and fast.next:
                prev = walk
                walk = walk.next
                fast = fast.next.next

            prev.next = None

            left = divide(head)
            right = divide(walk)
            
            return merge(left, right)
        
        def merge(l, r):
            dummy = ListNode()
            cur = dummy
            
            while l and r:
                if l.val <= r.val:
                    cur.next = l
                    l = l.next
                    cur = cur.next
                else:
                    cur.next = r
                    r = r.next
                    cur = cur.next
            
            while l and not r:
                cur.next = l
                l = l.next
                cur = cur.next
            
            while not l and r:
                cur.next = r
                r = r.next
                cur = cur.next
            
            return dummy.next
    
        return divide(head)
```
<br>

---
---

<br>


---
---
 
## **CODE 3**: ACCEPTED
### <u>날짜</u> 2022-06-01
#### <u>총 소요시간</u> 15m


<br>

#### <u>코드</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        
        
        def sort(head):
            
            if not head or not head.next:
                return head
            
            # 리스트를 두 파트로 나눈다.
            prev = None
            slow, fast = head, head
            
            while fast and fast.next:
                prev = slow
                slow = slow.next
                fast = fast.next.next
            
            # 두 리스트를 다시 재귀호출해서 나눈다.
            right = sort(slow)
            prev.next = None
            left = sort(head)
            
            # 두 리스트를 합친다.
            return merge(left, right)
        
        def merge(l, r):
            new = ListNode()
            dummy = new
            while l and r:
                if l.val <= r.val:
                    dummy.next = l
                    l = l.next
                    dummy = dummy.next
                else:
                    dummy.next = r
                    r = r.next
                    dummy = dummy.next
            
            while not l and r:
                dummy.next = r
                r = r.next
                dummy = dummy.next
            
            while l and not r:
                dummy.next = l
                l = l.next
                dummy = dummy.next
            
            return new.next
        
        return sort(head)
```
<br>

---
---

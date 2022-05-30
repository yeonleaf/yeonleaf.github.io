---
title: "(148) Sort List"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, linked-list(single)]

toc: true

date: 2022-05-30
last_modified_at: 2022-05-30
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

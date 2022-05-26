---
title: "(147) Insertion Sort List"
excerpt: "linked-list(single)"

categories:
    - algorithm
tags:
    - [leetcode, medium, linked-list(single), saw discussion]

toc: true

date: 2022-05-26
last_modified_at: 2022-05-26
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

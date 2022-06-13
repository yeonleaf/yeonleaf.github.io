---
title: "(180) Consecutive Numbers"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, sql, saw discussion]

toc: true

date: 2022-06-13
last_modified_at: 2022-06-13
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/consecutive-numbers/)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-06-13
#### <u>총 소요시간</u> 

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://codingspooning.tistory.com/entry/leetcode-MySQL-180-Consecutive-Numbers)
```sql
// Write your MySQL query statement below
select distinct l1.Num ConsecutiveNums
from Logs l1
where 3 = (select count(*)
from Logs l2
where l2.Id between l1.Id and l1.Id+2
and l2.Num = l1.Num)
```

---
---

---
title: "(180) Consecutive Numbers"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, sql, practice finished]

toc: true

date: 2022-06-13
last_modified_at: 2022-06-14
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

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-14
#### <u>총 소요시간</u> 15m

<br>

#### <u>설계</u>
```python
'''
log l1
log l2

3 <= select count(*) l1.num = l2.num and l2.id between l1.id and l1.id+2

'''
```

<br>

#### <u>코드</u>
```sql
/*Write your MySQL query statement below*/
select distinct l1.num as "ConsecutiveNums" from Logs l1
where 3 <= (select count(*) from Logs l2 where l1.num = l2.num and l2.id between l1.id and l1.id+2);
```
<br>


#### <u>디버깅</u>
```sql
{"headers": {"Logs": ["id", "num"]}, "rows": {"Logs": [[1, 1], [2, 1], [3, 3], [4, 3], [5, 3], [6, 3], [7, 3]]}}
expected != result -> fix (중복값 제거)
```
<br>

---
---
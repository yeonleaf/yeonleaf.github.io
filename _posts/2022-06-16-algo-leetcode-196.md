---
title: "(196) Delete Duplicate Emails"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, sql, saw discussion]

toc: true

date: 2022-06-16
last_modified_at: 2022-06-16
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/delete-duplicate-emails/)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-06-16 
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
delete하는데 g1에 없는 값을 select
group화 한 후 하나만 남긴 것을 select (g1)
```

<br>


#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/delete-duplicate-emails/discuss/55614/A-skillful-mysql-solution-avoid-%22-select-and-update-conflict%22)

접근 방향은 대충 맞았음. 내일 다시 한 번 풀어보기
```sql
delete from Person where id not in( 
    select t.id from (
        select min(id) as id from Person group by email
    ) t
)
```

---
---

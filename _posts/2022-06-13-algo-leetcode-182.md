---
title: "(182) Duplicate Emails"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, sql, need optimization]

toc: true

date: 2022-06-13
last_modified_at: 2022-06-13
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/duplicate-emails/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-13
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
# email select
# where count(email) > 1
# group?? email로 ??
```

<br>

#### <u>코드</u>
```sql
/*코드 1*/
select distinct p1.email from Person p1
where 1 < (select count(*) from Person p2 where p1.email = p2.email);

/*코드 2*/
select distinct p1.email 
from Person p1, (select email, count(*) as "cnt" from Person group by email) p2
where p1.email = p2.email and p2.cnt > 1; 
```
<br>


#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/duplicate-emails/discuss/53528/I-have-this-Simple-Approach-anybody-has-some-other-way)
```sql
/*standard approach*/
select email from Person
group by email
having count(*) > 1;

/*self join*/
select distinct a.email
from Person a join Person b
on (a.email = b.email)
where a.id <> b.id;

/*subquery (exists)*/
select distinct p1.email from Person a
where exists(select 1 from Person b where a.email = b.email limit 1, 1);
```

---
---

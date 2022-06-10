---
title: "(175) Combine Two Tables"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, sql, complete success]

toc: true

date: 2022-06-10
last_modified_at: 2022-06-10
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/combine-two-tables/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-10
#### <u>총 소요시간</u> 10m

<br>

#### <u>설계</u>
```python
Person에 있는 Id가 Address에 없는 경우 null을 넣으시오 -> left join
```

<br>

#### <u>코드</u>
```sql
/* Write your MySQL query statement below */
select p.firstName, p.lastName, a.city, a.state from Person p
left join Address a
on p.personId = a.personId;
```
<br>

---
---

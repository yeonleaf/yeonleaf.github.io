---
title: "(181) Employees Earning More Than Their Managers"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, sql, need practice]

toc: true

date: 2022-06-13
last_modified_at: 2022-06-13
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/employees-earning-more-than-their-managers/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-13
#### <u>총 소요시간</u> 25m

<br>

#### <u>설계</u>
```sql
'''
self employee.name Employee join
where managerId가 null이 아닌 회원을 선택 (employee)
employee와 manager(employee)를 inner join (id = managerId)
where employee.salary > manager.salary
'''
```

<br>

#### <u>코드</u>
```sql
select e.name "Employee"
from Employee e
inner join Employee m
on e.managerId is not null and m.id = e.managerId
where e.salary > m.salary;
```
<br>


#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/employees-earning-more-than-their-managers/discuss/53475/A-straightforward-method)
```sql
/*from절에서 Employee를 두 번 선택*/
select e1.name as "Employee"
from Employee e1, Employee e2
where e1.managerId = e2.id and e1.salary > e2.salary;

/*서브쿼리 사용*/
select e.name as "Employee"
from Employee e
where e.salary > (select m.salary from Employee m where m.id = e.managerId);
```

---
---

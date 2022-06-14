---
title: "(184) Department Highest Salary"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need optimization]

toc: true

date: 2022-06-14
last_modified_at: 2022-06-14
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/department-highest-salary/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-14
#### <u>총 소요시간</u> 30m

<br>

#### <u>설계</u>
```sql
'''
department 내에서 highest salary인 사람을 고르기
중복 가능

department d

employee를 검색하는데
서브쿼리로 e.departmentId = d.id인 max(salary)값을 가져오고
해당 max값과 salary값이 동일한 employee를 가져온다.

'''
```

<br>

#### <u>코드</u>
```sql
/*Write your MySQL query statement below*/
select distinct d.name as "Department", e.name as "Employee", e.salary as "Salary" from Department d, Employee e
where e.departmentId = d.id and e.salary = (select max(se.salary) from Employee se where se.departmentId = d.id);
```
<br>

#### <u>디버깅</u>
```sql
/*모든 Employee의 salary가 같은 경우*/
{"headers": {"Employee": ["id", "name", "salary", "departmentId"], "Department": ["id", "name"]}, "rows": {"Employee": [[1, "Joe", 70000, 1], [2, "Jim", 70000, 1], [3, "Henry", 70000, 2], [4, "Sam", 70000, 1], [5, "Max", 70000 , 1]], "Department": [[1, "IT"], [2, "Sales"]]}}
expected != result -> fix (where문에 e.departmentId = d.id 조건이 빠짐)
```

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/department-highest-salary/discuss/53607/Three-accpeted-solutions)
```sql
SELECT D.Name AS Department, E.Name AS Employee, E.Salary 
FROM
	Employee E,
	(SELECT DepartmentId,max(Salary) as max FROM Employee GROUP BY DepartmentId) T,
	Department D
WHERE E.DepartmentId = T.DepartmentId 
  AND E.Salary = T.max
  AND E.DepartmentId = D.id
```

---
---

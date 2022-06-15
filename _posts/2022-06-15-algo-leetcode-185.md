---
title: "(185) Department Top Three Salaries"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, hard, saw discussion]

toc: true

date: 2022-06-15
last_modified_at: 2022-06-15
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/department-top-three-salaries/)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-06-15
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
high earner -> department에서 salary가 가장 높은 세 사람을 조회

Department, Employee, Salary 조회
from Department d, Employee e,
where exists (해당 name, salary department에 Salary를 desc순으로 조회하고 limit 3 1)

'''
```

<br>

#### <u>코드</u>
```python
```
<br>


#### <u>다른 방식</u>

음...이해를 전혀 못하겠군...
틈틈히 와서 다시 읽어보자

[Discusstion Link](https://leetcode.com/problems/department-top-three-salaries/discuss/797620/Three-solutions%3A-window-function-subquery-and-Join)
```sql
SELECT D.Name as Department, E.Name as Employee, E.Salary 
FROM Department D, Employee E, Employee E2  
WHERE D.ID = E.DepartmentId and E.DepartmentId = E2.DepartmentId and 
E.Salary <= E2.Salary
group by D.ID,E.Name having count(distinct E2.Salary) <= 3
order by D.Name, E.Salary desc
```

---
---

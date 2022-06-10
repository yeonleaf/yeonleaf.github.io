---
title: "(177) Nth Highest Salary"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, sql, complete success]

toc: true

date: 2022-06-10
last_modified_at: 2022-06-10 
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/nth-highest-salary/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-10
#### <u>총 소요시간</u> 50m

<br>

#### <u>설계</u>
```python
'''
declare, set은 begin 다음 return 이전에 한다.
return 문 내부에 있는 쿼리에 세미콜론을 붙이면 syntax error가 발생한다.
offset은 첫 번째 행이 0이기 때문에 N-1처리를 해 주어야 한다.
'''
```

<br>

#### <u>코드</u>
```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  declare A int;      
  set A = N-1;

  RETURN (
      # Write your MySQL query statement below.
      select ifnull(
          (select distinct salary from Employee order by salary desc limit A, 1), null) from Employee limit 1
  );
END;
```
<br>
---
---

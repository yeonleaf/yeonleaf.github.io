---
title: "(183) Customers Who Never Order"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, sql, need optimization]

toc: true

date: 2022-06-14
last_modified_at: 2022-06-14
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/customers-who-never-order/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-14
#### <u>총 소요시간</u> 20m

<br>

#### <u>설계</u>
```sql
'''
Customers와 Orders를 left join해서
Orders id 값이 null인 케이스를 반환
'''
```

<br>

#### <u>코드</u>
```sql
/* Write your MySQL query statement below */
select c.name "Customers" from Customers c
left join Orders o
on c.id = o.customerId
where o.id is null;
```
<br>


#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/customers-who-never-order/discuss/53579/Three-accepted-solutions)
```sql
/*서브쿼리를 사용하는 두 가지 방법*/

SELECT A.Name as "Customers" from Customers A
WHERE NOT EXISTS (SELECT 1 FROM Orders B WHERE A.Id = B.CustomerId)

SELECT A.Name as "Customers"  from Customers A
WHERE A.Id NOT IN (SELECT B.CustomerId from Orders B)
```
---
---

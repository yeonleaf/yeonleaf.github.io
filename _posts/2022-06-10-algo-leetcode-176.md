---
title: "(176) Second Highest Salary"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, sql, saw discussion]

toc: true

date: 2022-06-10
last_modified_at: 2022-06-10
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/second-highest-salary/)

<br>

---
---
 
## **CODE 1**: 
### <u>날짜</u> 2022-06-10
#### <u>총 소요시간</u>

<br>

[reference1](https://wakestand.tistory.com/295)

[reference2](https://blog.naver.com/llotti/222160243576)

<br>

#### <u>코드</u>
```sql
/*Write your MySQL query statement below*/
select ifnull(
    (select distinct salary from Employee
    order by salary desc
    limit 1 offset 1), null) as SecondHighestSalary from Employee limit 1;
```
<br>

#### <u>디버깅</u>
```sql
{"headers":{"Employee":["id","salary"]},"rows":{"Employee":[[1,100],[2,200],[3,300]]}}

expected [200]
result [200], [200], [200]

-> fix
(끝에 limit 1을 붙여서 해결)


{"headers":{"Employee":["id","salary"]},"rows":{"Employee":[[1,100],[2,100]]}}
expected [100]
result null

-> fix
distinct 키워드 사용해서 해결
두 값이 동일하기 때문에 second highest value는 없어야 한다. 이 때문에 distinct를 사용해서 중복값을 없애준다.
distinct 키워드를 사용하지 않으면 서브쿼리 절에서
{"headers": ["salary"], "values": [[100]]}
이런 결과가 나오기 때문에 결과적으로 second highest value가 100이 나오게 된다.
```
<br>

---
---

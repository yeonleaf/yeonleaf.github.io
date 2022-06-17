---
title: "(197) Rising Temperature"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, sql, need optimization]

toc: true

date: 2022-06-17
last_modified_at: 2022-06-17
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/rising-temperature/)

<br>

---
---
 
## **CODE 1**: 
### <u>날짜</u> 2022-06-17
#### <u>총 소요시간</u> 15m

<br>

#### <u>코드</u>
```sql
-- Write your MySQL query statement below
select w1.id from Weather w1
where w1.temperature > (select w2.temperature from Weather w2 where w2.recordDate = date_sub(w1.recordDate, interval 1 day));
```
<br>

date_sub(날짜, interval n day) 형식 기억하기
(interval ㅇ day 이거 안 넣으면 syntax error 발생)

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/rising-temperature/discuss/55619/Simple-Solution)
```sql
SELECT wt1.Id 
FROM Weather wt1, Weather wt2
WHERE wt1.Temperature > wt2.Temperature AND 
      TO_DAYS(wt1.DATE)-TO_DAYS(wt2.DATE)=1;
```
```sql
select cur.Id
from Weather cur
join Weather prev
on prev.Date + interval 1 day = cur.Date
where cur.Temperature > prev.Temperature
```
---
---

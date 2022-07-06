---
title: "헤비 유저가 소유한 장소"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, complete success]

toc: true

date: 2022-07-06
last_modified_at: 2022-07-06
---

## **문제 링크**
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/77487)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-07-06
#### <u>총 소요시간</u> 15m

<br>

#### <u>설계</u>
```python
'''
셀프 조인
select distinct s1.id, s1.name, s1.host_id
s1.host_id = s2.host_id and s1.id <> s2.id
'''
```

<br>

#### <u>코드</u>
```sql
-- 코드를 입력하세요
select distinct p1.id, p1.name, p1.host_id
from places p1 inner join places p2
on p1.host_id = p2.host_id and p1.id <> p2.id
order by p1.id;
```
<br>


---
---

<br>

---
---
 
## **CODE 2**: 
### <u>날짜</u> 2022-07-06
#### <u>총 소요시간</u> 

group by 사용해서 풀어보기
<br>

#### <u>설계</u>
```sql
select p1.id, p1.name, p1.host_id from places p1
inner join (
    select host_id from places
    group by host_id
    where count(*) > 2
) p2
on p1.host_id = p2.host_id
order by p1.id;
```

<br>

#### <u>코드</u>
```sql
-- 코드를 입력하세요
select p1.id, p1.name, p1.host_id from places p1
inner join (
    select host_id, count(*) c from places
    group by host_id having c >= 2
) p2
on p1.host_id = p2.host_id
order by id;
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://school.programmers.co.kr/questions/30365)
```sql
-- 코드를 입력하세요
SELECT ID, NAME, HOST_ID
FROM PLACES A
WHERE (SELECT COUNT(HOST_ID) AS count
      FROM PLACES B
      WHERE A.HOST_ID=B.HOST_ID) >1;
```

---
---

#### <b> ✅ 최종 comment </b>
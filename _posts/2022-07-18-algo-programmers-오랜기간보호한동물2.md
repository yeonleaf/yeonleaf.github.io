---
title: "오랜 기간 보호한 동물 (2)"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, complete success]

toc: true

date: 2022-07-18
last_modified_at: 2022-07-18
---

## **문제 링크**
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/59411)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-07-18
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
inner join animal_outs
order by datediff(ao.datetime, ai.datetime) desc limit 2
'''
```

<br>

#### <u>코드</u>
```sql
SELECT ai.animal_id, ai.name from animal_ins ai
inner join animal_outs ao
on ai.animal_id = ao.animal_id
order by datediff(ao.datetime, ai.datetime) desc
limit 2
```

---
---

<br>

#### <b> ✅ 최종 comment </b>
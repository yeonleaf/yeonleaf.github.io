---
title: "오랜 기간 보호한 동물 (1)"
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
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/59044)

<br>

---
---
 
## **CODE 1**: 
### <u>날짜</u> 2022-07-18
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```sql
'''
animal_ins에는 있는데 animal_outs에는 없는 동물
animal_ins를 기반으로 left join, animal_outs가 null인 것만
datetime을 기준으로 오름차순 정렬
limit 3
'''
```

<br>

#### <u>코드</u>
```sql
SELECT ai.name, ai.datetime from animal_ins ai
left join animal_outs ao
on ai.animal_id = ao.animal_id
where ao.animal_id is null
order by ai.datetime
limit 3
```

---
---

<br>

#### <b> ✅ 최종 comment </b>
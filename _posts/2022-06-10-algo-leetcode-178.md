---
title: "(178) Rank Scores"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, sql, need optimization]

toc: true

date: 2022-06-10
last_modified_at: 2022-06-10
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/rank-scores/)

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
score distinct에 rank정보를 붙여서 새 테이블 만들기

Scores를 score에 desc하게 정렬하는데, 아까 만든 테이블과 조인해서 rank도 같이 조회하기

-> MYSQL이 제공하는 함수 사용
'''
```

<br>

#### <u>코드</u>
```sql
# Write your MySQL query statement below
select score, DENSE_RANK() over(order by score DESC) AS 'rank' from Scores;
```
<br>

- RANK() -> 공통 순위만큼 건너뜀 (1, 2, 2, 4)

- DANSE_RANK() -> 공통 순위를 뛰어넘지 않음 (1, 2, 2, 3)

- ROW_NUMBER() -> 공통 순위를 무시함 (1, 2, 3, 4)

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/rank-scores/discuss/456610/MySQL-Two-Simple-Solutions-and-Explanations-for-Beginners)
```sql
SELECT S.Score, COUNT(S2.Score) AS Rank FROM Scores S,
(SELECT DISTINCT Score FROM Scores) S2
WHERE S.Score<=S2.Score
GROUP BY S.Id 
ORDER BY S.Score DESC;
```
---
---

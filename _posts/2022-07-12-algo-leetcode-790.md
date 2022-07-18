---
title: "(790) Domino and Tromino Tiling"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, saw discussion]

toc: true

date: 2022-07-12
last_modified_at: 2022-07-12
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/domino-and-tromino-tiling/)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 
#### <u>총 소요시간</u> 

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://www.notion.so/790-Domino-and-Tromino-Tiling-6529dc44edb7441ea4b2364d56ffbfd2#481f475a2d5645cf9fec4f1c89147fd0)
```python
dp테이블을 두 개 사용
dp1
ㅇㅇㅇㅇ
ㅇㅇㅇㅇ

dp2
[1]
ㅁㅇㅇㅇ
ㅇㅇㅇㅇ

[2]
ㅇㅇㅇㅇ
ㅁㅇㅇㅇ

dp2[i] = dp2[i-1] + dp1[i-1]

(1) dp1[i-1] + tromino
ㅁㅇㅇㅇㅇ
ㅇㅇㅇㅇㅇ
(2) dp2[i-1] [2] + domino
ㅁㅇㅇㅇㅇ
ㅇㅇㅇㅇㅇ

dp1[i] = dp1[i-1] + dp1[i-2] + dp2[i-2] * 2

(1) dp1[i-1] + domino (세로 1개)
ㅇㅇㅇㅇㅇ
ㅇㅇㅇㅇㅇ

(2) dp1[i-2] + domino * 2 (가로 2개)
ㅇㅇㅇㅇㅇ
ㅇㅇㅇㅇㅇ

(3) dp2[i-2] [1] + tromino
ㅇㅇㅇㅇㅇ
ㅇㅇㅇㅇㅇ

(4) dp2[i-2] [2] + tromino
ㅇㅇㅇㅇㅇ
ㅇㅇㅇㅇㅇ
```

---
---

<br>

#### <b> ✅ 최종 comment </b>
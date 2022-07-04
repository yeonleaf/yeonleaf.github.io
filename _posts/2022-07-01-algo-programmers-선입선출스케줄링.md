---
title: "선입 선출 스케줄링"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, saw discussion]

toc: true

date: 2022-07-01
last_modified_at: 2022-07-01
---

## **문제 링크**
[Question Link](https://programmers.co.kr/learn/courses/30/lessons/12920)

<br>

---
---
 
## **CODE 1**: 감이 오지 않음..
### <u>날짜</u> 2022-07-01
#### <u>총 소요시간</u> 

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://dev-note-97.tistory.com/173)
```python
1. 시간을 구하기
1h -> 1의 약수를 가진 cpu
2h -> 2의 약수를 가진 cpu
3h -> 3의 약수를 가진 cpu
따라서 3시간째까지 수행된 작업은 1의 약수의 개수 + 2의 약수의 개수 + 3의 약수의 개수

이분 탐색을 통해 h시간에 할 수 있는 총 작업수가 >= n인 가장 작은 값을 구한다.

2. 남은 작업을 하기 위해 h+1의 약수를 가진 cpu에게 작업을 시켰을 때 작업이 끝나는 지점을 for문으로 찾기
```

---
---

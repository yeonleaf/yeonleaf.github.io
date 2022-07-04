---
title: "(813) Largest Sum of Averages"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium]

toc: true

date: 2022-07-03
last_modified_at: 2022-07-03
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/largest-sum-of-averages/)

<br>

---
---
 
## **CODE 1**: 
### <u>날짜</u> 
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
accu 9 10 12 15 24
s, e
9 

if s > e:
    return 0
elif s == e:
    return nums[e]

res = 0
for c in range(s, e+1):
    s == 0인 경우
    res = max(res, accu[c] + rec(c+1, e))
    아닌 경우
    res = max(res, accu[c] - accu[s-1] + rec(c+1, e))
return res

[9] [1, 2, 3, 9]
[9] [1, 2, 3] [9]
9 + 6 +
'''
```

<br>

#### <u>코드</u>
```python
```
<br>

#### <u>디버깅</u>
```python
```
<br>

#### <u>다른 방식</u>
[Discusstion Link]()
```python
```

---
---

<br>

#### <b> ✅ 최종 comment </b>
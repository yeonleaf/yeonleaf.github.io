---
title: "(354) Russian Doll Envelopes"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, hard, saw discussion]

toc: true

date: 2022-06-30
last_modified_at: 2022-06-30
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/russian-doll-envelopes/)

<br>

---
---
 
## **CODE 1**: WA
### <u>날짜</u> 2022-06-30
#### <u>총 소요시간</u> 50m

<br>

#### <u>설계</u>
```python
'''
envelopes.sort(key = lambda x: x[1])
std = envelopes[0]
cnt = 1
e1이 e2 내부에 들어갈 수 있으면 e2를 선택
들어갈 수 없으면 e1을 선택
w1 h1 w2 h2
std를 갱신해 나가기
h1 == h2 (cnt 갱신하지 않음)
    w1 < w2 -> e1 선택
    w1 >= w2 -> e2 선택
h1 < h2 
    w1 >= w2 [3, 2] [2, 3] -> e1 선택  (e1이 e2 안에 들어갈 수 없음) 
    w1 < w2 -> e2 선택 (e1이 e2 안에 들어갈 수 있음) (cnt 갱신함)
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def maxEnvelopes(self, envelopes: List[List[int]]) -> int:

        envelopes.sort(key = lambda x: x[1])
        w1, h1 = envelopes[0]
        cnt = 1
        
        for w2, h2 in envelopes[1:]:
            if h1 == h2 and w1 > w2:
                w1, h1 = w2, h2
            if h1 < h2 and w1 < w2:
                w1, h1 = w2, h2
                cnt += 1
        return cnt
```
<br>

#### <u>디버깅</u>
```python
[[5,4],[6,4],[6,7],[2,3],[5,3]]
expected == result

[[1, 1]]
expected == result

[[4, 4], [4, 3], [4, 2]]
expected == result

[[1, 5], [2, 4], [3, 3]]
expected == result

[[1, 9], [2, 3], [4, 5], [8, 7]]
expected == result

[[3,4], [1,4], [2,5]]
expected != result -> fix
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/russian-doll-envelopes/discuss/82796/A-Trick-to-solve-this-problem)

greedy : w 기준으로 정렬하고 h가 똑같은 경우 반대로 정렬

[Discusstion Link 2](https://leetcode.com/problems/russian-doll-envelopes/discuss/82763/Java-NLogN-Solution-with-Explanation)

dp 
1. w 기준으로 오름차순, h기준으로 내림차순 정렬
2. h 기준으로 lis
---
---

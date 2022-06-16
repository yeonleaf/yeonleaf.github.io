---
title: "(191) Number of 1 Bits"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, bit manipulation, shift operation, complete success]

toc: true

date: 2022-06-16
last_modified_at: 2022-06-16
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/number-of-1-bits/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-16
#### <u>총 소요시간</u> 15m

<br>

#### <u>설계</u>
```python
'''
비트 내에서 1의 개수를 찾으시오
&연산
>> 1연산
반복
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def hammingWeight(self, n: int) -> int:

        res = 0
        while n:
            res += (n & 1)
            n >>= 1

        return res
```
<br>

---
---

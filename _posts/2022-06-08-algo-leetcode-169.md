---
title: "(169) Majority Element"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, complete success]

toc: true

date: 2022-06-08
last_modified_at: 2022-06-08
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/majority-element/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-08
#### <u>총 소요시간</u> 15m

<br>

#### <u>설계</u>
```python
'''
limit = len(nums) / 2

dic에 num을 저장하면서 나가다가
dic[num] + 1 > limit이면 return num
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        
        limit = len(nums) / 2
        
        dic = {}
        
        for num in nums:
            if num not in dic:
                dic[num] = 1
            else:
                dic[num] += 1
            if dic[num] > limit:
                return num
        
```
<br>

#### <u>디버깅</u>
```python
[1, 2, 2, 2, 2, 4]
expected == result
```

---
---

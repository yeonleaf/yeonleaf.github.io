---
title: "(171) Excel Sheet Column Number"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, complete success]

toc: true

date: 2022-06-07
last_modified_at: 2022-06-07
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/excel-sheet-column-number/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-07
#### <u>총 소요시간</u> 20m

<br>

#### <u>설계</u>
```python
'''
ord(i)-64
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def titleToNumber(self, ctitle: str) -> int:
    
        ctitle = list(ctitle)
        res = 0
        ex = 0
        while ctitle:
            cur = ord(ctitle.pop())-64
            res += (pow(26, ex) * cur)
            ex += 1
        
        return res
```
<br>

#### <u>디버깅</u>
```python
"ATD"
expected == result (1200)
```
---
---

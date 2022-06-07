---
title: "(168) Excel Sheet Column Title"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, saw discussion]

toc: true

date: 2022-06-07
last_modified_at: 2022-06-07
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/excel-sheet-column-title/)

<br>

---
---
 
## **CODE 1**: 시간 초과 -> 힌트 봄
### <u>날짜</u> 2022-06-07
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''
28%26 -> 2


AA -> AZ (27 ~ 27+26)
BB -> BZ (53 ~ 53+26)

자리가 하나 올라가면 +26
701 // 26 -> 26
701 % 26 -> 25

26*26+26
colNum // 26 + 
26 * 1

while colNum <= 26
    str += dic[colNum // 26]
    colNum //= 26
str += dic[colNum]


str += dic[colNum]
p
ZZZ 26*26*26 + 26*26 + 26

AZZ 
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def convertToTitle(self, number: int) -> str:
        
        dic = {}
        for i in range(65, 91):
            dic[i-64] = chr(i)
        
        res = ""
        while number > 0:
            res += dic[number%26]
            number //= 26
        
        return res
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/excel-sheet-column-title/discuss/51404/Python-solution-with-explanation)
```python
class Solution:
    # @return a string
    def convertToTitle(self, num):
        capitals = [chr(x) for x in range(ord('A'), ord('Z')+1)]
        result = []
        while num > 0:
            result.append(capitals[(num-1)%26])
            num = (num-1) // 26
        result.reverse()
        return ''.join(result)
```

---
---

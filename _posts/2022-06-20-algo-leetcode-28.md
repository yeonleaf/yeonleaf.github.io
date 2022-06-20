---
title: "(28) Implement strStr()"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, 구현]

toc: true

date: 2022-06-20
last_modified_at: 2022-06-20
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/implement-strstr/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-20
#### <u>총 소요시간</u> 10m

<br>

#### <u>설계</u>
```python
'''
n = len(needle)
for i, v in enumerate(haystack):
    v == needle[0]이고 haystack[i:i+n] == needle이면 return i
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        
        if needle == "":
            return 0
        
        n = len(needle)
        for i, v in enumerate(haystack):
            if v == needle[0] and haystack[i:i+n] == needle:
                return i
        
        return -1
```
<br>


---
---

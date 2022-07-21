---
title: "(205) Isomorphic Strings"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, saw discussion]

toc: true

date: 2022-07-21
last_modified_at: 2022-07-21
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/isomorphic-strings/)

<br>

---
---
 
## **CODE 1**: WA
### <u>날짜</u> 2022-07-21
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
s와 t의 패턴을 dict에 기록한다.
패턴을 sort한다.
패턴이 같으면 return True 다르면 return False
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        
        dat_s = [0]*201
        dat_t = [0]*201
        
        for w in s:
            dat_s[ord(w)] += 1
        
        for w in t:
            dat_t[ord(w)] += 1
        
        dat_s.sort()
        dat_t.sort()
        
        if dat_s != dat_t:
            return False
        
        n = len(s)
        for i in range(n):
            dat_s[ord(s[i])] -= 1
            dat_t[ord(t[i])] -= 1
            if dat_s[ord(s[i])] != dat_t[ord(t[i])]:
                return False
            
        return True
```
<br>

#### <u>디버깅</u>
```python
"abcdcda"
"eeffggh"
expected != result
# 순서가 바뀌면 안된다!

"adad"
"dada"
expected != result
# replace로 고치면 a -> d로 바뀌면서 dddd가 되고 다음 턴에서 aaaa로 바뀌면서 return False하게 된다.

"bbbaaaba"
"abaaabbb"
expected == result

"bbbaaaba"
"aaabbbba"
expected != result
```

---
---

<br>

---
---
 
## **CODE 2**: WA
### <u>날짜</u> 2022-07-21
#### <u>총 소요시간</u> 

<br>

#### <u>코드</u>
```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        
        si, ti = 0, 0
        n = len(s)
        
        while si < n and ti < n:
            cur_s = s[si]
            while si+1 < n and s[si+1] == cur_s:
                si += 1
            
            cur_t = t[ti]
            while ti+1 < n and t[ti+1] == cur_t:
                ti += 1
            
            if si != ti:
                return False
            si += 1
            ti += 1
        return True
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/isomorphic-strings/discuss/57941/Python-different-solutions-(dictionary-etc).)
```python
class Solution(object):
    def isIsomorphic(self, s, t):
        s2t, t2s = {}, {}
        for i in range(len(s)):
            if s[i] in s2t and s2t[s[i]] != t[i]:
                return False
            if t[i] in t2s and t2s[t[i]] != s[i]:
                return False
            s2t[s[i]] = t[i]
            t2s[t[i]] = s[i]
        return True
```

---
---


<br>

#### <b> ✅ 최종 comment </b>
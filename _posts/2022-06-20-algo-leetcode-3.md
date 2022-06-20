---
title: "(3) Longest Substring Without Repeating Characters"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, sliding window, two pointer, saw discussion]

toc: true

date: 2022-06-20
last_modified_at: 2022-06-20
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

<br>

---
---
 
## **CODE 1**: WA + 시간 초과
### <u>날짜</u> 2022-06-20
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
dic : 문자의 index를 저장함
l, r
r이 
등록된 적 없는 문자일 경우
    res의 길이를 갱신(r-l+1)하고 r += 1
등록된 적 있는 문자일 경우 문자를 하나 지우고 하나 더함 -> 길이는 변하지 않음
    l = dic[s[r]] + 1
    dic[s[r]] = r
    r += 1
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:

        dic = {}
        n = len(s)
        res = 0
        l, r = 0, 0
        while r < n:
            if s[r] not in dic:
                dic[s[r]] = r
                res = max(res, r-l+1)
                r += 1
            else:
                l = dic[s[r]] + 1
                dic[s[r]] = r
                r += 1
        return res
```
<br>

#### <u>디버깅</u>
```python
""
expected == result

"abccba"
expected == result

"abcdefg"
expected == result

"abcddabcddabcdd"
expected == result

"abcdfabcdgabcdh"
expected == result

"tmmzuxt"
expected != result
# l을 갱신하고 나서 l 이전에 있었던 값들을 삭제해야 한다.

```
<br>

#### <u>다른 방식</u>
```python
used = {}
max_length = start = 0
for i, c in enumerate(s):
    if c in used and start <= used[c]:
        start = used[c] + 1
    else:
        max_length = max(max_length, i - start + 1)
        
    used[c] = i


return max_length
```

---
---

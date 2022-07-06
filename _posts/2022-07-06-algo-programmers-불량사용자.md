---
title: "불량사용자"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, complete success]

toc: true

date: 2022-07-06
last_modified_at: 2022-07-06
---

## **문제 링크**
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/64064)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-07-06
#### <u>총 소요시간</u> 21m

<br>

#### <u>설계</u>
```python
'''
banned_id ["fr*d*", "*rodo", "******", "******"]
frodo      frodo      abc123    abc123
fradi      crodo       frodoc   frodoc
범위도 1~8
완전탐색 문제
순서와 관계 없음 (같은 아이디 목록 = 같은 것)

불량 사용자 목록별로 매칭이 되는 이벤트 응모자 아이디 목록을 구한다.
ex) mallist "fr*d*" : ["frodo", "fradi"]

import re
re.fullmatch(pattern, string)

idx, path, results
if idx >= n:
    path.sort()
    if "".join(path) not in set:
        results.append(path)
    return 
for candi in mallist[banned_id[idx]]
    if candi not in path:
        (idx+1, path+[candi], results)
'''
```

<br>

#### <u>코드</u>
```python
import re
def solution(user_id, banned_id):
    
    def check(b, u):
        for i in range(len(u)):
            if b[i] != "*" and b[i] != u[i]:
                return False
        return True
    
    mal_dict = {}
    for bid in banned_id:
        dummy = []
        for uid in user_id:
            if len(bid) != len(uid):
                continue
            if check(bid, uid):
                dummy.append(uid)
        mal_dict[bid] = dummy
    
    n = len(banned_id)
    s = set()
    
    def rec(idx, path):
        nonlocal s, n
        if idx >= n:
            path.sort()
            key = "".join(path)
            if key not in s:
                s.add(key)
            return 
        for candi in mal_dict[banned_id[idx]]:
            if candi not in path:
                rec(idx+1, path+[candi])
    
    rec(0, [])
    return len(s)
```
<br>

---
---

<br>

#### <b> ✅ 최종 comment </b>

dfs 문제 (중복 제거해 주는 게 중요)
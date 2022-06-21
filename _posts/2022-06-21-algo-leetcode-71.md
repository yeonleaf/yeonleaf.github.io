---
title: "(71) Simplify Path"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, stack, complete success]

toc: true

date: 2022-06-21
last_modified_at: 2022-06-21
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/simplify-path/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-21
#### <u>총 소요시간</u> 20m

<br>

#### <u>설계</u>
```python
'''
path = split으로 / 모두 제거

stack

for ele in path:
    ele이 ""이거나 "."이면 continue
    
    ele이 ".."이면 stack이 비었는지 확인하고 pop(), continue
    
    이것도 저것도 아니라면 stack.append(ele)
    
"." -> current directory
".." -> parent directory
한 개 이상의 슬래시는 /로 정리하기
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def simplifyPath(self, path: str) -> str:

        path = path.split("/")
        
        stack = []
        
        for ele in path:
            if ele == "" or ele == ".":
                continue
            if ele == "..":
                if stack:
                    stack.pop()
                continue
            stack.append(ele)
        
        return "/" + "/".join(stack)
```
<br>

#### <u>디버깅</u>
```python
"/home/..a/alpha/../.."
expected == result

"/../../../a/b/c/./../.../../d"
expected == result

"/"
expected == result

"/home/../alpha"
expected == result
```
<br>

---
---

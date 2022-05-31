---
title: "(150) Evaluate Reverse Polish Notation"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, stack, complete sucess]

toc: true

date: 2022-05-31
last_modified_at: 2022-05-31
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-05-31
#### <u>총 소요시간</u> 35m

<br>

#### <u>설계</u>
```python
'''
tokens를 deque로 바꾸기 (popleft 사용하기 위함)
숫자만 있으면 stack에 그냥 넣기
operator가 나오면
stack에서 pop pop 해서 operator로 계산한 결과를 stack에 넣기

while stack and tokens:
    if isnumeric(tokens[0]):
        stack.append(tokens.popleft())
    else:
        op = tokens.popleft()
        n1 = stack.pop()
        n2 = stack.pop()
        stack.append(cal(n1, n2, op))
        
cal(n1, n2, op):
    if op == "+"
    ...
    return 결과값
'''
```

<br>

#### <u>코드</u>
```python
from collections import deque
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        
        def cal(n1, n2, op):
            if op == "+":
                return n1 + n2
            if op == "-":
                return n1 - n2
            if op == "*":
                return n1 * n2
            if op == "/":
                return int(n1 / n2)
        
        tk = deque(tokens)
        stack = []
        
        while tk:
            if tk[0] in ["+", "-", "*", "/"]:
                op = tk.popleft()
                n2 = stack.pop()
                n1 = stack.pop()
                stack.append(cal(n1, n2, op))
            else:
                stack.append(int(tk.popleft()))
        return stack[0]

```
<br>

---
---

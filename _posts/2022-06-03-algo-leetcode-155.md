---
title: "(155) Min Stack"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, stack, practice finished]

toc: true

date: 2022-06-03
last_modified_at: 2022-06-04
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/min-stack/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-03
#### <u>총 소요시간</u> 25m

<br>

#### <u>설계</u>
```python
'''
힙 사용?
push할 때 힙에도 같이 넣기
getMin할 때 heapq.heappop(heap)하면 끝남

하지만 pop의 경우에는?
힙에서 같은 값을 가진 원소를 찾아서 삭제를 해야 하는데 이게 불가능함 (항상 루트를 삭제)

mstack
mstack에 값이 없으면 그냥 append
값이 있고 그 값보다 새 값이 크면 append
작으면 appendleft

pop할 때 mstack에서 값을 찾아서 삭제해야 함
'''
```

<br>

#### <u>코드</u>
```python
from collections import deque

class MinStack:

    def __init__(self):
        self.stack = []
        self.mini = deque()

    def push(self, val: int) -> None:
        self.stack.append(val)

    def pop(self) -> None:
        self.stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return sorted(self.stack)[0]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/min-stack/discuss/49022/My-Python-solution)
```python
class MinStack:

def __init__(self):
    self.q = []

# @param x, an integer
# @return an integer
def push(self, x):
    curMin = self.getMin()
    if curMin == None or x < curMin:
        curMin = x
    self.q.append((x, curMin));

# @return nothing
def pop(self):
    self.q.pop()


# @return an integer
def top(self):
    if len(self.q) == 0:
        return None
    else:
        return self.q[len(self.q) - 1][0]


# @return an integer
def getMin(self):
    if len(self.q) == 0:
        return None
    else:
        return self.q[len(self.q) - 1][1]
```

---
---


<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-04
#### <u>총 소요시간</u>

<br>

#### <u>코드</u>
```python
'''
스택 하나 사용

(val, minval)


push::
lastMin = stack[-1][1]
stack.append((val, max(lastMin, val)))

getMin:
return stack[-1][1]
'''

class MinStack:

    def __init__(self):
        self.stack = []

    def push(self, val: int) -> None:
        if not self.stack:
            self.stack.append((val, val))
        else:
            lastMin = self.stack[-1][1]
            self.stack.append((val, min(lastMin, val)))

    def pop(self) -> None:
        self.stack.pop()

    def top(self) -> int:
        return self.stack[-1][0]

    def getMin(self) -> int:
        return self.stack[-1][1]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```

---
---

---
title: "(42) Trapping Rain Water"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, hard, stack, practice finished]

toc: true

date: 2022-06-21
last_modified_at: 2022-06-21
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/trapping-rain-water/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-21
#### <u>총 소요시간</u> 35m

<br>

#### <u>설계</u>
```python
'''
stack (index 저장)

trapped된다는 것 : i < i+1일 경우 trapped될 가능성이 있다고 본다.

i, v in height
stack에 아무것도 없으면 i를 그냥 넣는다.

stack and stack[-1] < v이면 trapped되었다고 본다.
    right = i (index)
    bottom = stack.pop() (index)
    while문을 돌려서 h보다 큰 left(index)를 찾는다. (pop하면 안 됨!)
    res += 너비(h-left) * 높이(height[left] - height[bottom])

return res
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        
        stack = []
        
        res = 0
        
        for i, v in enumerate(height):
            while stack and height[stack[-1]] < v:
                bidx = stack.pop()
                if not stack:
                    break
                lidx = stack[-1]
                res += ((i - lidx - 1) * (min(v, height[lidx]) - height[bidx]))
                print(res)
            stack.append(i)
        
        return res
```

```python
while stack and height[stack[-1]] < v:
```
이 부분이 가장 중요하다.
4, 2, 0, 3, 2, 5 이 예시에서
i가 3일 때 그보다 작은 0, 2를 한 턴에서 모두 해결해야 하기 때문이다.
그러지 않으면 0만 계산하고 2는 계산하지 않은 채 i가 다음으로 넘어가게 된다.

<br>

#### <u>디버깅</u>
```python
[7, 4, 3, 4, 5, 0, 1, 2, 3, 1, 0]
expected == result

[3]
expected == result

[1, 2]
expected == result

[7, 6, 7, 6, 7]
expected == result

[1, 0, 0, 0, 0, 1]
expected == result
```
<br>

---
---

---
title: "(84) Largest Rectangle in Histogram"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, hard, saw discussion, ⭐]

toc: true

date: 2022-06-24
last_modified_at: 2022-06-24
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/largest-rectangle-in-histogram/)

<br>

---
---
 
## **CODE 1**: 시간초과
### <u>날짜</u> 2022-06-24
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
스택에는 인덱스를 저장

0 1 2 3

3일 때
2를 height로 쓸 경우 5* (3-2+1) 10
1을 height로 쓸 경우 1* (3-1+1) 3
0을 height로 쓸 수 없음

현재 원소가 j라고 했을 때 i를 height로 쓸 수 없는 경우
i와 j 사이에 i보다 작은 원소가 있으면 height로 사용할 수 없다.

heights[stack[-1]] < num이면 이후 height로 사용할 수 없으므로 stack.pop() stack.append(num)

(가능한 시작 위치, 원소의 위치)
init = min(heights) * len(heights)

새로운 원소를 추가할 때 고려해야 할 점
1. 가로 길이를 초기화? -> (i, i)
5의 경우 이전 원소인 1보다 크기 때문에 가로 길이를 초기화해야 함

2. 기존의 가로 길이를 연장?
1의 경우 이전 원소인 2보다 작거나 같기 때문에 가로 길이를 연장할 수 있음 -> (stack[-1][0], i)

이 두 가지를 고려한 후 구할 수 있는 넓이의 최댓값을 갱신한다.
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        
        stack = []
        
        res = -1
        
        for i, v in enumerate(heights):
            if not stack:
                res = max(res, v)
                stack.append((i, i))
            else:
                if heights[stack[-1][1]] < v:
                    res = max(res, v)
                    stack.append((i, i))
                else:
                    w = i-stack[-1][0]+1
                    res = max(res, w*v)
                    stack.append((stack[-1][0], i))
        
        return res
```
<br>

#### <u>디버깅</u>
```python
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://abhinandandubey.github.io/posts/2019/12/15/Largest-Rectangle-In-Histogram.html)
```python
class Solution(object):
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        stack = [-1]
        heights.append(0)
        ans = 0
        for i, height in enumerate(heights):
            while heights[stack[-1]] > height:
                h = heights[stack.pop()] 
                w = i - stack[-1] - 1
                ans = max(ans, h*w)
            stack.append(i)
        heights.pop()
        return ans
```

---
---

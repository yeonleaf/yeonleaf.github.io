---
title: "(300) Longest Increasing Subsequence"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need optimization]

toc: true

date: 2022-06-30
last_modified_at: 2022-06-30
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/longest-increasing-subsequence/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-30
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
stack []
스택에 아무것도 없으면 stack.append(num)
스택에 뭐가 있으면 binary search로 num이 들어갈 자리 찾기
찾은 자리에 뭐가 있으면 새로운 원소로 교체.
찾은 자리에 뭐가 없으면 append
'''
```

<br>

#### <u>코드</u>
```python
from bisect import bisect_left 

class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:

        stack = []
        
        for num in nums:
            if not stack:
                stack.append(num)
            else:
                lo = bisect_left(stack, num)
                if lo == len(stack):
                    stack.append(num)
                else:
                    stack[lo] = num
        return len(stack)
```
<br>

#### <u>디버깅</u>
```python
[1,2,5,1,2,4,1,2,3,6]
expected == result

[1]
expected == result

[2, 2, 3, 4, 1, 5]
expected == result

# perfect ascending order
[1, 2, 3, 4, 5]
expected == result

# perfect descending order
[5, 4, 3, 2, 1]
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/longest-increasing-subsequence/discuss/1326552/Optimization-From-Brute-Force-to-Dynamic-Programming-Explained!)

top-down + memoization으로 풀이

---
---

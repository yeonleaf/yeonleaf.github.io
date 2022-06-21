---
title: "(34) Find First and Last Position of Element in Sorted Array"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, binary search, practice finished]

toc: true

date: 2022-06-20
last_modified_at: 2022-06-20
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-20
#### <u>총 소요시간</u> 30m

<br>

#### <u>설계</u>
```python
'''
이진탐색

st, ed

while st <= ed
nums[md] < target?
    st = md + 1
nums[md] > target?
    ed = md
nums[md] == target?
    target[st] == target[md] == target[ed]?
        return [st, ed]
    아닌 경우
        nums[st] < target?
            st += 1
        target < nums[ed]?
            ed -= 1
return [-1, -1]
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:

        st, ed = 0, len(nums)-1
        while st <= ed:
            md = (st + ed) // 2
            if nums[md] < target:
                st = md + 1
            elif nums[md] > target:
                ed = md - 1
            else:
                if nums[st] == nums[md] == nums[ed]:
                    return [st, ed]
                else:
                    if nums[st] < target:
                        st += 1
                    if target < nums[ed]:
                        ed -= 1
        return [-1, -1]
```
<br>

#### <u>디버깅</u>
```python
[7, 7, 7, 7, 7]
7
expected == result

[7]
7
expected == result

[5, 7, 7, 8, 8, 10]
5
expected == result


[5, 7, 7, 8, 8, 10]
10
expected == result

[2, 3, 3, 3, 4, 5, 5, 5, 6]
3
expected == result
```
<br>

---
---

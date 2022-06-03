---
title: "(162) Find Peak Element"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need optimization]

toc: true

date: 2022-06-03
last_modified_at: 2022-06-03
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/find-peak-element/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-03
#### <u>총 소요시간</u> 20m

<br>

#### <u>설계</u>
```python
'''
[1, 2, 3, 4, 5]
여기서 5는 peak인가??
nums[n]은 -inf로 상상하라고 되어 있기 때문에 peak 맞음

O(log n)이면 이진탐색 알고리즘 같은 것을 사용해야 함 (탐색할 때마다 탐색 범위가 줄어들음)

정렬된 배열이 아니다..

peak : neighbor보다 큰 값

n = len(nums)
res = max(nums[0], nums[-1])
i = 1

while문 사용 i < n-1

i-1 < i and i+1 < i이면 peak
    이 경우 i+1은 탐색할 필요가 없으니 건너뛰기
    i = i+2
아니면 i++

'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        n = len(nums)
        
        res = 0
        
        if nums[res] < nums[n-1]:
            res = n-1
        
        i = 1
        
        while i < n-1:
            if nums[i-1] < nums[i] and nums[i+1] < nums[i]:
                if nums[res] < nums[i]:
                    res = i
                i = i+2
            else:
                i += 1
        
        return res
```


#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/find-peak-element/discuss/1290642/intuition-behind-conditions-complete-explanation-diagram-binary-search)

가장 높은 peak을 고르는 문제가 아니라 peak만 발견하면 되는 문제!!!!!!!!

그래서 binary search로 풀 수 있음

---
---

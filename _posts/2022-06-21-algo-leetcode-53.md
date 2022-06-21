---
title: "(53) Maximum Subarray"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, kadane, divide and conquer, need optimization]

toc: true

date: 2022-06-21
last_modified_at: 2022-06-21
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/maximum-subarray/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-21
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
이전 것 더하기 + 이번 것 vs 이번 것

-2 1 -2 4 3 5 6 1 5
max = 6

'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:

        n = len(nums)
        dp = [0]*n
        dp[0] = nums[0]
        
        for i in range(1, n):
            dp[i] = max(nums[i], dp[i-1] + nums[i])
        
        return max(dp)
```
<br>

#### <u>디버깅</u>
```python
[3, -3, 4]
expected == result

# 누적합이 아니라 원소 하나만 선택해야 max를 만들 수 있는 경우
[2, -3, 4]
expected == result

[-1, 0, -1]
expected == result

# 모든 원소를 더해야 (누적합) max를 만들 수 있는 경우
[1, 0, 0, 0, 1]
expected == result
```
<br>

---
---

<br>

---
---
 
## **CODE 2**: 시간 초과
### <u>날짜</u> 2022-06-21 
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
divide and conquer
        
div(l, r)
left = 왼쪽 파트에서 가장 합이 큰 contiguous subarray 찾기
right = 오른쪽 파트에서 가장 합이 큰 contiguous subarray 찾기

return max(left+m, m, m+right)
'''
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/maximum-subarray/discuss/20452/C%2B%2B-DP-and-Divide-and-Conquer)

move to left / move to right 해서 가장 합이 큰 subarray를 구하는 방법이 맞았음

---
---
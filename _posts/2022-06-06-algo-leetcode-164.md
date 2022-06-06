---
title: "(164) Maximum Gap"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, hard, bucket sort, need optimization]

toc: true

date: 2022-06-06
last_modified_at: 2022-06-06
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/maximum-gap/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-06
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''
len(nums) < 2 -> retun 0

sort

O(n)..

1 3 6 9

res
1 ~ n-1까지 
nums[i] - nums[i-1]
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def maximumGap(self, nums: List[int]) -> int:
        
        n = len(nums)
        if n < 2: return 0
        
        form = sorted(nums)
                
        res = 0
        for i in range(1, n):
            res = max(res, form[i] - form[i-1])
        
        return res
```
<br>

#### <u>디버깅</u>
```python
[1, 1, 1, 1, 1]
expected (0) = result (0)

[1, 5, 2, 5, 10, 5]
expected (5) = resuult (5)

[0, 10000, 4, 10000, 2, 30000, 600, 80, 2]
expected != result -> fix


```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/maximum-gap/discuss/1241681/JavaPython-Bucket-Idea-with-Picture-Clean-and-Concise-O(N))

bucket sort::

bucket a, b, c가 있을 때

a의 max값 - b의 min값

b의 max값 - c의 min값

이런 식으로 비교할 수 있다. 같은 bucket 내에 있는 원소들보다 다른 bucket에 있는 원소들이 더 diff값이 크기 때문에 같은 bucket 내에 있는 원소는 비교하지 않는다.

따라서 우리는 각 bucket의 max와 min값만 있으면 된다.


```python
class Solution:
    def maximumGap(self, nums: List[int]) -> int:
        mi, ma, n = min(nums), max(nums), len(nums)
        if mi == ma: return 0  # All elements are the same
        bucketSize = math.ceil((ma - mi) / (n - 1))
        minBucket = [math.inf] * n
        maxBucket = [-math.inf] * n
        for x in nums:
            idx = (x - mi) // bucketSize
            minBucket[idx] = min(minBucket[idx], x)
            maxBucket[idx] = max(maxBucket[idx], x)

        maxGap = bucketSize  # Maximum gap is always greater or equal to bucketSize
        prev = maxBucket[0]  # We always have 0th bucket
        for i in range(1, n):
            if minBucket[i] == math.inf: continue  # Skip empty bucket
            maxGap = max(maxGap, minBucket[i] - prev)
            prev = maxBucket[i]
        return maxGap
```
<br>

---
---

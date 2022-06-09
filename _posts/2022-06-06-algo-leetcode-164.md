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

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-08
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''
max - min // len(nums)-1
9 - 1 // 4 -> 2

mindp 0~2,3~5,6~8,9~11로 나눌 수 있음
maxdp mindp와 동일

nums에 있는 값을 mindp, maxdp에 차례대로 넣기
mindp[nums[i] // len(nums)-1] = min(mindp[[nums[i] // len(nums)-1]], nums[i])

0 1 2 

i = 1부터 끝까지
res와 mindp[i]-maxdp[i-1] 비교
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def maximumGap(self, nums: List[int]) -> int:
        
        n = len(nums)
        
        if n < 2:
            return 0
        
        mi, ni = max(nums), min(nums)
        
        if mi - ni == 0:
            return 0
        
        bkt = math.ceil((mi - ni) / (n - 1))
        
        minNums = [int(1e9)]*n
        maxNums = [-int(1e9)]*n
        
        for num in nums:
            minNums[(num-ni)//bkt] = min(minNums[(num-ni)//bkt], num)
            maxNums[(num-ni)//bkt] = max(maxNums[(num-ni)//bkt], num)  

        res = -int(1e9)
        mi, ni = 0, 1
        while ni < n:
            if minNums[ni] != int(1e9) and maxNums[mi] != -int(1e9):
                res = max(res, minNums[ni] - maxNums[mi])
                mi += 1
                ni += 1
            else:
                if minNums[ni] == int(1e9):
                    ni += 1
                if maxNums[mi] == -int(1e9):
                    mi += 1
        
        return res
```
<br>

#### <u>디버깅</u>
```python
[0, 4, 2, 5, 33]
expected == result

[1, 17, 3, 5, 199, 3, 52, 4]
expected == result

[1, 1, 1, 2, 2, 3]
expected != result -> fix
(division by zero)


```

---
---

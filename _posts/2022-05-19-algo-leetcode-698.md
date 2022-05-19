---
title: "(698) Partition to K Equal Sum Subsets"
excerpt: "백트래킹"

categories:
    - algorithm
tags:
    - [leetcode, medium, BT, saw discussion]

toc: true

date: 2022-05-19
last_modified_at: 2022-05-19
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/)

<br>

---
---
 
## **CODE 1**: WA
### <u>날짜</u> 2022-05-19
#### <u>총 소요시간</u> 설계 ~ 코드 작성 (35m) + 1차 디버깅 (20m) -> 시간 초과

<br>

#### <u>설계</u>
```python
'''
nums, k
k개의 non-empty subset으로 나눌 수 있는가?

subset

nums의 순서는 바뀌어도 상관이 없다.

sum(nums) % k이면 return False

4 3 2 3 5 2 1
T F F F F F T

k == 0이면

n = len(nums)
visited [0] * len(nums)
select [[] for _ in range(k)]

idx == k이면
    if sum(visited) == n (모든 원소를 선택함):
        select의 모든 값이 같은지 확인
        같으면 return True
    return False
for i in range(len(nums)):
    not visited[i]이면
        visited[i] = 1
        selected[idx] += nums[i]
        return dfs(idx+1, visited) or dfs(idx, visited)
        selected[idx] -= nums[i]
        visited[i] = 0
'''
```

#### <u>코드</u>
```python
class Solution:
    def canPartitionKSubsets(self, nums: List[int], k: int) -> bool:
        
        if sum(nums) % k: return False
        
        n = len(nums)
        visited = [0]*n
        select = [0]*k
        
        self.dp = {}
        
        def bt(idx, select, visited):
            if idx == k:
                if sum(visited) == n:
                    if len(set(select)) == 1:
                        return True
                return False
            
            if sum(visited) == n:
                return False
            
            if tuple(select) in self.dp:
                return self.dp[tuple(select)]
            
            res = False
            for i in range(n):
                if not visited[i]:
                    visited[i] = 1
                    select[idx] += nums[i]
                    res = res or bt(idx, select, visited) or bt(idx+1, select, visited)
                    select[idx] -= nums[i]
                    visited[i] = 0
                    
            self.dp[tuple(select)] = res
            return res
        
        return bt(0, select, visited)
```

#### <u>디버깅</u>
```python
## nums.length == k == 1
[1]
1
expected == result

# sum(nums)%k and not result
[1, 4, 2, 5]
3
expected == result

## nums.length == k == 16
[1, 2, 3, 4, 5, 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, 3]
16
expected == result

## nums.length == 16 (true case) ★
[1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4]
4
expected != result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/discuss/180014/Backtracking-x-2)
```python
class Solution:
    def canPartitionKSubsets(self, nums: List[int], k: int) -> bool:
        
        nums_sum = sum(nums)
        if nums_sum % k != 0:
            return False
        subset_sum = nums_sum / k
        
        ks = [0] * k
        nums.sort(reverse=True)
        
        def can_partition(j):
            if j == len(nums):
                for i in range(k):
                    if ks[i] != subset_sum:
                        return False
                return True
            for i in range(k):
                if ks[i] + nums[j] <= subset_sum:
                    ks[i] += nums[j]
                    if can_partition(j + 1):
                        return True
                    ks[i] -= nums[j]
            return False

        return can_partition(0)
```
---
---

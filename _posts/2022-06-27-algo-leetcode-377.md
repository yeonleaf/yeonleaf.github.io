---
title: "(377) Combination Sum IV"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need practice, ⭐]

toc: true

date: 2022-06-27
last_modified_at: 2022-06-27
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/combination-sum-iv/)

<br>

---
---
 
## **CODE 1**: TLE
### <u>날짜</u> 2022-06-27
#### <u>총 소요시간</u> 20m

<br>

#### <u>설계</u>
```python
'''
nums는 distinct하고
같은 원소를 여러 번 선택할 수 있음
순서가 다르면 다른 combination으로 취급

min(nums) > target:
    return 0

rec(sum)
if sum == target:
    res += 1
    return
for i in range(n):
    if sum + nums[i] <= target:
        rec(sum + nums[i])


* negative values가 들어가면?
sum + num <= target 조건이 들어갈 수 없다.
일시적으로 target보다 커지더라도 나중에 음수가 나오면 <= target 조건을 달성할 수 있기 때문이다. 
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:

        if min(nums) > target:
            return 0
        
        self.res = 0
        def rec(accu):
            if accu == target:
                self.res += 1
                return
            for num in nums:
                if accu + num <= target:
                    rec(accu + num)
        
        rec(0)
        return self.res
```
<br>

#### <u>디버깅</u>
```python
[9]
9
expected == result

[1]
1000
expected == result

[1, 2, 3]
6
expected == result

[1, 2, 3]
9
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/combination-sum-iv/discuss/111860/Coin-change-AND-this-problem)

DP 문제
coin change 2 복습

---
---


<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-27
#### <u>총 소요시간</u> 20m

<br>

#### <u>코드</u>
```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        
        dp = [0]*(target+1)
        dp[0] = 1
        
        for i in range(1, target+1):
            for n in nums:
                if i-n >= 0:
                    dp[i] += dp[i-n]
            print(dp)
        return dp[-1]
```
<br>

```python
[1, 2, 3]
4

[1, 1, 0, 0, 0]
[1, 1, 2, 0, 0]
[1, 1, 2, 4, 0]
[1, 1, 2, 4, 7]

i == 3일 경우
[1, 2, 3]
1로 3을 만드는 케이스
1 + 2 케이스
2 + 1 케이스
3 + 0 케이스
를 모두 고려해야 한다.
```

---
---

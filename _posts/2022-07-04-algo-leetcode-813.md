---
title: "(813) Largest Sum of Averages"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, practice finished, ⭐]

toc: true

date: 2022-07-03
last_modified_at: 2022-07-11
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/largest-sum-of-averages/)

<br>

---
---
 
## **CODE 1**: TLE
### <u>날짜</u> 
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
accu 9 10 12 15 24
s, e
9 

if s > e:
    return 0
elif s == e:
    return nums[e]

res = 0
for c in range(s, e+1):
    s == 0인 경우
    res = max(res, accu[c] + rec(c+1, e))
    아닌 경우
    res = max(res, accu[c] - accu[s-1] + rec(c+1, e))
return res

[9] [1, 2, 3, 9]
[9] [1, 2, 3] [9]
9 + 6 +
'''
```

<br>

#### <u>코드</u>
```python
import statistics 
class Solution:
    def largestSumOfAverages(self, nums: List[int], k: int) -> float:
        n = len(nums)
        
        self.dp = {}
        
        def rec(s, e, k):
            if s > e:
                return 0
            
            if k == 1:
                return statistics.mean(nums[s:e+1])
            
            if (s, e, k) in self.dp:
                return self.dp[(s, e, k)]
            res = 0
            for c in range(s, e+1):
                res = max(res, statistics.mean(nums[s:c+1]) + rec(c+1, e, k-1))
            self.dp[(s, e, k)] = res
            return self.dp[(s, e, k)]
        
        return rec(0, n-1, k)
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/largest-sum-of-averages/discuss/122739/C%2B%2BJavaPython-Easy-Understood-Solution-with-Explanation)

귀찮다고 statistics.mean()을 사용해서 TLE가 뜬 것 같다ㅋㅋ...
아래의 방법은 최초 인덱스를 N-1로 두고 내려가는 방식이다. 이렇게 하면 K==1이 되었을 때 sum(A[:n]) / float(n)만으로 평균을 구할 수 있다.
```python
def largestSumOfAverages(self, A, K):
    memo = {}
    def search(n, k):
        if (n, k) in memo: return memo[n, k]
        if n < k: return 0
        if k == 1:
            memo[n, k] = sum(A[:n]) / float(n)
            return memo[n, k]
        cur, memo[n, k] = 0, 0
        for i in range(n - 1, 0, -1):
            cur += A[i]
            memo[n, k] = max(memo[n, k], search(i, k - 1) + cur / float(n - i))
        return memo[n, k]
    return search(len(A), K)
```

---
---

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-07-11
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
i, k (0부터 i까지 k번 나눌 수 있을 때 maximum score)

if k == 0: return sum(nums[:i+1]) / (i+1)
if c < 0: return 0

maxScore = -1
for c in i부터 0까지 -1
    current avg = sum(nums[c:i+1]) / i-c+1
    maxScore = max(maxScore, rec(c-1, k-1) + current avg)
return maxScore
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def largestSumOfAverages(self, nums: List[int], k: int) -> float:
    
        self.memo = {}
        
        def rec(i, k):
            if i < 0: return 0
            if i+1 < k: return -int(1e9)
            if k == 1: return sum(nums[:i+1]) / (i+1)
            
            if (i, k) in self.memo:
                return self.memo[(i, k)]
            
            res = -1
            for c in range(i, -1, -1):
                curVal = sum(nums[c:i+1]) / (i-c+1)
                res = max(res, rec(c-1, k-1) + curVal)
            self.memo[(i, k)] = res
            return self.memo[(i, k)]
        
        n = len(nums)
        return rec(n-1, k)
```
<br>

#### <u>디버깅</u>
```python
[1]
1
expected == result


[1, 3, 4, 5, 7]
5
expected == result


[9,1,2,3,9]
4
expected == result
```

---
---


#### <b> ✅ 최종 comment </b>
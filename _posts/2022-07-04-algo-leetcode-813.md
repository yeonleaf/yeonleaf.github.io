---
title: "(813) Largest Sum of Averages"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, saw discussion]

toc: true

date: 2022-07-03
last_modified_at: 2022-07-06
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

#### <b> ✅ 최종 comment </b>
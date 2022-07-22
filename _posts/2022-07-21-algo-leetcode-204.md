---
title: "(204) Count Primes"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, practice finished]

toc: true

date: 2022-07-21
last_modified_at: 2022-07-21
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/count-primes/)

<br>

---
---
 
## **CODE 1**: TLE
### <u>날짜</u> 2022-07-21
#### <u>총 소요시간</u> 30m

<br>

#### <u>설계</u>
```python
'''
n보다 작은 prime numbers
소수 : 1과 자기 자신으로만 나누어지는 수

2부터 sqrt까지 차례대로 나눠보기. 나눠지는 수가 있으면 소수가 아님 (시간초과)

2부터 n-1까지의 수를 에라스토네스의 체로 필터링 (시간초과)
2를 제외하고 2의 배수 지우기
3을 제외하고 3의 배수 지우기
5를 제외하고 5의 배수 지우기...
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def countPrimes(self, n: int) -> int:

        nums = [1 for _ in range(n)]
        nums[0], nums[1] = 0, 0
        
        d = 2
        
        while d < n:
            # 새로운 d 찾기
            while d <= n-1 and not nums[d]:
                d += 1
                
            # d를 제외하고 d의 배수 지우기
            # 다 확인할 필요는 없고 배수만 확인하면 되는데..
            for i in range(d, n, d):
                if i == d: continue
                if nums[i] and not i % d:
                    nums[i] = 0
                    
            # d 갱신하기
            d += 1
        
        return sum(nums)
        
```
<br>

#### <u>디버깅</u>
```python
0
expected == result

1
expected == result

2
expected == result

5000000
expected == result
```

for문으로 다시 풀어보기 (원리 자체는 잘 접근했음. 함수 최적화가 안 되어서 시간초과가 나는 것 같음)

---
---

<br>

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-07-22 
#### <u>총 소요시간</u> 

<br>

#### <u>코드</u>
```python
import math
class Solution:
    def countPrimes(self, n: int) -> int:

        if n < 2: return 0
        
        nums = [1 for _ in range(n)]
        nums[0], nums[1] = 0, 0
        
        d = 2
        
        for i in range(2, int(math.sqrt(n))+1):
            if nums[i]:
                for j in range(i, n, i):
                    if i == j: continue
                    if nums[j]: nums[j] = 0
        return sum(nums)
        
```


---
---

#### <b> ✅ 최종 comment </b>

소수 구할 때 = 에라스토네스의 체 + 탐색 범위는 math.sqrt(n)+1
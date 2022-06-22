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


<br>

---
---
 
## **CODE 3**: TLE
### <u>날짜</u> 2022-06-22
#### <u>총 소요시간</u> 25m

<br>

#### <u>설계</u>
```python
'''
l, r

l > r -> return 0

m

lsum = 중앙에서 왼쪽으로 넓혀나가면서 largest sum을 가진 contiguous subarray를 찾기
rsum = 중앙에서 오른쪽으로 넓혀나가면서 largest sum을 가진 contiguous subarray를 찾기

return max(lsum + m, rsum + m, m, div(l, m-1), div(m+1, r))
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        
        n = len(nums)
        
        def dq(l, r):
            
            if l > r:
                return 0
            
            if l == r:
                return nums[l]
            
            if r - l == 1:
                return max(nums[l], nums[r], nums[l]+nums[r])
            
            m = (l + r) // 2
            
            lsum = -int(1e9)
            ldum = 0
            for i in range(m-1, -1, -1):
                ldum = ldum + nums[i]
                lsum = max(lsum, ldum)
            
            rsum = -int(1e9)
            rdum = 0
            for i in range(m+1, n):
                rdum = rdum + nums[i]
                rsum = max(rsum, rdum)
                        
            return max(dq(l, m-1), dq(m+1, r), lsum + nums[m], nums[m], nums[m] + rsum, lsum + nums[m] + rsum)
        
        return dq(0, n-1)
```
<br>

#### <u>디버깅</u>
```python
[7, -1, -1, 2, -4, -5]
expected == result


[0, 0, 0]
expected == result


[-2, 1]
expected != result -> fix (원소의 개수가 한 개, 두 개일 때 예외처리 추가)

[2, 2, -3, -4, 0, -2, -2]
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/maximum-subarray/discuss/20452/C%2B%2B-DP-and-Divide-and-Conquer)
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        return maxSubArray(nums, 0, nums.size() - 1);
    }
private:
    int maxSubArray(vector<int>& nums, int l, int r) {
        if (l > r) {
            return INT_MIN;
        }
        int m = l + (r - l) / 2, ml = 0, mr = 0;
        int lmax = maxSubArray(nums, l, m - 1);
        int rmax = maxSubArray(nums, m + 1, r);
        for (int i = m - 1, sum = 0; i >= l; i--) {
            sum += nums[i];
            ml = max(sum, ml);
        }
        for (int i = m + 1, sum = 0; i <= r; i++) {
            sum += nums[i];
            mr = max(sum, mr);
        }
        return max(max(lmax, rmax), ml + mr + nums[m]);
    }
};
```

---
---

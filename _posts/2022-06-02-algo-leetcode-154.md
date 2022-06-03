---
title: "(154) Find Minimum in Rotated Sorted Array II"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, binary search, practice finished]

toc: true

date: 2022-06-02
last_modified_at: 2022-06-03
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-02
#### <u>총 소요시간</u> 약 1시간

<br>

#### <u>설계</u>
```python
'''
nums[m] > nums[r]인 경우
    min값은 무조건 오른쪽 범위에 있음
    
아닌 경우 (nums[m] <= nums[r])
    nums[m]값이 duplicate인 경우
    nums[m]의 시작점을 찾기? (pointer로)
    [4, 4, 0, 0, 0, 0, 0, 1]
    1. nums[m]이 최소값인 경우
        nums[m]의 duplicate가 왼쪽 범위에 없는 경우
        nums[m]의 duplicate가 왼쪽 범위에 있는 경우
        두 경우 모두 right = mid로 두면 해결이 됨
    [4, 4, 0, 1, 1, 1, 1, 1]
    2. nums[m]이 최소값이 아닌 경우
        이 경우 최소값은 왼쪽 범위에 있음
        이 경우에도 right = mid로 두면 됨

    [0, 1, 1, 1, 1, 1]
    
'''
'''
어쨌거나 duplicate값이 나오면 m을 duplicate의 맨 앞으로 옮겨야 함
duplicate?
1 <= m
while nums[m-1] == nums[m]:
    m -= 1



범위를 줄이기
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        
        n = len(nums)
        l, r = 0, n-1
        
        while l < r:
            m = (l + r) // 2
            if nums[m] > nums[r]:
                # duplicate의 오른쪽 끝만 찾으면 됨
                while m < n-1 and nums[m] == nums[m+1]:
                    m += 1
                l = m + 1
            else:
                # 양쪽으로 확장 (duplicate의 처음 위치와 끝 위치를 찾기)
                t = m
                while t < n-1 and nums[t] == nums[t+1]:
                    t += 1

                # t < n-1 and t > t+1인 경우 (오른쪽에 최솟값 후보가 있음)
                if t < n-1 and nums[t] > nums[t+1]:
                    l = t + 1
                else:
                    r = m
        return nums[l]
```
<br>

#### <u>디버깅</u>
```python
[1, 0, 0, 0, 0, 1]

[0, 0, 1, 1, 2, 2, 3, 3, 4, 4]

[3, 3, 1, 2]

[4, 0, 0, 1, 1, 1, 1, 1]

## failed case
[3, 3, 1, 1, 3]
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/discuss/48808/My-pretty-simple-code-to-solve-it)
```java
class Solution {
public:
    int findMin(vector<int> &num) {
        int lo = 0;
        int hi = num.size() - 1;
        int mid = 0;
        
        while(lo < hi) {
            mid = lo + (hi - lo) / 2;
            
            if (num[mid] > num[hi]) {
                lo = mid + 1;
            }
            else if (num[mid] < num[hi]) {
                hi = mid;
            }
            else { // when num[mid] and num[hi] are same
                hi--;
            }
        }
        return num[lo];
    }
};
```
---
---


<br>


---
---
 
## **CODE 2**: PRACTICE
### <u>날짜</u> 2022-06-03
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''
l, m, r
m > r이면 l = m+1
m <= r이면
    m < r인 경우
        r = m
    m == r인 경우
        r -= 1
[3, 1, 1, 1, 1, 1, 3]
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        
        n = len(nums)
        l, r = 0, n-1
        
        while l < r:
            m = (l + r) // 2
            if nums[m] > nums[r]:
                l = m + 1
            else:
                if nums[m] == nums[r]:
                    r -= 1
                else:
                    r = m
        
        return nums[l]
```
<br>

#### <u>디버깅</u>
```python
[3, 3, 1, 3] # 값 대신 인덱스를 쓴 실수 - 수정
```
<br>

---
---

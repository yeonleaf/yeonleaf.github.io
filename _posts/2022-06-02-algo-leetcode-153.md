---
title: "(153) Find Minimum in Rotated Sorted Array"
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
[Question Link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-02
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''
오름차순으로 되어 있는 부분을 찾아야 함
nums
[4, 5, 6, 7, 0, 1, 2]
left는 [4, 5, 6, 7] right는 [0, 1, 2]
left[0]과 right[0]을 비교해서 더 작은 쪽을 리턴

l, r, m
l > r이면 return l

m > r이면 오른쪽으로 이동
아니면 왼쪽으로 이동
m < r
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        
        l, r = 0, len(nums)-1
        
        res = int(1e9)
        
        while l <= r:
            m = (l+r)//2
            if nums[m] > nums[r]:
                res = min(res, nums[r])
                l = m+1
            else:
                res = min(res, nums[m])
                r = m-1
        
        return res
```
<br>

#### <u>디버깅</u>
```python
## minimum nums length(1)
[1]

[2, 3, 4, 5, 1]

[1, 2]
[2, 1]

## failed case ☆☆☆
[3, 1, 2]
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/discuss/158940/Beat-100%3A-Very-Simple-(Python)-Very-Detailed-Explanation)
```python
class Solution:
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # set left and right bounds
        left, right = 0, len(nums)-1
                
        # left and right both converge to the minimum index;
        # DO NOT use left <= right because that would loop forever
        while left < right:
            # find the middle value between the left and right bounds (their average);
			# can equivalently do: mid = left + (right - left) // 2,
			# if we are concerned left + right would cause overflow (which would occur
			# if we are searching a massive array using a language like Java or C that has
			# fixed size integer types)
            mid = (left + right) // 2
                        
            # the main idea for our checks is to converge the left and right bounds on the start
            # of the pivot, and never disqualify the index for a possible minimum value.

            # in normal binary search, we have a target to match exactly,
            # and would have a specific branch for if nums[mid] == target.
            # we do not have a specific target here, so we just have simple if/else.
                        
            if nums[mid] > nums[right]:
                # we KNOW the pivot must be to the right of the middle:
                # if nums[mid] > nums[right], we KNOW that the
                # pivot/minimum value must have occurred somewhere to the right
                # of mid, which is why the values wrapped around and became smaller.

                # example:  [3,4,5,6,7,8,9,1,2] 
                # in the first iteration, when we start with mid index = 4, right index = 9.
                # if nums[mid] > nums[right], we know that at some point to the right of mid,
                # the pivot must have occurred, which is why the values wrapped around
                # so that nums[right] is less then nums[mid]

                # we know that the number at mid is greater than at least
                # one number to the right, so we can use mid + 1 and
                # never consider mid again; we know there is at least
                # one value smaller than it on the right
                left = mid + 1

            else:
                # here, nums[mid] <= nums[right]:
                # we KNOW the pivot must be at mid or to the left of mid:
                # if nums[mid] <= nums[right], we KNOW that the pivot was not encountered
                # to the right of middle, because that means the values would wrap around
                # and become smaller (which is caught in the above if statement).
                # this leaves the possible pivot point to be at index <= mid.
                            
                # example: [8,9,1,2,3,4,5,6,7]
                # in the first iteration, when we start with mid index = 4, right index = 9.
                # if nums[mid] <= nums[right], we know the numbers continued increasing to
                # the right of mid, so they never reached the pivot and wrapped around.
                # therefore, we know the pivot must be at index <= mid.

                # we know that nums[mid] <= nums[right].
                # therefore, we know it is possible for the mid index to store a smaller
                # value than at least one other index in the list (at right), so we do
                # not discard it by doing right = mid - 1. it still might have the minimum value.
                right = mid
                
        # at this point, left and right converge to a single index (for minimum value) since
        # our if/else forces the bounds of left/right to shrink each iteration:

        # when left bound increases, it does not disqualify a value
        # that could be smaller than something else (we know nums[mid] > nums[right],
        # so nums[right] wins and we ignore mid and everything to the left of mid).

        # when right bound decreases, it also does not disqualify a
        # value that could be smaller than something else (we know nums[mid] <= nums[right],
        # so nums[mid] wins and we keep it for now).

        # so we shrink the left/right bounds to one value,
        # without ever disqualifying a possible minimum
        return nums[left]
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
nums[m] > nums[r]이면 l = m+1
아니면 r = m

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
                l = m+1
            else:
                r = m
        
        return nums[l]
```
<br>

---
---

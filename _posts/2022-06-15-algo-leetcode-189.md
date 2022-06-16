---
title: "(189) Rotate Array"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, practice finished]

toc: true

date: 2022-06-15
last_modified_at: 2022-06-16
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/rotate-array/)

<br>

---
---
 
## **CODE 1**: TLE
### <u>날짜</u> 2022-06-15
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
in-place로 하라고?

tmp = 맨 끝의 원소를 담는다.
0부터 n-2까지의 원소를 한 칸씩 앞으로 옮긴다.
nums[0]에 tmp를 담는다.
이 짓을 k번 반복한다.
'''
'''
돌리는 횟수 재조정
n번 돌리면 원래 배열로 돌아온다...
n+1번은 한 번 돌린 것과 동일하다...

k % n
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        
        if n == 1 or not k % n:
            return nums
        
        for _ in range(k%n):
            tmp = nums[-1]
            for i in range(n-2, -1, -1):
                nums[i+1] = nums[i]
            nums[0] = tmp
        
            
```
<br>

deque는 사용 불가능 (in-place로 하라고 했음)

#### <u>다른 방식</u>
힌트 얻음
reversed 활용하기?


#### <u>다른 방식</u>
reversed함수를 사용할 수 없기 때문에 (in-place 규정에 어긋남)
직접 함수를 만들어서 사용해야 함
[Discusstion Link](https://leetcode.com/problems/rotate-array/discuss/54250/Easy-to-read-Java-solution)

---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-16
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
전체 뒤집기
0:k-1까지 뒤집기
k:끝까지 뒤집기

l부터 r까지의 원소를 뒤집는 메서드 만들기

'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        
        n = len(nums)
        
        if n == 1:
            return nums
        
        k %= n
        
        def reverse(l, r):
            
            while l < r:
                nums[l], nums[r] = nums[r], nums[l]
                l += 1
                r -= 1
            
        reverse(0, n-1)
        reverse(0, k-1)
        reverse(k, n-1)
```
<br>

---
---

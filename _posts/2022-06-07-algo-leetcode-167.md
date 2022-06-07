---
title: "(167) Two Sum II - Input Array Is Sorted"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, two pointers, binary search, dictionary, complete success]

toc: true

date: 2022-06-07
last_modified_at: 2022-06-07
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-07
#### <u>총 소요시간</u> 15m

<br>

#### <u>설계</u>
```python
'''
이진탐색

for i1, v in enumerate(numbers):
    i2 이진탐색으로 target - v를 i+1:범위에서 찾기
    
    찾을 수 있으면(i1 + numbers[i2]가 실제로 target이면) return [i1+1, i2+1]

'''
```

<br>

#### <u>코드</u>
```python
from bisect import bisect_left

class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        
        for i1, v1 in enumerate(numbers):
            
            i2 = bisect_left(numbers, target - v1)
            if v1 + numbers[i2] == target:
                return [i1+1, i2+1]
```
<br>

#### <u>디버깅</u>
```python
[0, 0, 1, 3]
0
expected [1, 2] != result [1, 1] -> fix

[0, 1, 1, 4]
2
expected == result
```
<br>

---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
CODE 1(5%) -> CODE 2(65.71%)
### <u>날짜</u> 2022-06-07
#### <u>총 소요시간</u> 10m

<br>

#### <u>코드</u>
```python

class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
    
        dic = {}
        for i, v in enumerate(numbers):
            if v in dic:
                dic[v].append(i)
            else:
                dic[v] = [i]
            
        
        for i, v in enumerate(numbers):
            if target-v in dic:
                # dic[target-v]에 있는 인덱스를 확인하며 i와 겹치지 않는 인덱스를 찾기
                for ni in dic[target-v]:
                    if i != ni:
                        return [i+1, ni+1]
                
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/discuss/51249/Python-different-solutions-(two-pointer-dictionary-binary-search))
```python
# dictionary           
def twoSum2(self, numbers, target):
    dic = {}
    for i, num in enumerate(numbers):
        if target-num in dic:
            return [dic[target-num]+1, i+1]
        dic[num] = i
```

---
---

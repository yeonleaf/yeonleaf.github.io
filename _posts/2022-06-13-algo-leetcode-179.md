---
title: "(179) Largest Number"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, sorting, greedy, practice finished]

toc: true

date: 2022-06-13
last_modified_at: 2022-06-14
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/largest-number/)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-06-13
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
정렬..?
nums에 있는 단어를 string으로 바꾼다.

min(len(nums))에 맞춰서 string의 자리수를 정렬한다.
(가장 짧은 길이가 1이면 index 0까지만 정렬하는 식으로)

같은 앞자리를 가지고 있는 수 중에서 길이가 짧은 원소를 찾아서 길이가 같은 원소 사이에 들어갈 자리를 찾는다.

4 > 3 > 0이므로
34 3 30 
-> 예제의 경우 33430이 됨 (34330이 더 큼)


327 325 115 59 43
5943327325115

while
    count
        1부터 끝까지 비교할 때
            i1, i2 0, 0
            while i1 < len(nums[i-1]) or i2 < len(nums[i])
                nums[i-1][i1] == nums[i][i2]이면
                    i1 += 1
                    i2 += 1
                nums[i-1][i1] < nums[i][i2]이면
                    nums[i-1], nums[i] = nums[i], nums[i-1]
                    count += 1
                    break (swap 성공)
                i1 >= len(nums[i-1]) and i2 < len(nums[i]):
                    i1 = 0

    count가 0이면
        break
325 327 34
34 325 327
'''
```

<br>

#### <u>코드</u>
```python
```
<br>


#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/largest-number/discuss/53298/Python-different-solutions-(bubble-insertion-selection-merge-quick-sorts))
just bubble sort
```python
def largestNumber2(self, nums):
    for i in xrange(len(nums), 0, -1):
        for j in xrange(i-1):
            if not self.compare(nums[j], nums[j+1]):
                nums[j], nums[j+1] = nums[j+1], nums[j]
    return str(int("".join(map(str, nums))))
    
def compare(self, n1, n2):
    return str(n1) + str(n2) > str(n2) + str(n1)
```
compare 함수 기억해 두기
3, 30이 있을 때
303(n1 + n2) vs 330(n2 + n1)을 비교해서 n2 + n1이 더 크면 swap하는 방식

---
---

<br>

---
---
 
## **CODE 2**: 
### <u>날짜</u> 2022-06-14
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
nums를 str로 바꾸기
정렬 (x[0] 기준으로)

버블 정렬

count가 0이면 break

for i in range(1, n):
    nums[i-1][0] == nums[i][0]이면 swap할지 말지를 확인한다.
        check(nums[i-1], nums[i])이 True이면 
            nums[i-1], nums[i] = nums[i], nums[i-1]

def check(n1, n2): (swap해야 하는지 말아야 하는지)
    return int(str(n1) + str(n2)) < int(str(n2) + str(n1))
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def largestNumber(self, nums: List[int]) -> str:
        
        n = len(nums)

        if n == 1:
            return str(nums[0])
        
        def check(n1, n2):
            return int(str(n1) + str(n2)) < int(str(n2) + str(n1))
        
        str_nums = [str(i) for i in nums]
        
        str_nums.sort(reverse = True, key = lambda x: x[0])        
        
        while True:
            count = 0
            
            for i in range(1, n):
                if str_nums[i-1][0] == str_nums[i][0]:
                    if check(str_nums[i-1], str_nums[i]):
                        str_nums[i-1], str_nums[i] = str_nums[i], str_nums[i-1]
                        count += 1
            
            if count == 0:
                break
        
        if str_nums[0] == "0":
            return "0"
        return "".join(str_nums)     
```
<br>

#### <u>디버깅</u>
```python
[332, 333, 335, 34, 3]
expected == result

[3]
expected == result

[0, 0]
expected != result -> fix (line 162~163)
```

---
---

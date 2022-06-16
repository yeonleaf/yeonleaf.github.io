---
title: "(190) Reverse Bits"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, need optimization, bit manipulation, shift operation]

toc: true

date: 2022-06-16
last_modified_at: 2022-06-16
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/reverse-bits/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-16
#### <u>총 소요시간</u> 20m

<br>

#### <u>설계</u>
```python
'''
"10100101000001111010011100"

n을 이진수로 바꾸기
n의 길이를 재고 길이가 32가 되지 않으면 32 - len()만큼 0을 앞에 붙인다.
n을 뒤집는다.
n의 int()값을 반환한다.
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def reverseBits(self, n: int) -> int:

        bn = bin(n)[2:]
        if len(bn) < 32:
            bn = "0"*(32-len(bn)) + bn
        bn = bn[::-1]
        return int(bn, 2)
```
<br>


#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/reverse-bits/discuss/54738/Sharing-my-2ms-Java-Solution-with-Explanation)
bit manipulation (shift연산 사용)
```python
result = 0 (0000_0000_0000_0000_0000_0000_0000_0000)

n = 13 ( 0000_0000_0000_0000_0000_0000_0000_1101)

1. result를 왼쪽으로 한 번 shift연산 한다.
result << 1
2. n & 1로 가장 끝 자리를 얻어낸다. -> last
0000_0000_0000_0000_0000_0000_0000_1101
&
0000_0000_0000_0000_0000_0000_0000_0001
-> 1!
3. result = result + last

이 과정을 계속해서 반복한다.
```

---
---

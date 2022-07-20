---
title: "(201) Bitwise AND of Numbers Range"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, saw discussion]

toc: true

date: 2022-07-20
last_modified_at: 2022-07-20 
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/bitwise-and-of-numbers-range/)

<br>

---
---
 
## **CODE 1**: TLE
### <u>날짜</u> 2022-07-20
#### <u>총 소요시간</u> 15m

<br>

#### <u>설계</u>
```python 
'''
각 자리마다 대응하는 비트가 둘 다 1일 때 1을 반환
0과 비트연산을 하면 무조건 0
비트연산을 하다가 중간에 wise가 0이 뜨면 바로 for문을 탈출 (더 계산할 필요가 없음)
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def rangeBitwiseAnd(self, left: int, right: int) -> int:

        wise = left
        
        for num in range(left+1, right+1):
            wise = wise & num
            if not wise:
                break
        
        return wise
```
<br>

#### <u>디버깅</u>
```python
336
47758
expected == result

300
2147483647
expected == result

8
8
expected == result
```
<br>

---
---


<br>

---
---
 
## **CODE 2**: 시간 초과!
### <u>날짜</u> 2022-07-20
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
2의 제곱수마다 10 100 1000... 의 패턴이 생긴다.
2의 제곱수에 비트연산을 하면 첫 자리 1을 제외한 나머지 자리는 지워지게 된다.
따라서 right보다 작거나 같은 2의 제곱수 중 가장 큰 수를 찾으면 된다.
1에 &연산을 하면 1 아니면 0이 나오게 된다.
left가 1이고 right도 1인 경우에만 1이 나오고 나머지는 0
    
2보다 큰 경우에는 right보다 작거나 같은 2의 제곱수 중 가장 큰 수를 찾는다.
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def rangeBitwiseAnd(self, left: int, right: int) -> int:

        print(bin(left))
        
        if not left:
            return 0
        
        if left == 1:
            if right == 1: return 1
            else: return 0 
        
        # left보다 크지만 가장 작은 2의 제곱수 구하기
        
        wise = 1
        while wise*2 < left:
            wise *= 2
                
        # right보다 작지만 가장 큰 2의 제곱수 구하기
        
        while wise*2 <= right:
            wise*= 2
        
        return wise
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/bitwise-and-of-numbers-range/discuss/56729/Bit-operation-solution(JAVA))
```java
public int rangeBitwiseAnd(int m, int n) {
    int i = 0; // i means we have how many bits are 0 on the right
    while(m != n){
    m >>= 1;
    n >>= 1;
    i++;  
    }  
    return m << i;  
}
```

[Discussion Link](https://leetcode.com/problems/bitwise-and-of-numbers-range/discuss/593317/Simple-3-line-Java-solution-faster-than-100)
```python
while(n>m)
    n = n & n-1;
return n;
```

[Discussion Link](https://leetcode.com/problems/bitwise-and-of-numbers-range/discuss/56721/2-line-Solution(the-fastest)-with-detailed-explanation)

앞쪽부터 가장 긴 common prefix를 찾는다.

```
n > m
m xxx0111111
n xxx1000000

이 상태에서 n과 m을 and연산하면
xxx0000000이 된다.

따라서 우리는 n과 m의 prefix중 가장 긴 값을 구해야 하고
그러기 위해서는 n이 m보다 작아질 때까지 n의 오른쪽부터 1을 삭제해야 한다.

n & (n-1)은 n의 오른쪽 1을 삭제할 수 있는 가장 쉬운 방법이다. (암기)

```

---
---

<br>

#### <b> ✅ 최종 comment </b>
---
title: "(202) Happy Number"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, easy, practice finished]

toc: true

date: 2022-07-20
last_modified_at: 2022-07-20
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/happy-number/)

<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-07-20
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
'''
loop를 언제 끝내냐?
2*2 = 4
4*2 = 16
1*2 + 6*2 = 37

1이 되려면 1이 들어있어야 한다.
제곱해서 1이 되는 수는 1밖에 없기 때문이다.

happy number를 만들고 싶으면
자릿수들의 제곱을 더해서
10 100 1000... 등의 값을 만들어야 한다.

happy number가 아닌 수는 반복이 발생한다.
따라서 같은 수가 다시 나오면 종료하면 된다.
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def isHappy(self, n: int) -> bool:

        s = set()
        
        while n != 1:
            strn = str(n)
            dummy = 0
            
            for num in strn:
                dummy += pow(int(num), 2)
            if n in s:
                return False
            s.add(n)
            n = dummy
        return True
```
<br>

#### <u>디버깅</u>
```python
866
expected == result

1
expected == result

2147483647
expected == result
```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/happy-number/discuss/56917/My-solution-in-C(-O(1)-space-and-no-magic-math-property-involved-))

floyd cycle detection 알고리즘으로 풀 수 있다.
결국 반복되는 사이클을 찾는 문제이기 때문이다.

```cpp
int digitSquareSum(int n) {
    int sum = 0, tmp;
    while (n) {
        tmp = n % 10;
        sum += tmp * tmp;
        n /= 10;
    }
    return sum;
}

bool isHappy(int n) {
    int slow, fast;
    slow = fast = n;
    do {
        slow = digitSquareSum(slow);
        fast = digitSquareSum(fast);
        fast = digitSquareSum(fast);
    } while(slow != fast);
    if (slow == 1) return 1;
    else return 0;
}
```

---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-07-21
#### <u>총 소요시간</u> 20m

<br>

#### <u>설계</u>
```python
'''
floyd cycle detection 알고리즘

slow, fast
slow == fast이면 return False


'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def isHappy(self, n: int) -> bool:
        
        def trans(num):
            strn = str(num)
            dummy = 0
            
            for num in strn:
                dummy += pow(int(num), 2)
            
            return dummy
        
        slow, fast = n, n
        
        while True:
            slow = trans(slow)
            
            fast = trans(trans(fast))
            if slow == 1 or fast == 1:
                return True
            if slow == fast:
                return False
        return True
```
<br>

---
---


#### <b> ✅ 최종 comment </b>
---
title: "(172) Factorial Trailing Zeroes"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, saw discussion]

toc: true

date: 2022-06-07
last_modified_at: 2022-06-07
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/factorial-trailing-zeroes/)

<br>

---
---
 
## **CODE 1**: 1시간 초과
### <u>날짜</u> 2022-06-07
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''
5*4*3*2*1

100!일 경우
1 * 100 -> 0 2개
10의 배수를 만들 수 있는 수를 찾아야 함
2 * 50 -> 0 2개

n < 5이면 return 0


1 ~ n+1까지 딕셔너리에 넣는다.

1부터 i까지
    i+1부터 끝까지의 범위 내에서
    wish 1, 2, 3
    std = pow(10, wish)
    not std % n
        dic에 std // n이 있는지 확인
        res += wish
        break
        
'''
```


#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/factorial-trailing-zeroes/discuss/52373/Simple-CC%2B%2B-Solution-(with-detailed-explaination))
```python

5*2 factor는 100이라서 0의 개수가 2인데 왜 1씩 카운트하는가?

factor 5를 계산한 이후에
5^2 factor에서 5*5중의 하나는 이미 계산이 되어 있음
따라서 5^2 factor의 개수만 세면 됨 (*2할 필요 없음)

이와 비슷한 원리로 5^3 factor, 5*4 factor도 하나씩 계산하게 됨 (이미 이전 단계에서 -1씩을 하기 때문)

5로 몇 번 나눌 수 있는지
5^2로 몇 번 나눌 수 있는지
5^3로 몇 번 나눌 수 있는지...
를 쭉 더하면 된다.
```

---
---

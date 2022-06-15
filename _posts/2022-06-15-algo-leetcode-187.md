---
title: "(187) Repeated DNA Sequences"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, need optimization]

toc: true

date: 2022-06-15
last_modified_at: 2022-06-15
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/repeated-dna-sequences/)
 
<br>

---
---
 
## **CODE 1**: ACCEPTED
### <u>날짜</u> 2022-06-15
#### <u>총 소요시간</u> 45m

<br>

#### <u>설계</u>
```python

'''
하나 이상 등장하는 10-letter-long substring을 리턴하기
슬라이딩 윈도우
10^5 -> O(n^2)는 안 됨

단어 s는 무조건 DNA sequence로 주어짐
따라서 s의 subsequence도 DNA라고 봐야 함

dic {}
RES []

start, end = 0, 10

start < n and end < n
s[start:end]가 dic에 없는 경우 dic에 기록
s[start:end]가 dic에 있는 경우 res에 append
start += 1
end += 1

'''

```

<br>

#### <u>코드</u>
```python
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        dic = {}
        res = set()
        
        n = len(s)
        
        # edge case
        if n <= 10:
            return []
        
        start, end = 0, 10
        while start < n and end <= n:
            if s[start:end] not in dic:
                dic[s[start:end]] = True
            else:
                res.add(s[start:end])
            start += 1
            end += 1
        return list(res)
```
<br>

#### <u>디버깅</u>
```python
"ACGTACGTACGT"
expected == result

"AAAAAACCCCCC"
expected == result

"AAAAAAAAAA"
expected[] != result["AAAAAAAAAA"] -> edge case 수정

"AAAAAAAAAAA"
expected["AAAAAAAAAA"] != result[] -> while문 범위 수정 (end <= n)
```

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/repeated-dna-sequences/discuss/53867/Clean-Java-solution-(hashmap-%2B-bits-manipulation))
hashmap + bit manipulation
```java
00 -> 'A'
01 -> 'C'
10 -> 'G'
11 -> 'T'

char[] map = new char[26];
//map['A' - 'A'] = 0;
map['C' - 'A'] = 1;
map['G' - 'A'] = 2;
map['T' - 'A'] = 3;

1. sequence를 생성한다.
v = 0으로 두고
v << 2 (왼쪽으로 쉬프트 연산) -> v = 00
sequence의 글자 - 'A'를 map에서 찾아온 후 or연산 (둘 중 하나라도 1이면 1)
v |= map[s.charAt(j) - 'A'] -> v |= 01 -> v = 01

v << 2 -> v = 0100 -> map['G'-'A'] = 10 -> v = 0110

2. set을 두 개를 만듬
첫 번째 set에 이미 값이 있는 경우 false를 리턴
두 번째 set에 값이 있는 경우 우리가 이미 해당 sequence를 찾은 적이 있다는 것을 의미 -> output list에 다시 넣지 않는다.
sequence를 첫 번째 set, 두 번째 set에 다 넣었을 때 output list에 넣는다.

첫 번째에 넣지 않고 두 번째에 넣음 -> output list에 sequence를 넣기
첫 번째에 넣지 않고 두 번째에도 넣지 않음 -> 이미 두 번 이상 찾음 -> 아무것도 하지 않는다.

```
```java
public List<String> findRepeatedDnaSequences(String s) {
    Set<Integer> words = new HashSet<>();
    Set<Integer> doubleWords = new HashSet<>();
    List<String> rv = new ArrayList<>();
    char[] map = new char[26];
    //map['A' - 'A'] = 0;
    map['C' - 'A'] = 1;
    map['G' - 'A'] = 2;
    map['T' - 'A'] = 3;

    for(int i = 0; i < s.length() - 9; i++) {
        int v = 0;
        for(int j = i; j < i + 10; j++) {
            v <<= 2;
            v |= map[s.charAt(j) - 'A'];
        }
        if(!words.add(v) && doubleWords.add(v)) {
            rv.add(s.substring(i, i + 10));
        }
    }
    return rv;
}
```
---
---

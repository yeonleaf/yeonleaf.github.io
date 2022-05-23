---
title: "(146) LRU Cache"
excerpt: " "

categories:
    - algorithm
tags:
    - [leetcode, medium, hashmap, linked-list(double), saw discussion]

toc: true

date: 2022-05-23
last_modified_at: 2022-05-23
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/lru-cache/)

<br>

---
---
 
## **CODE 1**: TLE
### <u>날짜</u> 2022-05-23
#### <u>총 소요시간</u>

<br>

#### <u>설계</u>
```python
'''
가장 오래 전에 사용된 키와 교체한다.

고려해야 할 것

우선순위 관리
- get을 호출할 때마다 가장 우선순위가 낮은 key를 O(1) 시간복잡도로 얻을 수 있어야 함
- put이나 get을 호출할 때마다 우선순위 업데이트를 해야 함

업데이트 자체는 해도 되지 않을까? capacity가 3000 -> 3000*3000 9천만 O(n^2)까지는...

dic1 {} (key:value, pri)
dic2 {} (key:pri)
stack deque()

key: value, 

update(key):
    key의 우선순위를 업데이트한다.
    curr = dic_pri[key] (현재 key의 우선순위 인덱스의 위치)
    stack.pop(curr)
    del dict_pri[key]
    curr부터 capacity까지 for문으로 dic_pri에 있는 값을 업데이트 (-1)

put
    dic에 key가 있는 경우 
        dic1[key] = value
        update(key)
    dic에 key가 없는 경우
        stack의 길이 == capacity이면 (꽉 참)
            가장 우선순위가 낮은 키 하나를 제거한다.
            lostkey = stack.pop()
            del dic1[lostkey]
            del dic2[lostkey]
        dic1에 key:value 저장
        stack.append(key)
        dic2[key]:len(stack)-1
get
    dic에 값이 없으면 return -1
    update(key)
    return dic1[key]
    
get도 O(1)이어야 함...

'''

```

#### <u>코드</u>
```python
class LRUCache:
    
    def __init__(self, capacity: int):
        self.dict_val = {}
        self.dict_pri = {}
        self.stack = []
        self.capacity = capacity
    
        
    def update(self, key):

        cur = self.dict_pri[key]
        self.stack.pop(cur)
        
        for i in range(cur, len(self.stack)):
            self.dict_pri[self.stack[i]] -= 1
        
        self.stack.append(key)
        
        self.dict_pri[key] = len(self.stack)-1
    
    
    def get(self, key: int) -> int:
        if key not in self.dict_val:
            return -1
        self.update(key)
        return self.dict_val[key]

    
    def put(self, key: int, value: int) -> None:
        if key in self.dict_val:
            self.dict_val[key] = value
            self.update(key)
        else:  
            self.dict_val[key] = value
            self.stack.append(key)
            self.dict_pri[key] = len(self.stack)-1
            
            if len(self.stack) > self.capacity:
                lostkey = self.stack[0]
                self.stack = self.stack[1:]
                del self.dict_val[lostkey]
                del self.dict_pri[lostkey]
                
                for key in self.stack:
                    self.dict_pri[key] -= 1


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

#### <u>디버깅</u>
```python
## capacity == 1
["LRUCache", "put"]
[[1], [2, 2]]
expected == result

["LRUCache", "put", "put", "get"]
[[1], [2, 2], [3, 3], [2]]
expected == result

["LRUCache", "put", "put", "get"]
[[1], [2, 2], [3, 3], [3]]
expected == result


["LRUCache", "put", "put", "get"]
[[1], [2, 2], [3, 3], [3]]
expected == result


["LRUCache", "put", "put", "get"]
[[1], [2, 2], [3, 3], [3]]
expected == result

["LRUCache", "put", "put", "get"]
[[1], [2, 2], [2, 4], [2]]
expected == result

["LRUCache", "put", "put", "get", "put", "get", "get", "get", "put"]
[[2], [2, 2], [2, 5], [3], [3, 1], [2], [3], [2], [2, 6]]
expected == result


```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/lru-cache/discuss/45911/Java-Hashtable-%2B-Double-linked-list-(with-a-touch-of-pseudo-nodes))

double linked-list + hashmap

---
---

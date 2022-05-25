---
title: "(146) LRU Cache"
excerpt: "linked-list(double) + hashmap"

categories:
    - algorithm
tags:
    - [leetcode, medium, hashmap, linked-list(double), saw discussion]

toc: true

date: 2022-05-23
last_modified_at: 2022-05-25
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


<br>


---
---
 
## **CODE 2**:
### <u>날짜</u> 2022-05-24
#### <u>총 소요시간</u> 25*3 -> 시간 초과

<br>

#### <u>설계</u>
```python
'''
dict {} (key : value)

LRU -> double linked list로 추적

linked = Node()
= head (Node)
= last (Node)

Node
val
next
prev

update (키를 찾아서 맨 뒤로 보내기)
<cur = head에서 시작해서 key가 나올 때까지 while문>
find = cur
cur.prev.next = cur.next
find.next = None
last.next = find
last = last.next

get
key가 dict에 없으면 return -1
update(key)
return dict[key]

put
key가 dict에 있으면
    dict[key] = value
    update(key)
key가 dict에 없으면
    dict[key] = value
    last.next = Node(key)
    last = last.next
    
    if len(dict.values()) > capacity:
        del dict[head.val]
        head = head.next
    
'''
```

#### <u>코드</u>
```python

class Node:
    def __init__(self, val: int):
        self.val = val
        self.prev = None
        self.next = None

class LRUCache:

    def __init__(self, capacity: int):
        linked = None
        self.head = linked
        self.dict_val = {}
        self.capacity = capacity
        
    def update(self, key: int) -> None:

        cur = self.head
        while cur and cur.val != key:
            cur = cur.next
        
        if cur == self.head:
            return 
            
        find = cur
        if cur.prev:
            cur.prev.next = cur.next
        else:
            self.head = self.head.next
        find.prev = self.last
        find.next = None
        self.last.next = find
        self.last = self.last.next
    
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
            # 하나의 노드도 없는 경우
            if not self.head:
                self.dict_val[key] = value
                self.head = Node(key)
                self.last = self.head
            else:
                self.dict_val[key] = value
                new = Node(key)
                new.prev = self.last
                self.last.next = new
                self.last = self.last.next
                if len(self.dict_val.values()) > self.capacity:
                    del self.dict_val[self.head.val]
                    self.head = self.head.next
        
# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)



```

#### <u>디버깅</u>
```python
["LRUCache", "put", "get", "put", "put", "get", "put", "get"]
[[1], [2, 2], [2], [3, 1], [3, 2], [2], [3, 3], [3]]

```
<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/lru-cache/discuss/45911/Java-Hashtable-%2B-Double-linked-list-(with-a-touch-of-pseudo-nodes))

head -- 노드들 -- tail

노드를 넣을 때는 항상 head.next에 넣는다.

노드를 업데이트할 때는 노드를 제거 + 노드 넣기

노드 자체를 넘겨주면 굳이 head에서부터 시작해서 탐색할 필요가 없다.

가장 오래된 노드를 pop할 때는 tail.pre를 제거한다.

이렇게 하는 이유는 null 체크를 번거롭게 하지 않기 위해서다.

```java
import java.util.Hashtable;


public class LRUCache {

class DLinkedNode {
  int key;
  int value;
  DLinkedNode pre;
  DLinkedNode post;
}

/**
 * Always add the new node right after head;
 */
private void addNode(DLinkedNode node) {
    
  node.pre = head;
  node.post = head.post;

  head.post.pre = node;
  head.post = node;
}

/**
 * Remove an existing node from the linked list.
 */
private void removeNode(DLinkedNode node){
  DLinkedNode pre = node.pre;
  DLinkedNode post = node.post;

  pre.post = post;
  post.pre = pre;
}

/**
 * Move certain node in between to the head.
 */
private void moveToHead(DLinkedNode node){
  this.removeNode(node);
  this.addNode(node);
}

// pop the current tail. 
private DLinkedNode popTail(){
  DLinkedNode res = tail.pre;
  this.removeNode(res);
  return res;
}

private Hashtable<Integer, DLinkedNode> 
  cache = new Hashtable<Integer, DLinkedNode>();
private int count;
private int capacity;
private DLinkedNode head, tail;

public LRUCache(int capacity) {
  this.count = 0;
  this.capacity = capacity;

  head = new DLinkedNode();
  head.pre = null;

  tail = new DLinkedNode();
  tail.post = null;

  head.post = tail;
  tail.pre = head;
}

public int get(int key) {

  DLinkedNode node = cache.get(key);
  if(node == null){
    return -1; // should raise exception here.
  }

  // move the accessed node to the head;
  this.moveToHead(node);

  return node.value;
}


public void put(int key, int value) {
  DLinkedNode node = cache.get(key);

  if(node == null){

    DLinkedNode newNode = new DLinkedNode();
    newNode.key = key;
    newNode.value = value;

    this.cache.put(key, newNode);
    this.addNode(newNode);

    ++count;

    if(count > capacity){
      // pop the tail
      DLinkedNode tail = this.popTail();
      this.cache.remove(tail.key);
      --count;
    }
  }else{
    // update the value.
    node.value = value;
    this.moveToHead(node);
  }
}

}
```
---
---


<br>

---
---
 
## **CODE 3**: PRACTICE
### <u>날짜</u> 2022-05-25
#### <u>총 소요시간</u> 1h

<br>

#### <u>설계</u>
```python
'''
dic {} key : node

head(Node), tail(Node)
head.next = tail
tail.prev = head

addNode(node)
    head의 next에 노드를 넣는다.
    
deleteNode(node)
    node.prev.next = node.next
    
updateNode(node)
    deleteNode
    addNode
    
get(key)
    dic에 key가 없으면 return -1
    key가 있으면 
    updateNode(dic[key])
    return dic[key].val

put(key:value)
    dic에 key가 있으면
        dic[key].val = value
        updateNode(dic[key])
    
    dic에 key가 없으면
        new = Node(key, value)
        addNode(new)
        
        count ++ 
        
        count > capacity:
            t = tail.pre
            deleteNode(t)
            del dic[t.key]
        
'''
```

#### <u>코드</u>
```python

class Node:
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None

class LRUCache:


    def __init__(self, capacity: int):
        
        self.capacity = capacity
        
        self.head = Node(-1, -1)
        self.tail = Node(-1, -1)

        self.dic = {}
        self.count = 0
        
        self.head.next = self.tail
        self.tail.prev = self.head

    def addNode(self, node: Node) -> None:
        node.prev = self.head
        node.next = self.head.next
        self.head.next.prev = node
        self.head.next = node
        
    def deleteNode(self, node: Node) -> None:
        pre = node.prev
        post = node.next
        
        pre.next = post
        post.prev = pre
        
    def updateNode(self, node: Node) -> None:
        self.deleteNode(node)
        self.addNode(node)

        
    def get(self, key: int) -> int:
        if key not in self.dic:
            return -1
        self.updateNode(self.dic[key])
        return self.dic[key].val

    def put(self, key: int, value: int) -> None:
        if key in self.dic:
            self.dic[key].val = value
            self.updateNode(self.dic[key])
        else:
            new = Node(key, value)
            self.addNode(new)
            self.dic[key] = new
            self.count += 1
            
            if self.count > self.capacity:
                t = self.tail.prev
                print("[%s]"%t.val)
                self.deleteNode(t)
                del self.dic[t.key]
                self.count -= 1

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)


```
---
---

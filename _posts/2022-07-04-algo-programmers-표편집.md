---
title: "표편집"
excerpt: ""

categories:
    - algorithm
tags:
    - [orogrammers, lv3, need practice]

toc: true

date: 2022-07-04
last_modified_at: 2022-07-04
---

## **문제 링크**
[Question Link](https://programmers.co.kr/learn/courses/30/lessons/81303)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-07-04
#### <u>총 소요시간</u> 29m

<br>

#### <u>설계</u>
```python
'''
행의 삭제 여부를 담을 result
U X -> 현재 선택된 행에서 x칸 위의 행 선택
D X -> 현재 선택된 행에서 X칸 아래의 행 선택
C -> 현재 행 삭제 후 바로 한 칸 아래의 행 선택. 삭제된 행이 가장 마지막 행이면 바로 윗 행 선택
Z -> 최근 삭제된 행을 복구

result [] 행의 삭제 여부를 기록
stack [] 삭제된 행 번호를 담기

U X D X를 수행할 함수 move (i, U/D, X)
cnt = 0
while cnt < X:
    ni = U/D에 따라 i를 옮김
    result[ni]가 O인 경우에만 cnt += 1
    i = ni
return i
    
delete(i):
    result[i] = X
    stack.append(i)
    i가 마지막 행인 경우 d = -1 아니면 d = 1
    while result[i] == "X":
        i += d
    return i

recover():
    result[stack.pop()] = 'O'
    
move, delete는 커서를 바꿈. recover는 바꾸지 않음

1000 -> O(n^2) 정도의 수행은 가능
'''
```

<br>

#### <u>코드</u>
```python
def solution(n, k, cmds):
    
    res = ["O"]*n
    stack = []
    
    def move(i, d, x):
        cnt = 0
        while cnt < x:
            i += d
            if res[i] == "O":
                cnt += 1
        return i
    
    def delete(i):
        res[i] = "X"
        stack.append(i)
        d = -1 if i == n-1 else 1
        while res[i] == "X":
            i += d
        return i
    
    def recover():
        res[stack.pop()] = "O"
    
    ci = k
    for cmd in cmds:
        if len(cmd) == 1:
            if cmd == "Z":
                recover()
            else:
                ci = delete(ci)
        else:
            d, step = cmd.split(" ")
            d = 1 if d == "D" else -1
            ci = move(ci, d, int(step))
            
    return "".join(res)  
```

---
---

<br>

---
---
 
## **CODE 2**:
### <u>날짜</u> 2022-07-04
#### <u>총 소요시간</u> 70m (code1 + code2)

<br>

#### <u>코드</u>
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.prev = None
        self.next = None

def solution(n, k, cmds):
    
    # up
    def up(c, x):
        for _ in range(x):
            c = c.prev
        return c
    
    # down
    def down(c, x):
        for _ in range(x):
            c = c.next
        return c
    
    # delete
    def delete(c):
        stack.append(c)
        prv = c.prev
        nxt = c.next
        prv.next = nxt
        if not nxt:
            return prv
        nxt.prev = prv
        return nxt
    
    # recover
    def recover():
        target = stack.pop()
        target.prev.next = target
        if target.next:
            target.next.prev = target
    
    ## main logic
    # 양방향 연결리스트 만들기
    dummy = Node(-1)
    head = Node(0)
    head.prev = dummy
    dummy.next = head
    
    cur = head
    for i in range(1, n):
        new = Node(i)
        new.prev = cur
        cur.next = new
        cur = cur.next
        
    # 커서 옮기기
    cur = head
    for _ in range(k):
        cur = cur.next
    
    stack = []
    
    for cmd in cmds:
        if len(cmd) == 1:
            if cmd == "Z":
                recover()
            else:
                cur = delete(cur)
        else:
            d, step = cmd.split(" ")
            if d == "U":
                cur = up(cur, int(step))
            else:
                cur = down(cur, int(step))
    
    res = ["X"]*n
    dummy = dummy.next
    while dummy:
        res[dummy.val] = "O"
        dummy = dummy.next
    return "".join(res)
```
<br>

#### <u>디버깅</u>
```python
입력값 〉	1, 0, ["C"]
기댓값 〉	"X"
expected != result
# head 앞에 dummy를 두지 않으면 delete할 때 런타임 에러가 발생함
```

---
---

<br>

#### <b> ✅ 리스트 탐색 방식을 사용하기 전에 linked-list를 사용할 생각을 먼저 해 보자! </b>
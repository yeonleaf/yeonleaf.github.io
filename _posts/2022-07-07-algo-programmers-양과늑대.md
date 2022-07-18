---
title: "양과 늑대"
excerpt: ""

categories:
    - algorithm
tags:
    - [programmers, lv3, saw discussion]

toc: true

date: 2022-07-07
last_modified_at: 2022-07-08
---

## **문제 링크**
[Question Link](https://school.programmers.co.kr/learn/courses/30/lessons/92343)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
# 완전탐색인듯? info의 길이가 17로 제한되어 있다는 점에서..아래 레벨에 양이 있을지 늑대가 있을지 알 수 없다는 점에서 greedy하게 풀 수 있는 문제도 아니다.
# 문제는 이게 tree가 아니고 그래프여서 다시 루트 노드로 돌아올 수 있다는 점이다...
# 해당 노드의 양/늑대를 모은 상태인지 모으지 않은 상태인지 기록하는 배열이 필요
# 만약 이미 해당 노드의 양/늑대를 모았다면 다시 방문해도 양/늑대를 다시 모으지 않는다.
# collect = [0]*n
# res = 1 (항상 루트 노드에는 양이 있기 때문)
# dfs(node, sheep, wolf)
    # sheep < wolf이면 return
    # res = max(res, sheep)
    # node와 연결된 노드를 순회한다. (nxt)
    # nxt를 방문한 적이 있다면 info[nxt]를 확인해서 sheep, wolf를 업데이트
    # nxt를 방문한 적이 없다면 sheep, wolf를 업데이트하지 않고 단순 방문
# 연결 리스트 만들기 (어차피 모든 노드를 차례대로 방문하는 형식이기 때문에 연결 리스트가 더 잘 맞음)

# 무한 반복을 줄이는 방법..
# 현재 노드에서 다음 노드로 이동할 때 sheep이 wolf보다 많은 상태일 때만 이동하게 하기 -> 소용 없음

```

<br>

#### <u>코드</u>
```python
def solution(info, edges):

    n = len(info)
    adj = [[] for _ in range(n)]
    
    for n1, n2 in edges:
        adj[n1].append(n2)
        adj[n2].append(n1)
    
    res = 1
    
    info[0] = -1
    
    def dfs(node, sheep, wolf):
        nonlocal res, n, info
        if sum(info) == -n:
            return 
        res = max(res, sheep)
        old = info[:]
        for nxt in adj[node]:
            if info[nxt] == -1:
                dfs(nxt, sheep, wolf)
            else:
                if sheep > wolf+1:
                    info[nxt] = -1
                    dfs(nxt, sheep, wolf+1)
                    info = old[:]
                else:
                    info[nxt] = -1
                    dfs(nxt, sheep+1, wolf)
                    info = old[:]
    
    dfs(0, 1, 0)
    
    return res
```

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://school.programmers.co.kr/questions/25736)
```python
'''
양방향 그래프를 사용하면 안 된다.
단방향 그래프를 기본적으로 사용하고
부모 노드를 방문한 후 
방문할 수 있는 노드 리스트에 부모 노드를 제거
부모 노드의 자식 노드를 추가
리스트를 사용할 시 깊은 복사로
'''
```

---
---

<br>

---
---
 
## **CODE 2**: 시간 초과!
### <u>날짜</u> 2022-07-08
#### <u>총 소요시간</u> 

<br>

#### <u>설계</u>
```python
# able에서 부모 노드를 꺼낸다.
# 부모 노드가 늑대이면 sheep < wolf+1인지 확인 만약 그렇다면 res = max(res, sheep), return
# 부모 노드의 직계 자식들을 꺼내서 able에 넣는다.
# 다음 턴으로 넘어간다.
```

<br>

#### <u>코드</u>
```python
def solution(info, edges):

    n = len(info)
    adj = [[] for _ in range(n)]
    
    for n1, n2 in edges:
        adj[n1].append(n2)    
    
    print(adj)
    res = 0
    
    def dfs(able, sheep, wolf):
        nonlocal res

        if sheep < wolf:
            return 
        
        while able:
            node = able.pop()
        
            nsheep, nwolf = sheep, wolf
            
            if info[node]:
                nwolf += 1
            else:
                nsheep += 1
            
            if nsheep < nwolf:
                return 
            res = max(res, nsheep)

            dfs(able+adj[node], nsheep, nwolf)

                    
    dfs([0], 0, 0)
    return res
```
<br>

#### <u>디버깅</u>
```python
[0, 1], [[0, 1]]
expected == result

[0, 1, 1, 0, 0, 0, 1, 0, 0], [[0, 1], [0, 2], [1, 3], [1, 4], [2, 5], [2, 6], [6, 7], [6, 8]]
expected != result
```

---
---


<br>

#### <b> ✅ 최종 comment </b>
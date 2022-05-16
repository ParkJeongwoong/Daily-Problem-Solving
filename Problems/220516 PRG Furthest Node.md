# 220515 PRG Furthest Node

링크 : https://programmers.co.kr/learn/courses/30/lessons/49189

제목 : 가장 먼 노드

유형 : 그래프

---

```python
from collections import deque

def solution(n, edge):
    answer = 0
    nodes = [[] for _ in range(n)]
    for e in edge:
        nodes[e[0]-1].append(e[1]-1)
        nodes[e[1]-1].append(e[0]-1)
    visited = [False]*n
    max_distance = 0
    queue = deque([[0, 0]])
    while queue:
        node, distance = queue.popleft()
        if visited[node]:
            continue
        visited[node] = True
        if distance == max_distance:
            answer += 1
        else:
            max_distance += 1
            answer = 1
        for next_node in nodes[node]:
            queue.append([next_node, distance+1])
    return answer
```


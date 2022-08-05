# 220805 BOJ 11725 Find Parents

링크 : https://www.acmicpc.net/problem/11725

제목 : 트리의 부모 찾기

유형 : DFS

---

```python
import sys
input = sys.stdin.readline

def main():
    N = int(input())
    tree = [[] for _ in range(N+1)]
    for _ in range(N-1):
        a, b = map(int, input().split())
        tree[a].append(b)
        tree[b].append(a)
    parents = [1]*(N+1)
    parents[0] = -1
    parents[1] = 1

    visited = [False] * (N+1)
    stack = [1]

    while stack:
        node = stack.pop()
        if visited[node]:
            continue
        visited[node] = True

        for next_node in tree[node]:
            if not visited[next_node]:
                stack.append(next_node)
                parents[next_node] = node
    
    for i in range(2,N+1):
        print(parents[i])

        

if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`284ms` `Python 3`

- 문제의 이름은 Tree지만 DFS로 풀었다
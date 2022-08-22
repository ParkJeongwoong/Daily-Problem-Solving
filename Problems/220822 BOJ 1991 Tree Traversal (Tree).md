# 220822 BOJ 1991 Tree Traversal

링크 : https://www.acmicpc.net/problem/1991

제목 : 트리 순회

유형 : Tree

---

```python
import sys
input = sys.stdin.readline
from collections import deque

def main():
    def type1():
        print(alphabet(0), end="")
        nodes = [tree_list[0][2], tree_list[0][1]]
        while nodes:
            node = nodes.pop()
            if not node:
                continue
            print(alphabet(node), end="")
            nodes.append(tree_list[node][2])
            nodes.append(tree_list[node][1])
        print()

    def type2():
        nodes = deque([0])
        while nodes:
            node = nodes.popleft()
            if visited[node] or (type(node) == bool and not node):
                continue
            if nodeCheck2(node):
                print(alphabet(node), end="")
                visited[node] = True
            if not visited[tree_list[node][2]]:
                nodes.appendleft(tree_list[node][2])
            if not visited[node]:
                nodes.appendleft(node)
            if not visited[tree_list[node][1]]:
                nodes.appendleft(tree_list[node][1])
        print()

    def type3():
        nodes = deque([0])
        while nodes:
            node = nodes.popleft()
            if visited[node] or (type(node) == bool and not node):
                continue
            if nodeCheck3(node):
                print(alphabet(node), end="")
                visited[node] = True
            if not visited[node]:
                nodes.appendleft(node)
            if not visited[tree_list[node][2]]:
                nodes.appendleft(tree_list[node][2])
            if not visited[tree_list[node][1]]:
                nodes.appendleft(tree_list[node][1])
        print()

    def nodeCheck2(node):
        res = False
        if not tree_list[node][1] or visited[tree_list[node][1]]:
            res = True
        return res

    def nodeCheck3(node):
        res = False
        if not tree_list[node][1] or visited[tree_list[node][1]]:
            if not tree_list[node][2] or visited[tree_list[node][2]]:
                res = True
        return res

    N = int(input())
    tree_list = [[False, False, False] for _ in range(N)]
    for _ in range(N):
        a, b, c = input().split()
        if b != '.':
            tree_list[index(a)][1] = index(b)
            tree_list[index(b)][0] = index(a)
        if c != '.':
            tree_list[index(a)][2] = index(c)
            tree_list[index(c)][0] = index(a)
    
    type1()
    visited = [False]*N
    type2()
    visited = [False]*N
    type3()

def index(a):
    return ord(a)-65
def alphabet(i):
    return chr(i+65)
        

if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`92ms` `Python 3`



전위순회, 중위순회, 후위순회

- 재귀를 쓰면 쉽지만 개인적으로 재귀를 선호하지 않는다.
# 220801 BOJ 2644 Calculate Relation

링크 : https://www.acmicpc.net/problem/2644

제목 : 촌수 계산

유형 : Graph

---

```python
import sys
input = sys.stdin.readline

def main():

    def dfs(A, B, N):
        stack = [(A,0)]

        while True:
            a, level = stack.pop()

            if a == B:
                return level

            level += 1
            
            for i in range(N):
                relations[i][a] = 0
                if relations[a][i]:
                    stack.append((i,level))            

            if not stack:
                return -1
    
    # Run
    N = int(input())
    A, B = map(int, input().split())
    M = int(input())

    relations = [[0]*N for _ in range(N)]
    for _ in range(M):
        a, b = map(int, input().split())
        relations[a-1][b-1] = 1
        relations[b-1][a-1] = 1

    print(dfs(A-1,B-1,N))



if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`76ms` `Python 3`
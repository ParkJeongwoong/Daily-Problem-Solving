# 220721 BOJ 2468 Safe Area

링크 : https://www.acmicpc.net/problem/2468

제목 : 안전 영역

유형 : Brute Force, Graph

---

```python
import sys
input = sys.stdin.readline

def main():

    def dfs(i,j, level):
        if isSunken(i,j,level) or visited[i][j]:
            return False

        stack = [(i,j)]

        while stack:
            y, x = stack.pop()

            if visited[y][x]:
                continue
            visited[y][x] = True
            if isSunken(y,x,level):
                continue

            for d in range(4):
                ny = y + dy[d]
                nx = x + dx[d]
                if 0<=ny and ny<N and 0<=nx and nx<N and not visited[ny][nx]:
                    stack.append((ny,nx))

        return True
        
    def isSunken(i,j,level):
        if area[i][j] < level:
            return True
    
    # Run
    dy = [0,-1,0,1]
    dx = [1,0,-1,0]
    N = int(input())
    area = []
    minHeight = 100
    maxHeight = 1
    answer = 0

    for _ in range(N):
        tempArea = list(map(int, input().split()))
        minHeight = min(minHeight, min(tempArea))
        maxHeight = max(maxHeight, max(tempArea))
        area.append(tempArea)

    for level in range(minHeight-1, maxHeight+1):
        visited = [[False]*N for _ in range(N)]
        tempAnswer = 0
        for i in range(N):
            for j in range(N):
                tempAnswer += dfs(i,j, level)
        answer = max(answer, tempAnswer)

    print(answer)



if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`1552ms` `Python 3`

- 처음에 level의 범위를 `range(minHeight-1, maxHeight)까지로 했다가 틀렸다 (수위가 maxHeigt까지는 차야하는데 maxHeight-1에서 끝나니까 maxHeight-1 높이는 잠기지 않는 것으로 여겨졌다)
- 이를 발견 못하고 range를 1~100으로 잡으니 통과하는 걸 보고 level의 범위를 수정해서 해결
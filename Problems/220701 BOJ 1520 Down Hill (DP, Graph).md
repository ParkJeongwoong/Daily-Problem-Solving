# 220701 BOJ 1520 Down Hill

링크 : https://www.acmicpc.net/problem/1520

제목 : 내리막길

유형 : DP, Graph

---

## DFS

```python
import sys
input = sys.stdin.readline
sys.setrecursionlimit(10**6)

def main():
    dx = [1, -1, 0, 0]
    dy = [0, 0, 1, -1]

    def dfs(x, y):
        if x == m-1 and y == n-1:
            return 1
        if dp[x][y] != -1:
            return dp[x][y]
        dp[x][y] = 0
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0 <= nx < m and 0 <= ny < n:
                if board[nx][ny] < board[x][y]:
                    dp[x][y] += dfs(nx, ny)
        return dp[x][y]

    m, n = map(int, input().split())
    board = [list(map(int, input().split())) for _ in range(m)]
    dp = [[-1]*n for _ in range(m)]
    print(dfs(0, 0))

if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`176ms` `Python 3`

- DFS를 쓰면 재귀함수를 사용해야 한다.
  - 그래서 Recursion Error를 막기 위해 `setrecursionlimit`를 사용해야 한다.
  - 마지막 종점부터 값을 Return해서 역으로 그래프를 채워야 하기 때문
  - 미방문 상태(-1)가 아니라면 DFS로 값을 가져오고 방문 상태라면 dp 값을 가져와서 더하는 방식
    - 특정 위치(x, y)에서 도착지까지 갈 수 있는 경우의 수 = 다음 위치들의 경우의 수의 합

## BFS

```python
import sys
import heapq
input = sys.stdin.readline

def main():
    dx, dy = [-1, 0, 1, 0], [0, 1, 0, -1]

    def bfs(x, y):
        heap = [(-board[x][y], x, y)]
        dp = [[0] * M for _ in range(N)]
        dp[x][y] = 1

        while heap:
            cnt, cx, cy = heapq.heappop(heap)

            for i in range(4):
                nx, ny = cx + dx[i], cy + dy[i]

                if not 0 <= nx < N or not 0 <= ny < M:
                    continue
                if board[nx][ny] >= board[cx][cy]:
                    continue

                if dp[nx][ny] == 0:
                    heapq.heappush(heap, (-board[nx][ny], nx, ny))
                dp[nx][ny] += dp[cx][cy]

        return dp


    N, M = map(int, input().split())
    board = [list(map(int, input().split())) for _ in range(N)]

    print(bfs(0, 0)[N - 1][M - 1])

if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`160ms` `Python 3`

- BFS를 쓰면 Heap을 사용해야 한다.
  - 파이썬의 heapq는 최소힙이므로 board 값을 음수로 만들어 가장 높은 곳부터 방문하도록 변경
  - Heap을 사용하지 않으면 이미 방문한 길을 나중에 다시 방문하는 경우가 생길 수 있음
    - 재방문하는 위치의 DP값으로는 도착지까지의 경우의 수를 완전히 파악할 수 없음
      - 재방문 지점 이후에 분기가 생기거나, 다른 경로에서 다시 재방문이 발생할 수 있기 때문
      - 즉 애초에 동일한 위치에 재방문이 일어나면 안 됨
    - Heap을 사용하면 이런 문제 없이 재방문 없이 방문 가능한 가장 높은 곳들부터 순서대로 탐색 가능
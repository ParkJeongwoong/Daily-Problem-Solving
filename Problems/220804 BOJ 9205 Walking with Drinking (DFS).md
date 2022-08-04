# 220804 BOJ 9205 Walking with Drinking

링크 : https://www.acmicpc.net/problem/1182

제목 : 맥주 마시면서 걸어가기

유형 : DFS

---

```python
import sys
input = sys.stdin.readline

def main():
    def positive(num):
        if num < 0:
            return -num
        return num

    def manhattan(a,b):
        return positive(a[0]-b[0]) + positive(a[1]-b[1])

    def drinkAndGo(distance):
        beerDrink = distance // 50
        if distance % 50:
            beerDrink += 1
        beerLeft = 20 - beerDrink
        if beerLeft<0:
            return False
        return True

    # Run
    t = int(input())
    for _ in range(t):
        n = int(input())
        graph = [list(map(int,input().split())) for _ in range(n+2)]
        visited = [False]*(n+2)
        stack = [0]
        while stack:
            node = stack.pop()
            if visited[node]:
                continue
            elif node == n+1:
                print("happy")
                break
            visited[node] = True

            for next_node in range(n+2):
                if visited[next_node]:
                    continue
                if drinkAndGo(manhattan(graph[node], graph[next_node])):
                    stack.append(next_node)
        else:
            print("sad")

        

if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`88ms` `Python 3`
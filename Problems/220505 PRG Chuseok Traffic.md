# 220505 PRG Chuseok Traffic

링크 : https://programmers.co.kr/learn/courses/30/lessons/17676

제목 : 추석 트래픽

유형 : Greedy

---

```python
import sys
input = sys.stdin.readline


def main():
    move = [(0,1), (1,1), (1,0), (1,-1), (0,-1), (-1,-1), (-1,0), (-1,1)]

    def dfs(i,j):
        pos = [(i,j)]
        while pos:
                x,y = pos.pop()
                if not geo[y][x]:
                    continue
                geo[y][x] = 0

                for xd, yd in move:
                    if x+xd<0 or y+yd<0 or x+xd>=w or y+yd>=h:
                        continue
                    if not geo[y+yd][x+xd]:
                        continue
                    pos.append((x+xd, y+yd))
                    
    while True:
        w, h = map(int, input().split())
        if w == 0 and h == 0:
            break
        geo = [list(map(int, input().split())) for _ in range(h)]
        island = 0

        for i in range(w):
            for j in range(h):
                if not geo[j][i]:
                    continue
                island += 1
                dfs(i,j)
        print(island)
        

if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```



## 다른 사람의 풀이

```python
def solution(lines):

    #get input
    S , E= [], [] 
    totalLines = 0 
    for line in lines:
        totalLines += 1
        type(line)
        (d,s,t) = line.split(" ")

       ##time to float
        t = float(t[0:-1])
        (hh, mm, ss) = s.split(":")
        seconds = float(hh) * 3600 + float(mm) * 60 + float(ss)

        E.append(seconds + 1)
        S.append(seconds - t + 0.001)

    #count the maxTraffic
    S.sort()

    curTraffic = 0
    maxTraffic = 0
    countE = 0
    countS = 0
    while((countE < totalLines) & (countS < totalLines)):
        if(S[countS] < E[countE]):
            curTraffic += 1
            maxTraffic = max(maxTraffic, curTraffic)
            countS += 1
        else: ## it means that a line is over.
            curTraffic -= 1
            countE += 1

    return maxTraffic
```


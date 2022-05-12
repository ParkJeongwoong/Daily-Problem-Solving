# 220512 PRG Rank

링크 : https://programmers.co.kr/learn/courses/30/lessons/49191

제목 : 순위

유형 : Graph

---

```python
def solution(n, results):
    def DFS(w_l, root, node):
        if w_l == 'w': # node가 이길 사람들
            for i in range(n):
                if winTable[node][i] and not winTable[root][i]:
                    winTable[root][i] = 1
                    DFS('w', root, i)
        else:
            for i in range(n):
                if loseTable[node][i] and not loseTable[root][i]:
                    loseTable[root][i] = 1
                    DFS('l', root, i)
        
    answer = 0
    winTable = [[0]*n for _ in range(n)] # 내가 이긴 사람들
    loseTable = [[0]*n for _ in range(n)] # 내가 진 사람들
    stack = []
    
    for result in results:
        winner = result[0]-1
        loser = result[1]-1
        winTable[winner][loser] = 1
        loseTable[loser][winner] = 1
        
    for i in range(n):
        for j in range(n):
            if winTable[i][j]:
                DFS('w',i,j)
            elif loseTable[i][j]:
                DFS('l',i,j)
    
    for i in range(n):
        if sum(winTable[i])+sum(loseTable[i]) == n-1:
            answer += 1
                
    return answer
```


# 220908 PRG 42628 Double Priority Queue

링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42628

제목 : 이중우선순위큐

유형 : Heap

---

```python
import heapq

def solution(operations):
    answer = []
    maxheap = []
    minheap = []
    cnt = 0
    
    for operation in operations:
        op, op_id = operation.split()
        if op == "I":
            heapq.heappush(maxheap, -int(op_id))
            heapq.heappush(minheap, int(op_id))
            cnt += 1
        elif op == "D" and op_id == "1":
            if cnt > 0:
                heapq.heappop(maxheap)
                cnt -= 1
        elif op == "D" and op_id == "-1":
            if cnt > 0:
                heapq.heappop(minheap)
                cnt -= 1
        
        if cnt == 0:
            maxheap = []
            minheap = []
    
    if cnt == 0:
        answer.extend([0,0])
    else:
        answer.extend([-heapq.heappop(maxheap),heapq.heappop(minheap)])
    
    return answer
```

- 마지막에 cnt == 0 일 때의 조건을 두지 않으면 예외가 생긴다.
  
  - 입력 : ["I 4", "I 3", "I 2", "I 1", "D 1", "D 1", "D -1", "D -1", "I 5", "I 6"]
  
  - 정답 : [6, 5]
  
  - 예외 : [6, 3] # 4와 3을 maxheap에서 빼서 minheap에는 남아있는 문제 발생
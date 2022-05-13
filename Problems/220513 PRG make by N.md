# 220513 PRG make by N

링크 : https://programmers.co.kr/learn/courses/30/lessons/42895

제목 : N으로 표현

유형 : DP

---

```python
def solution(N, number):
    dp = [None,
          [N],
          [N*10+N],
          [N*100+N*10+N],
          [N*1000+N*100+N*10+N],
          [N*10000+N*1000+N*100+N*10+N],
          [],
          [],
          [],[]]
    
    for i in range(1,9):
        numList = dp[i]
        for num in numList:
            if num == number:
                return i
            for j in range(1,min(i+1,9-i)):
                jnumList = dp[j]
                for jnum in jnumList:
                    if num+jnum > 0:
                        dp[i+j].append(num+jnum)
                    if num*jnum > 0:
                        dp[i+j].append(num*jnum)
                    if num-jnum > 0:
                        dp[i+j].append(num-jnum)
                    if num//jnum > 0:
                        dp[i+j].append(num//jnum)
                    if jnum-num > 0:
                        dp[i+j].append(jnum-num)
                    if jnum//num > 0:
                        dp[i+j].append(jnum//num)
                    
    return -1
```

- BFS로 처음에 시도하다가 실패
  - node에서 N만큼 사칙연산한 값들을 다음 node로 잡았는데, 이러면 *(N+N) 같은 경우를 찾아낼 수 없다 

- DP로 바꾼 뒤 헤맸는데 빼기, 나누기 연산에서 두 변수의 위치를 바꾸는 경우를 생각하지 않았기 때문이었다

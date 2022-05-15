# 220515 PRG Immigration

링크 : https://programmers.co.kr/learn/courses/30/lessons/43238

제목 : 입국심사

유형 : 이분탐색

---

```python
def solution(n, times):
    min_time = 1
    max_time = max(times)*n
    while min_time < max_time:
        mid = (max_time+min_time)//2
        finished = 0
        for time in times:
            finished += mid // time
        if finished < n:
            min_time = mid+1
        else:
            max_time = mid
    return min_time
```

- Command & Conquert로 시도하다가 재귀가 너무 깊어 실패
- 이분탐색으로 시간에 대해 쪼개면서 실행 (시간은 정렬되어 있기 때문에 가능)
  - n명에 대해서 매번 최적의 라인을 C&C로 탐색하는 것보다
  - 이분탐색으로 가능한 모든 시간에 대해서 몫을 더하는 게 더 이득

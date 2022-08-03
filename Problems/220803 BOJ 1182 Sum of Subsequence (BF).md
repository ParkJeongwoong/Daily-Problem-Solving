# 220803 BOJ 1182 Sum of Subsequence

링크 : https://www.acmicpc.net/problem/1182

제목 : 부분 수열의 합

유형 : BF

---

```python
import sys
input = sys.stdin.readline

def main():
    # Run
    N, S = map(int, input().split())
    numbers = list(map(int, input().split()))
    answer = 0

    standard = 2**(N) -1
    for i in range(1,standard+1):
        number_i = 1
        tmp_sum = 0
        while i:
            j = i % 2
            if j:
                tmp_sum += numbers[N-number_i]
            number_i += 1
            i //= 2
        if tmp_sum == S:
            answer += 1
    
    print(answer)

if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`2716ms` `Python 3`

- 비트 마스킹을 이용해서 N개의 수를 선택하는 경우의 수를 나누었다.
  
  - 3가지 수의 경우 001, 010, 011, 100, 101, 110, 111로 선택하는 경우의 수가 나뉘고 이는 1 ~ 2^N -1의 이진법으로 표현 가능
  
  - 
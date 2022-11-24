# 221124 PRG 132266 (BFS)

링크 : https://www.acmicpc.net/problem/12891

제목 : DNA 비밀번호

유형 : Sliding Window

---

```python
import sys
input = sys.stdin.readline
from collections import deque

def main():
    def DNAcheck(flags):
        if flags[0] and flags[1] and flags[2] and flags[3]:
            return True

    answer = 0
    S, P = map(int, input().split())
    DNAstring = input().rstrip()
    ACGT = list(map(int, input().split()))
    DNAmap = {"A":0, "C":1, "G":2, "T":3}

    s = 0
    e = P
    DNAtemp = [0,0,0,0]
    for i in range(s,e):
        dna = DNAstring[i]
        DNAtemp[DNAmap[dna]] += 1

    flags = [False, False, False, False]
    flags[0] = DNAtemp[0] >= ACGT[0]
    flags[1] = DNAtemp[1] >= ACGT[1]
    flags[2] = DNAtemp[2] >= ACGT[2]
    flags[3] = DNAtemp[3] >= ACGT[3]

    if DNAcheck(flags):
        answer += 1
    s += 1
    e += 1

    while e <= S:
        sDNA = DNAstring[s-1]
        eDNA = DNAstring[e-1]
        DNAtemp[DNAmap[sDNA]] -= 1
        DNAtemp[DNAmap[eDNA]] += 1

        flags[DNAmap[sDNA]] = DNAtemp[DNAmap[sDNA]] >= ACGT[DNAmap[sDNA]]
        flags[DNAmap[eDNA]] = DNAtemp[DNAmap[eDNA]] >= ACGT[DNAmap[eDNA]]        

        if DNAcheck(flags):
            answer += 1

        s += 1
        e += 1

    print(answer)



if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`612ms` `Python3`
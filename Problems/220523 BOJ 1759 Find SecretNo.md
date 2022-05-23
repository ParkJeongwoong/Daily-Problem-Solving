# 220523 BOJ 1759 Find SecretNo

링크 : https://www.acmicpc.net/problem/1759

제목 : 암호 만들기

유형 : 백트래킹

---

```python
import sys
input = sys.stdin.readline


def main():
    def print_res():
        print(''.join(res))
    def next_step(idx, vCount):
            # check, vCount = check_res(idx, vCount)
            # if not check:
            #     return
            res.append(candidates[idx])
            backtracking(idx+1,vCount)
            res.pop()
    def check_res(idx, vCount):
        check = True
        if candidates[idx] in 'aeiou':
            vCount += 1
        if idx >= vowels and vCount == 0:
            check = False
        if L - vCount < 2:
            check = False

        return check, vCount
    def backtracking(start, vCount):
        if len(res) == L:
            v = 0
            s = 0
            for r in res:
                if r in 'aeiou':
                    v += 1
                else:
                    s += 1
            if v < 1 or s < 2:
                return
            return print_res()
        for i in range(start,C):
            next_step(i,vCount)

    res = []
    vowels = -1

    L, C = map(int, input().split())
    candidates = list(input().split())
    candidates.sort()
    for i in range(C):
        if candidates[i] in 'aeiou':
            vowels = i

    backtracking(0,0)

        

if __name__ == "__main__":
    I = sys.stdin.readline
    main()
```

`80ms` `Python 3`

- check_res 함수가 동작하지 않아 임시로 만든 코드

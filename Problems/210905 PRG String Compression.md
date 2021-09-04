# 210905 PRG String Compression

링크 : https://programmers.co.kr/learn/courses/30/lessons/60057

제목 : 프로그래머스 문자열 압축

유형 : String

---

```python
def solution(s):
    answer = len(s)
    num = 1
    max_num = len(s)//2
    
    while num <= max_num:
        curr_word = s[:num]
        curr_compressed = 1
        curr_answer = len(s)
        
        compressed = [] # 압축시킨 정도
        from_idx = num
        to_idx = 2*num
        while to_idx <= len(s):
            if s[from_idx:to_idx] == curr_word:
                curr_compressed += 1
                curr_answer -= num
            else:
                if curr_compressed > 1:
                    compressed.append(str(curr_compressed))
                curr_compressed = 1
                curr_word = s[from_idx:to_idx]
            from_idx += num
            to_idx += num
        else:
            if curr_compressed > 1:
                compressed.append(str(curr_compressed))
        
        for compressed_el in compressed:
            curr_answer += len(compressed_el)
        answer = min(answer, curr_answer)
        num += 1
    
    return answer
```


# 220511 PRG Open Chat

링크 : https://programmers.co.kr/learn/courses/30/lessons/42888

제목 : 오픈채팅방

유형 : Greedy

---

```python
def in_msg(nickname):
    return nickname + "님이 들어왔습니다."
def out_msg(nickname):
    return nickname + "님이 나갔습니다."

def solution(records):
    def check_action(data):
        action = data[0]
        usr_id = data[1]
        if action == "Enter":
            nickname = data[2]
            pre_answer.append((action, usr_id))
            return nickname
        elif action == "Leave":
            pre_answer.append((action, usr_id))
        elif action == "Change":
            nickname = data[2]
            return nickname
    def msg_mkr(msg):
        action = msg[0]
        usr = msg[1]
        if action == "Enter":
            return in_msg(usr_nickname[usr])
        if action == "Leave":
            return out_msg(usr_nickname[usr])
        
    pre_answer = []
    answer = []
    usr_nickname = dict()
    for record in records:
        parsed = record.split()
        nickname = check_action(parsed)
        if nickname:
            usr_nickname.update({parsed[1]: nickname})
    
    for msg in pre_answer:
        answer.append(msg_mkr(msg))
        
    return answer
```



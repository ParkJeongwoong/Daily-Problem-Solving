# 210821 PRG SQL GROUP BY

링크 : https://programmers.co.kr/learn/courses/30/parts/17044

제목 : 프로그래머스 SQL GROUP BY

유형 : SQL

`Oracle`

---

## 1

```sql
SELECT ANIMAL_TYPE, COUNT(ANIMAL_TYPE) count FROM ANIMAL_INS GROUP BY ANIMAL_TYPE ORDER BY ANIMAL_TYPE;
```



## 2

```sql
SELECT * FROM (SELECT NAME, COUNT(NAME) COUNT FROM ANIMAL_INS GROUP BY NAME ORDER BY NAME) WHERE COUNT>1;
```



## 3

```sql
SELECT HOUR, COUNT(TIME) COUNT
FROM (SELECT LEVEL+8 AS HOUR FROM DUAL CONNECT BY LEVEL < 12) H,
    (SELECT TO_CHAR(DATETIME,'HH24') AS TIME FROM ANIMAL_OUTS) AO
WHERE HOUR=TIME
GROUP BY HOUR
ORDER BY HOUR;
```



## 4

```sql
SELECT HOUR, COUNT(TIME) COUNT
FROM (SELECT LEVEL-1 AS HOUR FROM DUAL CONNECT BY LEVEL < 25) H,
    (SELECT TO_CHAR(DATETIME,'HH24') AS TIME FROM ANIMAL_OUTS) AO
WHERE HOUR=TIME(+)
GROUP BY HOUR
ORDER BY HOUR;
```


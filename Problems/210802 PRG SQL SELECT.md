# 210802 PRG SQL SELECT

링크 : https://programmers.co.kr/learn/courses/30/parts/17042

제목 : 프로그래머스 SQL SELECT

유형 : SQL

---

## 1

```mysql
SELECT * FROM ANIMAL_INS
```



## 2

```mysql
SELECT NAME, DATETIME FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC
```



## 3

```mysql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'Sick'
ORDER BY ANIMAL_ID
```



## 4

```mysql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE INTAKE_CONDITION != 'Aged'
ORDER BY ANIMAL_ID
```



## 5

```mysql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```



## 6

```mysql
SELECT ANIMAL_ID, NAME, DATETIME FROM ANIMAL_INS
ORDER BY NAME ASC, DATETIME DESC
```



## 7

```mysql
SELECT NAME FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 1
```


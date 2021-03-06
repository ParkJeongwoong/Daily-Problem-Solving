# 210915 PRG SQL String, Date

링크 : https://programmers.co.kr/learn/courses/30/parts/17047

제목 : 프로그래머스 SQL String, Date

유형 : SQL

`MySQL`

---

## 1

```sql
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE FROM ANIMAL_INS
WHERE NAME  IN ('Lucy', 'Ella', 'Pickle', 'Rogan', 'Sabrina', 'Mitty')
ORDER BY ANIMAL_ID
```



## 2

```sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE ANIMAL_TYPE = 'Dog'
    AND NAME LIKE '%EL%'
ORDER BY NAME
```



## 3

```sql
SELECT ANIMAL_ID, NAME,
    CASE WHEN  SEX_UPON_INTAKE LIKE 'Neutered%' THEN 'O'
        WHEN  SEX_UPON_INTAKE LIKE 'Spayed%' THEN 'O'
        ELSE 'X'
    END AS 중성화
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```



## 4

```sql
SELECT AI.ANIMAL_ID, AI.NAME
FROM ANIMAL_INS AI, ANIMAL_OUTS AO
WHERE AI.ANIMAL_ID = AO.ANIMAL_ID
ORDER BY AI.DATETIME - AO.DATETIME
LIMIT 2
```



## 5

```sql
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, '%Y-%m-%d') AS '날짜'
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```


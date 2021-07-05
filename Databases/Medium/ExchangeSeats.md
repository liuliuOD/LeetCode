## [Exchange Seats](https://leetcode.com/problems/exchange-seats)

### Solution :

Method 1 :
```sql
SELECT id,
  CASE
    WHEN MOD(id, 2) = 0 THEN LAG(student, 1) OVER ()
    WHEN MOD(id, 2) = 1 THEN IF(id = (SELECT MAX(id) FROM seat), student, LEAD(student, 1) OVER ())
  END AS student
FROM seat;
```

Method 2 : (Faster)
```sql
SELECT CASE
    WHEN MOD(id, 2) = 0 THEN id - 1
    WHEN MOD(id, 2) = 1 THEN IF(id = (SELECT MAX(id) FROM seat), id, id + 1)
  END AS id, student
FROM seat
ORDER BY id ASC;
```

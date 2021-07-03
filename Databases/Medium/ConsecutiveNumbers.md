## [Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers)

### Solution :

Method 1 :
```sql
SELECT DISTINCT Num AS 'ConsecutiveNums'
FROM (
  SELECT Num, LEAD(Num, 1) OVER () AS next, LEAD(Num, 2) OVER () AS next_2
  FROM Logs
) AS temp
WHERE Num = next and Num = next_2;
```

Method 2 :
```sql
SELECT DISTINCT Num AS 'ConsecutiveNums'
FROM (
  SELECT Num, LAG(Num, 1) OVER () AS previous, LAG(Num, 2) OVER () AS previous_2
  FROM Logs
) AS temp
WHERE Num = previous and Num = previous_2;
```

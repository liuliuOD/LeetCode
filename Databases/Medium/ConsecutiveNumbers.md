## [Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers)

### Solution :

Method 1 (LEAD) :
```sql
SELECT DISTINCT Num AS 'ConsecutiveNums'
FROM (
  SELECT Num, LEAD(Num, 1) OVER () AS next, LEAD(Num, 2) OVER () AS next_2
  FROM Logs
) AS temp
WHERE Num = next and Num = next_2;
```

Method 2 (LAG) :
```sql
SELECT DISTINCT Num AS 'ConsecutiveNums'
FROM (
  SELECT Num, LAG(Num, 1) OVER () AS previous, LAG(Num, 2) OVER () AS previous_2
  FROM Logs
) AS temp
WHERE Num = previous and Num = previous_2;
```

Method 3 (EXISTS) :
```sql
SELECT l.num AS 'ConsecutiveNums'
FROM logs AS l
WHERE EXISTS (
    SELECT id
    FROM logs AS l2
    WHERE l2.id IN (l.id+1, l.id+2)
      AND l2.num = l.num
      GROUP BY l2.num
      HAVING COUNT(l2.num) = 2
)
GROUP BY l.num;
```

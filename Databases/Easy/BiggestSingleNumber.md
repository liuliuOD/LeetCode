## [Biggest Single Number](https://leetcode.com/problems/biggest-single-number)

### Solution :

Method 1 :
```sql
SELECT (
  SELECT num
  FROM MyNumbers
  GROUP BY num
  HAVING COUNT(*) = 1
  ORDER bY num DESC
  LIMIT 1
) AS num;
```

Method 2 :
```sql
SELECT MAX(tmp.num) AS num 
FROM (
  SELECT num
  FROM MyNumbers
  GROUP BY num
  HAVING COUNT(*) = 1
) tmp;
```

Method 3 (Only applicable when the database always has at least one record):
```sql
SELECT IF(COUNT(num) = 1, num, NULL) AS num
FROM MyNumbers
GROUP BY num
ORDER bY COUNT(*) ASC, num DESC
LIMIT 1;
```

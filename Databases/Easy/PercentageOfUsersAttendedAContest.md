## [Percentage Of Users Attended A Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest)

### Solution :

Method 1 :
```sql
SELECT contest_id, ROUND(COUNT(*) / (SELECT COUNT(DISTINCT user_id) FROM users) * 100, 2) AS percentage
FROM register
GROUP BY contest_id
ORDER BY percentage DESC, contest_id ASC;
```

Method 2 :
```sql
WITH temp AS (
  SELECT COUNT(DISTINCT user_id) AS amount FROM users
);

SELECT contest_id, ROUND(COUNT(*) / (SELECT amount FROM temp) * 100, 2) AS percentage
FROM register
GROUP BY contest_id
ORDER BY percentage DESC, contest_id ASC;
```

Method 3 :
```sql
WITH temp AS (
  SELECT COUNT(DISTINCT user_id) AS amount FROM users
);

SELECT contest_id, ROUND(COUNT(*) / amount * 100, 2) AS percentage
FROM register, temp
GROUP BY contest_id
ORDER BY percentage DESC, contest_id ASC;
```

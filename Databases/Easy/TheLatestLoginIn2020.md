## [The Latest Login In 2020](https://leetcode.com/problems/the-latest-login-in-2020)

### Solution :

Method 1 :
```sql
SELECT user_id, MAX(time_stamp) AS last_stamp
FROM logins
WHERE time_stamp BETWEEN '2020-01-01 00:00:00' AND '2021-01-01 00:00:00'
GROUP BY user_id;
```

Method 2 :
```sql
SELECT user_id, MAX(time_stamp) AS last_stamp
FROM logins
WHERE YEAR(time_stamp) = 2020
GROUP BY user_id;
```

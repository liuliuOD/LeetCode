## [Find Followers Count](https://leetcode.com/problems/find-followers-count)

### Solution :

Method 1 :
```sql
SELECT user_id, COUNT(user_id) AS followers_count
FROM followers
GROUP BY user_id
ORDER BY user_id ASC;
```

Method 2 :
```sql
SELECT DISTINCT user_id, COUNT(user_id) OVER (PARTITION BY user_id ORDER BY user_id) AS followers_count
FROM followers;
```

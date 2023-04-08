## [Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table)

### Solution :

Method 1 :
```sql
SELECT user_id, CONCAT(UPPER(SUBSTR(name, 1, 1)), LOWER(SUBSTR(name, 2, CHAR_LENGTH(name) - 1))) AS name
FROM users
ORDER BY user_id ASC;
```

Method 2 :
```sql
SELECT user_id, CONCAT(UPPER(LEFT(name, 1)), LOWER(RIGHT(name, CHAR_LENGTH(name) - 1))) AS name
FROM users
ORDER BY user_id ASC;
```

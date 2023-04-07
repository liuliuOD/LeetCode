## [Find Users With Valid EMails](https://leetcode.com/problems/find-users-with-valid-e-mails)

### Solution :

Method 1 :
```sql
SELECT *
FROM users
WHERE mail REGEXP '^[A-Za-z]+[\\w.-]*@leetcode\\.com';
```

Method 2 :
```sql
SELECT *
FROM users
WHERE REGEXP_LIKE(mail, '^[A-Za-z]+[\\w.-]*@leetcode\\.com');
```

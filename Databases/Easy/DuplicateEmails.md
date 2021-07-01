## [Duplicate Emails](https://leetcode.com/problems/duplicate-emails)

### Solution :
```sql
SELECT Email
FROM Person
GROUP BY Email
HAVING count(Email) > 1
```

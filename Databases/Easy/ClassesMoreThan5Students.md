## [Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students)

### Solution :

```sql
SELECT class
FROM courses
GROUP BY class
HAVING COUNT(DISTINCT student) >= 5;
```

## [Find Total Time Spent By Each Employee](https://leetcode.com/problems/find-total-time-spent-by-each-employee)

### Solution :

Method 1 :
```sql
SELECT event_day AS day, emp_id, SUM(out_time - in_time) AS total_time
FROM employees
GROUP BY emp_id, event_day;
```

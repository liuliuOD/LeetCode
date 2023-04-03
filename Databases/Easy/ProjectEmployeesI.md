## [Project Employees I](https://leetcode.com/problems/project-employees-i)

### Solution :

Method 1 :
```sql
SELECT p.project_id, ROUND(SUM(e.experience_years) / COUNT(*), 2) AS average_years
FROM project AS p
JOIN employee AS e ON e.employee_id = p.employee_id
GROUP BY p.project_id;
```

Method 2 :
```sql
SELECT p.project_id, ROUND(AVG(e.experience_years), 2) AS average_years
FROM project AS p
JOIN employee AS e ON e.employee_id = p.employee_id
GROUP BY p.project_id;
```

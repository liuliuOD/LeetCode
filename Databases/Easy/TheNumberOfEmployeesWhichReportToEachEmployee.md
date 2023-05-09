## [The Number Of Employees Which Report To Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee)

### Solution :

Method 1 :
```sql
SELECT e2.employee_id, e2.name, COUNT(*) AS reports_count, ROUND(AVG(e1.age)) AS average_age
FROM employees AS e1
JOIN employees AS e2 ON e2.employee_id = e1.reports_to
WHERE e2.employee_id IS NOT NULL
GROUP BY e2.employee_id
ORDER BY e2.employee_id ASC;
```

Method 2 (Too slow) :
```sql
SELECT reports_to AS employee_id, (SELECT name FROM employees AS e WHERE e.employee_id = employees.reports_to) AS name, COUNT(*) AS reports_count, ROUND(AVG(age)) AS average_age
FROM employees
WHERE reports_to IS NOT NULL
GROUP BY reports_to
ORDER BY reports_to ASC;
```

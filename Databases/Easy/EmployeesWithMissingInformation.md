## [Employees With Missing Information](https://leetcode.com/problems/employees-with-missing-information)

### Solution :

Method 1 :
```sql
SELECT employee_id
FROM employees AS e
LEFT JOIN salaries AS s
USING (employee_id)
WHERE s.salary IS NULL
UNION
SELECT employee_id
FROM employees AS e
RIGHT JOIN salaries AS s
USING (employee_id)
WHERE e.name IS NULL
ORDER BY employee_id ASC;
```

Method 2 :
```sql
SELECT employee_id
FROM (
  SELECT *
  FROM employees AS e
  LEFT JOIN salaries AS s
  USING (employee_id)
  UNION
  SELECT *
  FROM employees AS e
  RIGHT JOIN salaries AS s
  USING (employee_id)
) AS full
WHERE name IS NULL
  OR salary IS NULL
ORDER BY employee_id ASC;
```

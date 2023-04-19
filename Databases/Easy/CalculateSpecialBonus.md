## [Calculate Special Bonus](https://leetcode.com/problems/calculate-special-bonus)

### Solution :

Method 1 :
```sql
SELECT employee_id, (CASE WHEN employee_id % 2 = 1 AND SUBSTR(name, 1, 1) != 'M' THEN salary ELSE 0 END) AS bonus
FROM employees
ORDER BY employee_id ASC;
```

Method 2 :
```sql
SELECT employee_id, IF(employee_id % 2 = 1 AND SUBSTR(name, 1, 1) != 'M', salary, 0) AS bonus
FROM employees
ORDER BY employee_id ASC;
```

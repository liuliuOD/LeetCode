## [Primary Department For Each Employee](https://leetcode.com/problems/primary-department-for-each-employee)

### Solution :

Method 1 :
```sql
SELECT employee_id, department_id
FROM (
  SELECT *, COUNT(*) OVER(PARTITION BY employee_id) AS employee_amount
  FROM employee
) AS temp
WHERE primary_flag = 'Y'
  OR employee_amount = 1;
```

Method 2 (behaviors of `GROUP BY` in MySQL are different with other):
```sql
SELECT employee_id, (CASE WHEN COUNT(*) = 1 THEN department_id
ELSE SUM((primary_flag = 'Y') * department_id) END) AS department_id
FROM employee
GROUP BY employee_id;
```

Method 3 :
```sql
SELECT employee_id, department_id
FROM employee
GROUP BY employee_id
HAVING COUNT(*) = 1
UNION
SELECT employee_id, department_id
FROM employee
WHERE primary_flag = 'Y';
```

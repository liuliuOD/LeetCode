## [Employee Bonus](https://leetcode.com/problems/employee-bonus)

### Solution :

Method 1 :
```sql
SELECT e.name, b.bonus
FROM employee AS e
LEFT JOIN bonus AS b ON b.empId = e.empId
WHERE b.bonus < 1000
 OR b.bonus IS NULL;
```

Method 2 :
```sql
SELECT e.name, b.bonus
FROM employee AS e
LEFT JOIN bonus AS b ON b.empId = e.empId
WHERE IFNULL(b.bonus, 0) < 1000;
```

Method 3 :
```sql
SELECT e.name, b.bonus
FROM employee AS e
LEFT JOIN bonus AS b ON b.empId = e.empId
WHERE COALESCE(b.bonus, 0) < 1000;
```

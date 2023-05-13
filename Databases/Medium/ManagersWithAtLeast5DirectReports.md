## [Managers With At Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports)

### Solution :

Method 1 :
```sql
SELECT name
FROM employee
WHERE EXISTS (
    SELECT *
    FROM employee AS e
    WHERE e.managerId = employee.id
    GROUP BY e.managerId
    HAVING COUNT(*) >= 5
);
```

Method 2 :
```sql
SELECT e1.name
FROM employee AS e1
JOIN employee AS e2 ON e1.id = e2.managerId
GROUP BY e1.id
HAVING COUNT(e1.id) >= 5;
```

Method 3 :
```sql
SELECT name
FROM employee
WHERE id IN (
    SELECT managerId
    FROM employee
    WHERE managerId IS NOT NULL
    GROUP BY managerId
    HAVING COUNT(*) >= 5
);
```

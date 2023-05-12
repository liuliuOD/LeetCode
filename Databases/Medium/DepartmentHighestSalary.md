## [Department Highest Salary](https://leetcode.com/problems/department-highest-salary)

### Solution :

Method 1 (RANK) :
```sql
SELECT temp.Department, temp.Employee, temp.Salary
FROM (
  SELECT D.Name AS Department, E.Name AS Employee, E.Salary, RANK() OVER (PARTITION BY DepartmentId ORDER BY Salary DESC) AS 'rank'
  FROM Employee AS E
  JOIN Department AS D ON D.Id = E.DepartmentId
) temp
WHERE temp.rank = 1;
```

Method 2 (RANK) :
```sql
SELECT D.Name AS Department, temp.Employee, temp.Salary
FROM (
  SELECT DepartmentId, Name AS Employee, Salary, RANK() OVER (PARTITION BY DepartmentId ORDER BY Salary DESC) AS 'rank'
  FROM Employee
) temp
JOIN Department AS D ON D.Id = temp.DepartmentId
WHERE temp.rank = 1;
```

Method 3 (RANK) :
```sql
WITH temp AS (
  SELECT D.Name AS Department, E.Name AS Employee, Salary, RANK() OVER (PARTITION BY DepartmentId ORDER BY Salary DESC) AS 'rank'
  FROM Employee AS E
  JOIN Department AS D ON D.Id = E.DepartmentId
);

SELECT Department, Employee, Salary
FROM temp
WHERE temp.rank = 1;
```

Method 4 : (Very Slow)
```sql
SELECT D.Name AS Department, E.Name AS Employee, E.Salary
FROM Employee AS E
JOIN Department AS D ON D.Id = E.DepartmentId
WHERE E.Salary = (
  SELECT MAX(Salary)
  FROM Employee
  WHERE E.DepartmentId = Employee.DepartmentId
);
```

Method 5 (EXISTS) :
```sql
SELECT d.name AS 'Department', e.name AS 'Employee', e.salary AS 'Salary'
FROM employee AS e
JOIN department AS d ON e.departmentId = d.id
WHERE EXISTS (
  SELECT id
  FROM employee AS e2
  WHERE e2.departmentId = e.departmentId
    GROUP BY e2.departmentId
    HAVING MAX(e2.salary) = e.salary
);
```

Method 6 (IN multiple columns) :
```sql
SELECT d.name AS 'Department', e.name AS 'Employee', e.salary AS 'Salary'
FROM employee AS e
JOIN department AS d ON e.departmentId = d.id
WHERE (e.departmentId, e.salary) IN (
  SELECT departmentId, MAX(salary)
  FROM employee AS e2
  GROUP BY e2.departmentId
);
```

## [Department Highest Salary](https://leetcode.com/problems/department-highest-salary)

### Solution :

Method 1 :
```sql
SELECT temp.Department, temp.Employee, temp.Salary
FROM (
  SELECT D.Name AS Department, E.Name AS Employee, E.Salary, RANK() OVER (PARTITION BY DepartmentId ORDER BY Salary DESC) AS 'rank'
  FROM Employee AS E
  JOIN Department AS D ON D.Id = E.DepartmentId
) temp
WHERE temp.rank = 1;
```

Method 2 :
```sql
SELECT D.Name AS Department, temp.Employee, temp.Salary
FROM (
  SELECT DepartmentId, Name AS Employee, Salary, RANK() OVER (PARTITION BY DepartmentId ORDER BY Salary DESC) AS 'rank'
  FROM Employee
) temp
JOIN Department AS D ON D.Id = temp.DepartmentId
WHERE temp.rank = 1;
```

Method 3 :
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

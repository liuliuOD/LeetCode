## [Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries)

### Solution :

```sql
WITH temp AS (
  SELECT Name, Salary, DepartmentId, DENSE_RANK() OVER (PARTITION BY DepartmentId ORDER BY Salary DESC) AS 'rank'
  FROM Employee
);

SELECT D.Name AS Department, T.Name AS Employee, T.Salary
FROM temp AS T
JOIN Department AS D ON T.DepartmentId = D.Id
WHERE T.rank <= 3;
```

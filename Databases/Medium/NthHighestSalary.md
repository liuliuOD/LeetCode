## [Nth Highest Salary](https://leetcode.com/problems/nth-highest-salary)

### Solution :
```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
      SELECT 
        IF(MAX(temp.rank) < N, NULL, Salary)
      FROM (
          SELECT Salary, DENSE_RANK() OVER (ORDER BY Salary DESC) AS 'rank'
          FROM Employee
        ) AS temp
      WHERE temp.rank = N
  );
END
```

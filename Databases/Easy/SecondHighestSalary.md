## [Second Highest Salary](https://leetcode.com/problems/second-highest-salary)

### Solution :

Method 1 :
```sql
select MAX(Salary) as SecondHighestSalary 
from Employee
where Salary not in (
    select MAX(Salary)
    from Employee
)
```

Method 2 :
```sql
select (
    select DISTINCT Salary
    from Employee
    ORDER BY Salary DESC
    LIMIT 1
    OFFSET 1
) as SecondHighestSalary
```
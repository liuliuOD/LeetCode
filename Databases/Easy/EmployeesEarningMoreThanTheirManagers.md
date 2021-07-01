## [Employees Earning More Than Their Managers](https://leetcode.com/problems/employees-earning-more-than-their-managers)

### Solution :

Method 1 :
```sql
select Name as 'Employee'
from Employee as employee
where employee.Salary > (
    select Salary
    from Employee as manager
    where employee.ManagerId = manager.Id
)
```

Method 2 : (faster)
```sql
select employee.Name as Employee
from Employee as employee
join Employee as manager
on employee.managerId = manager.Id
where employee.Salary > manager.Salary
```

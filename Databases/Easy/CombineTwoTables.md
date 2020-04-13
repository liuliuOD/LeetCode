## [Combine Two Tables](https://leetcode.com/problems/combine-two-tables)

### Solution :
```sql
select FirstName, LastName, City, State
from Person as p
left join Address as a
on p.PersonId = a.PersonId
```
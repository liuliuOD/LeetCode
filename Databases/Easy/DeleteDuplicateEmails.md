## [Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails)

### Solution :

Method 1 :
```sql
delete p1
from Person as p1, Person as p2
where p1.Email = p2.Email
    and p1.Id > p2.Id
```

Method 2 :
```sql
delete
from Person
where Id not in (
    select *
    from (
        select MIN(Id)
        from Person
        group by Email
    ) as tmp
)
```
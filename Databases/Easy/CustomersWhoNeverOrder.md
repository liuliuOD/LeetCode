## [Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/)

### Solution :
```sql
SELECT Name AS 'Customers'
FROM Customers
WHERE Id NOT IN (
    SELECT CustomerId FROM Orders
)
```

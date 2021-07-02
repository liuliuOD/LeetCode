## [Swap Salary](https://leetcode.com/problems/swap-salary)

### Solution :

Method 1 :
```sql
UPDATE Salary
SET sex = CASE
  WHEN sex = 'm'
    THEN 'f'
  ELSE
    'm'
  END;
```

Method 2 :
```sql
UPDATE Salary
SET sex = IF(sex = 'f', 'm', 'f');
```

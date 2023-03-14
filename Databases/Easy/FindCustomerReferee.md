## [Find Customer Referee](https://leetcode.com/problems/find-customer-referee)

### Solution :

Method 1 :
```sql
SELECT name
FROM customer
WHERE referee_id != 2
  OR referee_id IS NULL;
```

Method 2 :
```sql
SELECT name
FROM customer
WHERE id NOT IN (SELECT id FROM customer WHERE referee_id = 2)
```

Method 3 :
```sql
SELECT name
FROM customer
WHERE IFNULL(referee_id, -1) != 2;
```

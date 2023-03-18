## [Sales Person](https://leetcode.com/problems/sales-person)

### Solution :

Method 1 :
```sql
SELECT sp.name
FROM SalesPerson AS sp
WHERE NOT EXISTS (
  SELECT * FROM orders AS o WHERE o.sales_id = sp.sales_id AND o.com_id IN (
    SELECT com_id FROM company AS c WHERE c.name = 'RED'
  )
);
```

Method 2 :
```sql
WITH RED_COM_ID AS (
  SELECT com_id FROM company AS c WHERE c.name = 'RED'
);

SELECT sp.name
FROM SalesPerson AS sp
WHERE NOT EXISTS (
  SELECT *
  FROM orders AS o
  JOIN RED_COM_ID AS rci ON rci.com_id = o.com_id
    WHERE o.sales_id = sp.sales_id
);
```

Method 3 :
```sql
WITH RED_COM_ID AS (
  SELECT com_id FROM company AS c WHERE c.name = 'RED'
);

SELECT name from SalesPerson AS sp
WHERE sp.sales_id NOT IN
(
  SELECT o.sales_id
  FROM orders AS o
  JOIN RED_COM_ID AS rci ON rci.com_id = o.com_id
);
```

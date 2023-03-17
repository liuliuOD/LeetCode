## [Customer Placing the Largest Number of Orders](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders)

### Solution :

Method 1 :
```sql
SELECT customer_number
FROM (
  SELECT customer_number, COUNT(*) AS AMOUNT
  FROM orders
  GROUP BY customer_number
) AS temp
ORDER BY AMOUNT DESC
LIMIT 1;
```

Method 2 :
```sql
WITH temp AS (
    SELECT customer_number, COUNT(*) AS AMOUNT FROM orders GROUP BY customer_number
);
SELECT customer_number
FROM temp
ORDER BY AMOUNT DESC
LIMIT 1;
```

Method 3 :
```sql
SELECT customer_number
FROM orders
GROUP BY customer_number
ORDER BY COUNT(*) DESC
LIMIT 1;
```

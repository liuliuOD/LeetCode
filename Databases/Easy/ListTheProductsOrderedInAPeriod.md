## [List The Products Ordered In A Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period)

### Solution :

Method 1 :
```sql
SELECT p.product_name, SUM(o.unit) AS unit
FROM orders AS o
JOIN products AS p ON p.product_id = o.product_id
WHERE o.order_date BETWEEN '2020-02-01' AND '2020-02-29'
GROUP BY o.product_id
HAVING unit >= 100;
```

Method 2 :
```sql
SELECT p.product_name, SUM(o.unit) AS unit
FROM orders AS o
JOIN products AS p
USING (product_id)
WHERE o.order_date BETWEEN '2020-02-01' AND '2020-02-29'
GROUP BY o.product_id
HAVING unit >= 100;
```

Method 3 :
```sql
SELECT (SELECT product_name FROM products AS p WHERE p.product_id = o.product_id) AS product_name, SUM(o.unit) AS unit
FROM orders AS o
WHERE o.order_date BETWEEN '2020-02-01' AND '2020-02-29'
GROUP BY o.product_id
HAVING unit >= 100;
```

Method 4 :
```sql
SELECT p.product_name, SUM(o.unit) AS unit
FROM orders AS o
JOIN products AS p
USING (product_id)
WHERE o.order_date LIKE '2020-02-%'
GROUP BY o.product_id
HAVING unit >= 100;
```

## [Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i)

### Solution :

Method 1 :
```sql
SELECT p.product_name, s.year, s.price
FROM sales AS s
JOIN product AS p ON p.product_id = s.product_id;
```

Method 2 :
```sql
SELECT p.product_name, s.year, s.price
FROM product AS p
JOIN sales AS s ON s.product_id = p.product_id;
```

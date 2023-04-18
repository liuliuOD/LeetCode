## [Recyclable And Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products)

### Solution :
```sql
SELECT product_id
FROM products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';
```

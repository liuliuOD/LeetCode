## [Average Selling Price](https://leetcode.com/problems/average-selling-price)

### Solution :

Method 1 :
```sql
SELECT us.product_id, ROUND(SUM(us.units * p.price) / SUM(us.units), 2) AS average_price
FROM UnitsSold AS us
JOIN prices AS p ON p.product_id = us.product_id AND us.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY us.product_id;
```

Method 2 :
```sql
SELECT us.product_id, ROUND(SUM(us.units * p.price) / SUM(us.units), 2) AS average_price
FROM UnitsSold AS us
JOIN prices AS p ON p.product_id = us.product_id
WHERE us.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY us.product_id;
```

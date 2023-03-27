## [Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date)

### Solution :

Method 1 :
```sql
SELECT sell_date, COUNT(DISTINCT product) AS num_sold, GROUP_CONCAT(DISTINCT product) AS products
FROM activities
GROUP BY sell_date
ORDER BY sell_date ASC, product ASC;
```

Method 2 :
```sql
SELECT sell_date, COUNT(DISTINCT product) AS num_sold, GROUP_CONCAT(DISTINCT product ORDER BY product ASC) AS products
FROM activities
GROUP BY sell_date
ORDER BY sell_date ASC;
```

Method 3 :
```sql
SELECT sell_date, COUNT(product) AS num_sold, GROUP_CONCAT(product ORDER BY product ASC) AS products
FROM (SELECT DISTINCT sell_date, product FROM activities) AS activities
GROUP BY sell_date
ORDER BY sell_date ASC;
```

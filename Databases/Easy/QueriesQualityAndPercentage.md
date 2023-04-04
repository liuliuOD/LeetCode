## [Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage)

### Solution :

Method 1 :
```sql
SELECT query_name, ROUND(SUM(rating / position) / COUNT(*), 2) AS quality, ROUND(SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS poor_query_percentage
FROM queries
GROUP BY query_name;
```

Method 2 :
```sql
SELECT query_name, ROUND(AVG(rating / position), 2) AS quality, ROUND(SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS poor_query_percentage
FROM queries
GROUP BY query_name;
```

Method 3 :
```sql
SELECT query_name, ROUND(AVG(rating / position), 2) AS quality, ROUND(AVG(CASE WHEN rating < 3 THEN 1 ELSE 0 END) * 100, 2) AS poor_query_percentage
FROM queries
GROUP BY query_name;
```

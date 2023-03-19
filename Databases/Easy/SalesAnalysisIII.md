## [Sales Analysis III](https://leetcode.com/problems/sales-analysis-iii)

### Solution :

Method 1 :
```sql
SELECT p.product_id, p.product_name
FROM product AS p
JOIN sales AS s ON s.product_id = p.product_id
WHERE s.sale_date BETWEEN '2019-01-01' AND '2019-03-31'
  AND NOT EXISTS (
    SELECT product_id
    FROM sales AS s2
    WHERE s2.sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31' 
      AND s2.product_id = s.product_id
  )
  GROUP BY p.product_id;
```

Method 2 :
```sql
SELECT p.product_id, p.product_name
FROM product AS p
WHERE EXISTS (
    SELECT product_id
    FROM sales AS s
    WHERE s.sale_date BETWEEN '2019-01-01' AND '2019-03-31' 
      AND s.product_id = p.product_id
  )
  AND NOT EXISTS (
    SELECT product_id
    FROM sales AS s
    WHERE s.sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31' 
      AND s.product_id = p.product_id
  )
  GROUP BY p.product_id;
```

Method 3 :
```sql
SELECT p.product_id, p.product_name
FROM product AS p
WHERE EXISTS (
    SELECT s.product_id
    FROM sales AS s
    LEFT JOIN sales AS s2 ON s2.product_id = s.product_id AND s2.sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'
    WHERE s.sale_date BETWEEN '2019-01-01' AND '2019-03-31' 
      AND s.product_id = p.product_id
      AND s2.product_id IS NULL
  )
  GROUP BY p.product_id;
```

Method 4 :
```sql
SELECT p.product_id, p.product_name
FROM product AS p
WHERE p.product_id IN (
    SELECT s.product_id
    FROM sales AS s
    LEFT JOIN sales AS s2 ON s2.product_id = s.product_id AND s2.sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'
    WHERE s.sale_date BETWEEN '2019-01-01' AND '2019-03-31' 
      AND s.product_id = p.product_id
      AND s2.product_id IS NULL
  )
  GROUP BY p.product_id;
```

Method 5 :
```sql
SELECT p.product_id, p.product_name
FROM product AS p
WHERE p.product_id IN (
    SELECT s.product_id
    FROM sales AS s
    LEFT JOIN sales AS s2 ON s2.product_id = s.product_id AND s2.sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'
    WHERE s.sale_date BETWEEN '2019-01-01' AND '2019-03-31' 
      AND s.product_id = p.product_id
      AND s2.product_id IS NULL
    GROUP BY s.product_id
  );
```

Method 6 :
```sql
SELECT p.product_id, p.product_name
FROM product AS p
JOIN (
  SELECT s.product_id
  FROM sales AS s
  LEFT JOIN sales AS s2 ON s2.product_id = s.product_id AND s2.sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'
  WHERE s.sale_date BETWEEN '2019-01-01' AND '2019-03-31' 
    AND s2.product_id IS NULL
  GROUP BY s.product_id
) AS s ON s.product_id = p.product_id;
```

Method 7 :
```sql
WITH s AS (
  SELECT s.product_id
  FROM sales AS s
  LEFT JOIN sales AS s2 ON s2.product_id = s.product_id AND s2.sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'
  WHERE s.sale_date BETWEEN '2019-01-01' AND '2019-03-31' 
    AND s2.product_id IS NULL
  GROUP BY s.product_id
);

SELECT p.product_id, p.product_name
FROM product AS p
JOIN s ON s.product_id = p.product_id;
```

Method 8 :
```sql
SELECT p.product_id, p.product_name
FROM product AS p
WHERE EXISTS (
  SELECT product_id
  FROM sales AS s
  WHERE s.product_id = p.product_id
  GROUP BY s.product_id
  HAVING MIN(s.sale_date) >= '2019-01-01'
    AND MAX(s.sale_date) <= '2019-03-31'
)
GROUP BY p.product_id;
```

Method 9 :
```sql
SELECT p.product_id, p.product_name
FROM product AS p
JOIN sales AS s ON s.product_id = p.product_id
GROUP BY s.product_id
HAVING MIN(s.sale_date) >= '2019-01-01'
  AND MAX(s.sale_date) <= '2019-03-31';
```

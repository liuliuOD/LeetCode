## [Triangle Judgement](https://leetcode.com/problems/triangle-judgement)

### Solution :

Method 1 :
```sql
SELECT x, y, z, CASE WHEN z >= x + y
 OR y >= x + z
 OR x >= y + z THEN 'No' ELSE 'Yes' END AS triangle
FROM triangle;
```

Method 2 :
```sql
SELECT x, y, z, CASE WHEN x + y > z
 AND x + z > y
 AND y + z > x THEN 'Yes' ELSE 'No' END AS triangle
FROM triangle;
```

Method 3 :
```sql
SELECT x, y, z, IF(x + y > z AND x + z > y AND y + z > x, 'Yes', 'No') AS triangle
FROM triangle;
```

Method 4 :
```sql
SELECT x, y, z, IF((x + y + z) / 2 > GREATEST(x, y, z), 'Yes', 'No') AS triangle
FROM triangle;
```

Method 5 :
```sql
SELECT x, y, z, CASE WHEN (x + y + z) / 2 > GREATEST(x, y, z) THEN 'Yes' ELSE 'No' END AS triangle
FROM triangle;
```

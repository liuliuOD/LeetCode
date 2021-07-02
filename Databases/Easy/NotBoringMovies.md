## [Not Boring Movies](https://leetcode.com/problems/not-boring-movies)

### Solution :

Method 1 :
```sql
SELECT *
FROM Cinema
WHERE id % 2 = 1
  AND description != 'boring'
  ORDER BY rating DESC;
```

Method 2 :
```sql
SELECT *
FROM Cinema
WHERE mod(id, 2) = 1
  AND description != 'boring'
  ORDER BY rating DESC;
```

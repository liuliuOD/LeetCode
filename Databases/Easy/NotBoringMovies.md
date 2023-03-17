## [Not Boring Movies](https://leetcode.com/problems/not-boring-movies)

### Solution :

Method 1 :
```sql
SELECT *
FROM cinema
WHERE id % 2 = 1
  AND description != 'boring'
  ORDER BY rating DESC;
```

Method 2 :
```sql
SELECT *
FROM cinema
WHERE MOD(id, 2) = 1
  AND description != 'boring'
  ORDER BY rating DESC;
```

Method 3 :
```sql
SELECT *
FROM cinema
WHERE MOD(id, 2) = 1
  AND id NOT IN (SELECT id FROM cinema WHERE description = 'boring')
  ORDER BY rating DESC;
```

Method 4 :
```sql
SELECT *
FROM cinema
WHERE id & 1 = 1 AND description != 'boring'
  ORDER BY rating DESC;
```

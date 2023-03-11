## [Rising Temperature](https://leetcode.com/problems/rising-temperature/)

### Solution :

Method 1 :
```sql
SELECT id
FROM weather AS w
WHERE w.temperature > (SELECT w2.temperature
  FROM weather AS w2
  WHERE w2.recordDate = DATE_SUB(w.recordDate, INTERVAL 1 DAY) LIMIT 1);
```

Method 2 :
```sql
SELECT w.id
FROM Weather w
JOIN Weather w2 ON w2.recordDate = DATE_SUB(w.recordDate, INTERVAL 1 DAY)
WHERE w.temperature > w2.temperature;
```

Method 3 :
```sql
SELECT w.id
FROM weather AS w, weather AS w2
WHERE w.temperature > w2.temperature
  AND DATEDIFF(w.recordDate, w2.recordDate) = 1;
```

Method 4 :
```sql
SELECT w.id
FROM weather AS w, weather AS w2
WHERE DATE_SUB(w.recordDate, INTERVAL 1 DAY) = w2.recordDate
  AND w.temperature > w2.temperature;
```

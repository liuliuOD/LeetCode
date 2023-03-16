## [Big Countries](https://leetcode.com/problems/big-countries)

### Solution :

Method 1 :
```sql
SELECT name, population, area
FROM world
WHERE area >= 3000000
  OR population >= 25000000;
```

Method 2 :
```sql
SELECT name, population, area
FROM world
WHERE area >= 3000000
UNION
SELECT name, population, area
FROM world
WHERE population >= 25000000;
```

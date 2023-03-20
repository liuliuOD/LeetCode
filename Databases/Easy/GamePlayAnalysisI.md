## [Game Play Analysis I](https://leetcode.com/problems/game-play-analysis-i)

### Solution :

Method 1 :
```sql
SELECT player_id, MIN(event_date) AS first_login
FROM activity
GROUP BY player_id;
```

Method 2 :
```sql
SELECT player_id, event_date AS first_login
FROM (
  SELECT player_id, event_date, RANK() OVER (PARTITION BY player_id ORDER BY event_date ASC) AS sort
  FROM activity
) AS temp
WHERE sort = 1;
```

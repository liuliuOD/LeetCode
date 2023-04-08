## [Average Time Of Process Per Machine](https://leetcode.com/problems/average-time-of-process-per-machine)

### Solution :

Method 1 :
```sql
SELECT machine_id, ROUND(SUM(processing_time) / COUNT(machine_id), 3) AS processing_time
FROM (
  SELECT machine_id, MAX(timestamp) - MIN(timestamp) AS processing_time
  FROM activity
  GROUP BY machine_id, process_id
) AS temp
GROUP BY machine_id;
```

Method 2 :
```sql
WITH temp AS (
  SELECT machine_id, MAX(timestamp) - MIN(timestamp) AS processing_time
  FROM activity
  GROUP BY machine_id, process_id
);

SELECT machine_id, ROUND(SUM(processing_time) / COUNT(machine_id), 3) AS processing_time
FROM temp
GROUP BY machine_id;
```

Method 3 :
```sql
SELECT machine_id, ROUND(SUM(CASE WHEN activity_type = 'END' THEN timestamp WHEN activity_type = 'START' THEN -timestamp END) / COUNT(DISTINCT process_id), 3) AS processing_time
FROM activity
GROUP BY machine_id;
```

Method 4 :
```sql
SELECT a1.machine_id, ROUND(AVG(a2.timestamp - a1.timestamp), 3) AS processing_time
FROM activity AS a1
JOIN activity AS a2
USING (machine_id, process_id)
WHERE a1.activity_type = 'START' AND a2.activity_type = 'END'
GROUP BY a1.machine_id;
```

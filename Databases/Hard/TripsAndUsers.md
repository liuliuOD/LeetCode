## [Trips And Users](https://leetcode.com/problems/trips-and-users)

### Solution :

Method 1 :
```sql
SELECT Request_at AS Day, ROUND(COUNT(CASE WHEN Status = 'completed' THEN NULL ELSE 1 END) / COUNT(*), 2) AS 'Cancellation Rate'
FROM Trips
WHERE Client_Id IN (SELECT Users_Id FROM Users WHERE Banned = 'No')
  AND Driver_Id IN (SELECT Users_Id FROM Users WHERE Banned = 'No')
  AND Request_at BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY Request_at;
```

Method 2 :
```sql
SELECT t.Request_at AS Day, ROUND(COUNT(CASE WHEN t.Status = 'completed' THEN NULL ELSE 1 END) / COUNT(*), 2) AS 'Cancellation Rate'
FROM Trips AS t
JOIN users AS u1 ON u1.Users_Id = t.Client_Id
JOIN users AS u2 ON u2.Users_Id = t.Driver_Id
WHERE u1.Banned = 'No'
  AND u2.Banned = 'No'
  AND t.Request_at BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY t.Request_at;
```

Method 3 :
```sql
SELECT t.Request_at AS Day, ROUND(COUNT(CASE WHEN t.Status = 'completed' THEN NULL ELSE 1 END) / COUNT(*), 2) AS 'Cancellation Rate'
FROM Trips AS t
JOIN users AS u1 ON u1.Users_Id = t.Client_Id AND u1.Banned = 'No'
JOIN users AS u2 ON u2.Users_Id = t.Driver_Id AND u2.Banned = 'No'
WHERE t.Request_at BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY t.Request_at;
```

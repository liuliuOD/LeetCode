## [Reformat Department Table](https://leetcode.com/problems/reformat-department-table)

### Solution :

Method 1 :
```sql
SELECT id,
  SUM(IF(month = 'Jan', revenue, null)) as 'Jan_Revenue',
  SUM(IF(month = 'Feb', revenue, null)) as 'Feb_Revenue',
  SUM(IF(month = 'Mar', revenue, null)) as 'Mar_Revenue',
  SUM(IF(month = 'Apr', revenue, null)) as 'Apr_Revenue',
  SUM(IF(month = 'May', revenue, null)) as 'May_Revenue',
  SUM(IF(month = 'Jun', revenue, null)) as 'Jun_Revenue',
  SUM(IF(month = 'Jul', revenue, null)) as 'Jul_Revenue',
  SUM(IF(month = 'Aug', revenue, null)) as 'Aug_Revenue',
  SUM(IF(month = 'Sep', revenue, null)) as 'Sep_Revenue',
  SUM(IF(month = 'Oct', revenue, null)) as 'Oct_Revenue',
  SUM(IF(month = 'Nov', revenue, null)) as 'Nov_Revenue',
  SUM(IF(month = 'Dec', revenue, null)) as 'Dec_Revenue'
FROM Department
GROUP BY id;
```

Method 2 :
```sql
SELECT id,
  MAX(CASE WHEN month = 'Jan' THEN revenue ELSE NULL END) AS Jan_Revenue,
  MAX(CASE WHEN month = 'Feb' THEN revenue ELSE NULL END) AS Feb_Revenue,
  MAX(CASE WHEN month = 'Mar' THEN revenue ELSE NULL END) AS Mar_Revenue,
  MAX(CASE WHEN month = 'Apr' THEN revenue ELSE NULL END) AS Apr_Revenue,
  MAX(CASE WHEN month = 'May' THEN revenue ELSE NULL END) AS May_Revenue,
  MAX(CASE WHEN month = 'Jun' THEN revenue ELSE NULL END) AS Jun_Revenue,
  MAX(CASE WHEN month = 'Jul' THEN revenue ELSE NULL END) AS Jul_Revenue,
  MAX(CASE WHEN month = 'Aug' THEN revenue ELSE NULL END) AS Aug_Revenue,
  MAX(CASE WHEN month = 'Sep' THEN revenue ELSE NULL END) AS Sep_Revenue,
  MAX(CASE WHEN month = 'Oct' THEN revenue ELSE NULL END) AS Oct_Revenue,
  MAX(CASE WHEN month = 'Nov' THEN revenue ELSE NULL END) AS Nov_Revenue,
  MAX(CASE WHEN month = 'Dec' THEN revenue ELSE NULL END) AS Dec_Revenue
FROM Department
GROUP BY 1 ;
```

## [Article Views I](https://leetcode.com/problems/article-views-i)

### Solution :

Method 1 :
```sql
SELECT DISTINCT author_id AS id
FROM views
WHERE EXISTS (
  SELECT *
  FROM views AS v2
  WHERE v2.author_id = v2.viewer_id
    AND v2.author_id = views.author_id
  LIMIT 1
)
ORDER BY id ASC;
```

Method 2 :
```sql
SELECT DISTINCT author_id AS id
FROM views
WHERE author_id = viewer_id
ORDER BY id ASC;
```

Method 3 :
```sql
SELECT DISTINCT v1.author_id AS id
FROM views AS v1
JOIN views AS v2 ON v1.author_id = v2.author_id AND v1.author_id = v2.viewer_id
ORDER BY id ASC;
```

## [Rank Scores](https://leetcode.com/problems/rank-scores)

### Solution :
```sql
SELECT Score AS score, DENSE_RANK() OVER (ORDER BY Score DESC) AS 'Rank'
FROM Scores;
```

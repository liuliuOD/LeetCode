## [Invalid Tweets](https://leetcode.com/problems/invalid-tweets)

### Solution :

Method 1 :
```sql
SELECT tweet_id
FROM tweets
WHERE CHAR_LENGTH(content) > 15;
```

Method 2 (only if there are not special characters):
```sql
SELECT tweet_id
FROM tweets
WHERE LENGTH(content) > 15;
```

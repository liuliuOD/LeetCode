## [Customer Who Visited But Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions)

### Solution :

Method 1 :
```sql
SELECT v.customer_id, COUNT(*) AS count_no_trans
FROM visits AS v
LEFT JOIN transactions AS t ON t.visit_id = v.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
```

Method 2 :
```sql
SELECT customer_id, COUNT(*) AS count_no_trans
FROM visits
WHERE visit_id NOT IN (
  SELECT visit_id
  FROM transactions
)
GROUP BY customer_id;
```

Method 3 :
```sql
SELECT customer_id, COUNT(*) AS count_no_trans 
FROM visits
WHERE NOT EXISTS (
	SELECT visit_id
	FROM transactions AS t
	WHERE t.visit_id = visits.visit_id
	)
GROUP BY customer_id;
```

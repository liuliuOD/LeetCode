## [Bank Account Summary II](https://leetcode.com/problems/bank-account-summary-ii)

### Solution :

Method 1 :
```sql
SELECT u.name, SUM(t.amount) AS balance
FROM users AS u
JOIN transactions AS t ON t.account = u.account
GROUP BY u.account
HAVING balance > 10000;
```

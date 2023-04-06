## [Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier)

### Solution :

Method 1 :
```sql
SELECT e2.unique_id, e.name
FROM employees AS e
LEFT JOIN EmployeeUNI AS e2
USING (id);
```

Method 2 :
```sql
SELECT e2.unique_id, e.name
FROM employees AS e
LEFT JOIN EmployeeUNI AS e2 ON e2.id = e.id;
```

## [Patients With A Condition](https://leetcode.com/problems/patients-with-a-condition)

### Solution :

Method 1 :
```sql
SELECT patient_id, patient_name, conditions
FROM patients
WHERE conditions LIKE 'DIAB1%'
  OR conditions LIKE '% DIAB1%';
```

Method 2 :
<br>
`\b` means space or nothing.
```sql
SELECT * FROM patients
WHERE conditions REGEXP '\\bDIAB1';
```

Method 3 :
```sql
SELECT * FROM patients WHERE conditions REGEXP '^DIAB1| DIAB1';
```

Method 4 (very slow):
```sql
SELECT * FROM patients WHERE conditions REGEXP '(^| )DIAB1';
```

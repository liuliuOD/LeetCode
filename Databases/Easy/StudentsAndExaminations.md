## [Students And Examinations](https://leetcode.com/problems/students-and-examinations)

### Solution :
```sql
SELECT s.student_id, s.student_name, sj.subject_name, COUNT(e.student_id) AS attended_exams
FROM students AS s
JOIN subjects AS sj
LEFT JOIN examinations AS e ON s.student_id = e.student_id AND sj.subject_name = e.subject_name
GROUP BY s.student_id, sj.subject_name
ORDER BY s.student_id, sj.subject_name;
```

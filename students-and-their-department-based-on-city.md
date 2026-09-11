# Students and Their Department Based on City

## Problem Statement
Write a query to display the list of student's name and their department name who are all from 'Coimbatore'. Sort the result based on student's name.

**Database Schema Context:**
This query utilizes a College Management System (CMS) schema, specifically interacting with the `Student` and `Department` tables.

**Tables:**
- **Student:** `student_id` (PK), `student_name`, `address`, `city`, `department_id` (FK)
- **Department:** `department_id` (PK), `department_name`, `department_block_number`

---

## Solution

### Approach: Inner Join, Filtering, and Sorting
To combine related data from two separate tables based on a foreign key relationship and filter rows by a specific location:
1. **Joining Tables:** We perform an `INNER JOIN` between the `Student` table (`s`) and the `Department` table (`d`) using their common key (`s.department_id = d.department_id`).
2. **Filtering:** We restrict the records using `WHERE s.city = 'Coimbatore'` to extract only students belonging to that specific city.
3. **Sorting:** The `ORDER BY student_name` clause ensures the final output list is sorted alphabetically by the student names.

### SQL Query
```sql
SELECT 
    s.student_name,
    d.department_name
FROM Student AS s
INNER JOIN Department AS d
    ON s.department_id = d.department_id
WHERE s.city = 'Coimbatore'
ORDER BY student_name;

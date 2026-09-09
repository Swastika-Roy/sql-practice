# Categories Starting with 'M'

## Problem Statement
Write an SQL query to display the category id and category name whose name starts with 'M'.

Your output should have 2 columns as given below:
`CATEGORYID` | `CATEGORYNAME`

**Database Schema Context:**
This query is based on the `channelcategory` table from a television viewing database schema.

**Table: channelcategory**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| categoryid | varchar | Primary Key. The ID of the category. |
| categoryname | varchar | The name of the category. |

---

## Solution

### Approach: String Pattern Matching with LIKE
To filter records based on a specific string pattern, we use the `LIKE` operator along with wildcards.
1. **Filtering:** We use the condition `WHERE categoryname LIKE 'M%'`. The `%` is a wildcard character in SQL that represents zero, one, or multiple characters. Therefore, `'M%'` perfectly matches any string that strictly starts with the letter 'M'.
2. **Strict Aliasing:** Many automated assessment portals have strict output validation. Since the problem explicitly requires the output headers to be `CATEGORYID` and `CATEGORYNAME`, we use the `AS` keyword to alias our selected columns in uppercase, ensuring no test cases fail due to case sensitivity in the column names.

### SQL Query
```sql
SELECT 
    categoryid AS CATEGORYID, 
    categoryname AS CATEGORYNAME 
FROM channelcategory 
WHERE categoryname LIKE 'M%';

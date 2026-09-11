# Customers with Specific Account Types

## Problem Statement
Write an SQL query to display the first name, contact number, and balance of all the customers whose account type starts with "Sa". The output should be ordered by the customer's first name.

Your output should have 3 columns as given below:
`FIRST_NAME` | `CONTACT` | `BALANCE`

**Database Schema Context:**
This query integrates three tables from a banking schema: `customer`, `account`, and `account_type`.

---

## Solution

### Approach: Multi-Table Joins and String Filtering
To connect a customer's personal details with their financial balance and the categorical name of their account, we must perform a multi-table join.
1. **Joining Tables:** We use `INNER JOIN` to connect `customer` (alias `c`) to `account` (alias `a`) via `Customer_ID`. We then join `account` to `account_type` (alias `at`) via `Account_Type_ID`.
2. **Pattern Matching:** We apply the `WHERE` clause using the `LIKE 'Sa%'` operator on the `Account_Type_Name` column to isolate account types starting with "Sa" (e.g., Savings, Salary).
3. **Sorting:** The `ORDER BY c.First_Name` clause ensures the final result set is sorted alphabetically ascending by the customer's first name.
4. **Strict Aliasing:** We extract the required columns and explicitly alias them in uppercase using the `AS` keyword to meet strict output validation criteria.

### SQL Query
```sql
SELECT 
    c.First_Name AS FIRST_NAME,
    c.Contact AS CONTACT,
    a.Balance AS BALANCE
FROM customer AS c
INNER JOIN account AS a
    ON c.Customer_ID = a.Customer_ID
INNER JOIN account_type AS at
    ON at.Account_Type_ID = a.Account_Type_ID
WHERE at.Account_Type_Name LIKE 'Sa%'
ORDER BY c.First_Name;

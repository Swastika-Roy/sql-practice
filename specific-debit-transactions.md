# Specific Debit Transactions

## Problem Statement
Write an SQL query to display the transaction id, transaction amount, and transaction type of all the transactions whose transaction type is "Debit" and transaction amount is greater than 10000 but less than 50000.

Your output should have 3 columns as given below:
`TRANSACTION_ID` | `AMOUNT` | `TRANSACTION_TYPE`

**Database Schema Context:**
This query is built upon a banking schema containing tables like `branch`, `customer`, `account_type`, `account`, `loan`, and `transaction`. For this requirement, we focus specifically on the `transaction` table.

**Table: transaction**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| Transaction_ID | decimal | Primary Key. The ID of the transaction. |
| Account_ID | decimal | Foreign Key pointing to the account. |
| Transaction_Date | date | The date of the transaction. |
| Amount | decimal | The monetary value of the transaction. |
| Transaction_Type | varchar | The type of transaction (e.g., Debit, Credit). |

---

## Solution

### Approach: Filtering with Multiple Conditions and Aliasing
To extract the precise financial records matching both categorical and numerical criteria, we utilize conditional filtering.
1. **Filtering by Type:** We restrict our rows using `WHERE Transaction_Type = 'Debit'` to isolate only debit transactions.
2. **Numerical Range Filtering:** We apply range operators (`> 10000` and `< 50000`) combined with the `AND` operator to strictly capture amounts greater than 10000 and less than 50000, avoiding boundary inclusions like exact 10000 values.
3. **Strict Column Aliasing:** Automated assessment portals check for exact case-sensitive header names. We use the `AS` keyword to ensure output columns match `TRANSACTION_ID`, `AMOUNT`, and `TRANSACTION_TYPE` precisely.

### SQL Query
```sql
SELECT 
    Transaction_ID AS TRANSACTION_ID, 
    Amount AS AMOUNT, 
    Transaction_Type AS TRANSACTION_TYPE 
FROM transaction 
WHERE Transaction_Type = 'Debit' 
  AND (Amount > 10000 AND Amount < 50000);

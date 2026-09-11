# Generate Username and Password

## Problem Statement
Write a query to display the username and password of all customers. Give an alias name as `USERNAME` and `PASSWORD`. Sort the result based on the Username in ascending order.

Username and password are generated as below:
*   **USERNAME:** concatenate the customer name with customer id.
*   **PASSWORD:** concatenate first 3 characters of customer name with last 4 digits of customer phone.

**Table: customer**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| cust_id | varchar(10) | Primary Key. The ID of the customer. |
| cust_name | varchar(20) | The name of the customer. |
| cust_phone | bigint(20) | The phone number of the customer. |
| cust_address | varchar(20) | The address of the customer. |

---

## Solution

### Approach: String Manipulation Functions
To generate customized strings based on multiple table columns, we utilize built-in SQL string manipulation functions:
1. **Concatenation (`CONCAT`):** We use the `CONCAT()` function to join multiple strings together. For the `USERNAME`, it simply joins `cust_name` and `cust_id`.
2. **Substring Extraction (`LEFT` & `RIGHT`):** 
   - `LEFT(cust_name, 3)` extracts the first three characters from the left of the customer's name.
   - `RIGHT(cust_phone, 4)` extracts the last four digits from the phone number. Even though the phone number is stored as a numeric type (e.g., BIGINT), SQL implicitly casts it to a string for this operation.
3. **Aliasing & Sorting:** We alias the generated strings explicitly as `USERNAME` and `PASSWORD`. Finally, we sort the entire result set in ascending order by the generated `USERNAME` using `ORDER BY USERNAME ASC`.

### SQL Query
```sql
SELECT 
    CONCAT(cust_name, cust_id) AS USERNAME,
    CONCAT(LEFT(cust_name, 3), RIGHT(cust_phone, 4)) AS 'PASSWORD'
FROM customer
ORDER BY USERNAME ASC;

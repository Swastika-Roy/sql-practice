# Total Sale Day Wise

## Problem Statement
Write a query to display `order_date`, total order amount in each day. Give an alias name for total order amount as `TOTAL_SALE`. Sort the result based on `order_date`.

*NOTE: Maintain the same sequence of column order, as specified in the question description.*

**Database Schema Context:**
This query requires only the `orders` table from a larger food/hotel delivery schema.

**Table: orders**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| order_id | varchar(10) | Primary Key. The ID of the order. |
| customer_id | varchar(10) | Foreign Key pointing to customers. |
| hotel_id | varchar(10) | Foreign Key pointing to hotel_details. |
| partner_id | varchar(10) | Foreign Key pointing to delivery_partners. |
| order_date | date | The date when the order was placed. |
| order_amount | int | The total amount of the order. |

---

## Solution

### Approach: Grouping and Aggregation
To calculate the daily total revenue, we need to group the transaction records by their respective dates and then sum the order amounts.
1. **Aggregation:** We use the `SUM(order_amount)` aggregate function to calculate the total sales volume.
2. **Grouping:** The `GROUP BY order_date` clause ensures that the summation is done on a per-day basis rather than across the entire table.
3. **Aliasing:** We explicitly alias the aggregated sum as `TOTAL_SALE` to meet the exact string requirement of the evaluation engine.
4. **Sorting:** We use `ORDER BY order_date` to sort the final aggregated result chronologically.

### SQL Query
```sql
SELECT 
    order_date,
    SUM(order_amount) AS TOTAL_SALE
FROM orders
GROUP BY order_date
ORDER BY order_date;

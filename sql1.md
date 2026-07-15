# SQL Practice Challenges

---

## Challenge 1: Find Top Restaurants in Kolkata with High Average Order Amount

**Concepts Covered:** `INNER JOIN`, `GROUP BY`, `HAVING`, `Scalar Subquery`, `Aggregate Functions`.

### 1. Database Schema

#### **`restaurants` Table**
| Column Name | Data Type | Constraints |
| :--- | :--- | :--- |
| `id` | INT | PRIMARY KEY |
| `name` | VARCHAR(100) | |
| `city` | VARCHAR(50) | |
| `rating` | DECIMAL(3,1) | |

#### **`orders` Table**
| Column Name | Data Type | Constraints |
| :--- | :--- | :--- |
| `order_id` | INT | PRIMARY KEY |
| `restaurant_id` | INT | FOREIGN KEY references `restaurants(id)` |
| `order_date` | DATE | |
| `amount` | DECIMAL(10,2) | |
| `status` | VARCHAR(20) | Values: 'COMPLETED', 'CANCELLED', 'PENDING' |

---

### 2. The Problem Statement
Write a single SQL query to find the restaurants that meet **ALL** of the following conditions:
1. The restaurant must be located in the city of **'Kolkata'**.
2. The restaurant must have successfully served **at least 5** 'COMPLETED' orders.
3. The average order amount of 'COMPLETED' orders for that specific restaurant must be strictly greater than the **overall average order amount** of ALL 'COMPLETED' orders across the entire platform.

**Required Output Columns:** `restaurant_name`, `total_completed_orders`, `average_order_amount`

---

### 3. My Solution
```sql
SELECT 
    restaurants.name AS restaurant_name, 
    COUNT(orders.status) AS total_completed_orders, 
    AVG(orders.amount) AS average_order_amount 
FROM restaurants 
INNER JOIN orders ON restaurants.id = orders.restaurant_id 
WHERE restaurants.city = 'Kolkata' AND orders.status = 'COMPLETED'
GROUP BY restaurants.name, restaurants.city
HAVING COUNT(orders.status) >= 5 
   AND AVG(orders.amount) > (SELECT AVG(amount) FROM orders WHERE status = 'COMPLETED');
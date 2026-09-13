# 181. Employees Earning More Than Their Managers

**LeetCode:** https://leetcode.com/problems/employees-earning-more-than-their-managers/
**Difficulty:** Easy
**Category:** SQL / Self JOIN

## Problem

We have an `Employee` table containing information about employees and their managers.

Write a SQL query to find the employees who **earn more than their managers**.

Return the employee's `name` as `Employee`.

## Solution

```sql
SELECT
    e.name AS Employee
FROM Employee AS e
INNER JOIN Employee AS m
    ON e.managerId = m.id
WHERE e.salary > m.salary;
```

## Explanation

### 1. Why do we use the same table twice?

The `Employee` table contains information about both employees and managers.

For example:

| id | name  | salary | managerId |
| -: | ----- | -----: | --------: |
|  1 | Joe   |  70000 |         3 |
|  2 | Henry |  80000 |         4 |
|  3 | Sam   |  60000 |      NULL |
|  4 | Max   |  90000 |      NULL |

Here, Joe's manager is Sam because:

```text
Joe.managerId = 3
Sam.id = 3
```

So we need to compare the salary of an employee with the salary of their manager.

This is called a **Self JOIN** because we join the `Employee` table with itself.

### 2. Create two references to the table

```sql
FROM Employee AS e
INNER JOIN Employee AS m
```

Here:

* `e` represents the **employee**
* `m` represents the **manager**

Both references point to the same `Employee` table.

### 3. Match each employee with their manager

```sql
ON e.managerId = m.id
```

The employee's `managerId` points to the `id` of their manager.

For example:

```text
e.managerId = 3
m.id        = 3
```

Therefore, the employee and their manager are matched together.

### 4. Compare their salaries

```sql
WHERE e.salary > m.salary
```

We only want employees whose salary is greater than their manager's salary.

So:

```text
Employee salary > Manager salary
```

### 5. Return the employee's name

```sql
SELECT e.name AS Employee
```

The problem requires the output column to be named `Employee`, so we use:

```sql
AS Employee
```

## Why `INNER JOIN`?

We only need employees who have a manager because we cannot compare the salary of an employee with a manager who doesn't exist.

`INNER JOIN` automatically excludes employees whose `managerId` is `NULL` or doesn't match another employee.

## Key Concept

> **Self JOIN allows us to compare rows within the same table.**

In this problem:

```text
Employee table
      ↓
   Self JOIN
      ↓
Employee + Manager
      ↓
Compare salaries
      ↓
Employee salary > Manager salary
```

### Final Takeaway

When a table contains a relationship to itself, such as an employee having another employee as their manager, a **Self JOIN** is a useful way to compare the related rows.

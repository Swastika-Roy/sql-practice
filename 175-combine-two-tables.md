# 175. Combine Two Tables

**LeetCode:** https://leetcode.com/problems/combine-two-tables/
**Difficulty:** Easy
**Category:** SQL / JOIN

## Problem

We have two tables: `Person` and `Address`.

The `Person` table contains information about people, while the `Address` table contains their address information.

Write a SQL query to report:

* `firstName`
* `lastName`
* `city`
* `state`

for **every person**.

If a person does not have an address, their `city` and `state` should be `NULL`.

## Solution

```sql
SELECT
    p.firstName,
    p.lastName,
    a.city,
    a.state
FROM Person AS p
LEFT JOIN Address AS a
    ON p.personId = a.personId;
```

## Explanation

### 1. Start with the `Person` table

```sql
FROM Person AS p
```

We use `Person` as the left table because we need to include **every person** in the result.

### 2. Use `LEFT JOIN`

```sql
LEFT JOIN Address AS a
```

A `LEFT JOIN` keeps **all rows from the left table**, even when there is no matching row in the right table.

Therefore, if a person does not have an address, their `city` and `state` will be `NULL`.

### 3. Match the two tables

```sql
ON p.personId = a.personId
```

The two tables are connected using the `personId` column.

### 4. Select the required columns

```sql
SELECT
    p.firstName,
    p.lastName,
    a.city,
    a.state
```

We select the four columns required by the problem.

## Why `LEFT JOIN`?

We cannot use `INNER JOIN` because an `INNER JOIN` would remove people who do not have an address.

For example:

**Person**

| personId | firstName | lastName |
| -------: | --------- | -------- |
|        1 | Allen     | Wang     |
|        2 | Bob       | Alice    |

**Address**

| addressId | personId | city          | state    |
| --------: | -------: | ------------- | -------- |
|         1 |        1 | New York City | New York |

With `LEFT JOIN`, the result is:

| firstName | lastName | city          | state    |
| --------- | -------- | ------------- | -------- |
| Allen     | Wang     | New York City | New York |
| Bob       | Alice    | NULL          | NULL     |

Bob is still included because `Person` is the left table.

## Key Concept

> **LEFT JOIN keeps every row from the left table and adds matching data from the right table. If no match exists, the right-table columns become `NULL`.**

### Final Takeaway

Use a **`LEFT JOIN`** whenever the problem requires you to keep **all records from one table**, even when there is no corresponding record in another table.

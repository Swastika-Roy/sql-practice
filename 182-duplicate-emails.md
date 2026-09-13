# 182. Duplicate Emails

**LeetCode:** https://leetcode.com/problems/duplicate-emails/description/
**Difficulty:** Easy
**Category:** SQL / GROUP BY / HAVING

## Problem

We have a `Person` table containing the email address of each person.

Write a SQL query to report all **duplicate email addresses**.

An email is considered duplicate if it appears **more than once** in the table.

## Solution

```sql
SELECT
    email
FROM Person
GROUP BY email
HAVING COUNT(email) > 1;
```

## Explanation

### 1. Group rows by email

```sql
GROUP BY email
```

`GROUP BY` puts all rows having the same email address into one group.

For example:

| id | email                         |
| -: | ----------------------------- |
|  1 | [a@abc.com](mailto:a@abc.com) |
|  2 | [b@abc.com](mailto:b@abc.com) |
|  3 | [a@abc.com](mailto:a@abc.com) |

After grouping:

```text
a@abc.com → 2 rows
b@abc.com → 1 row
```

### 2. Count each email

```sql
COUNT(email)
```

This counts how many times each email appears in its group.

So we get:

| email                         | COUNT(email) |
| ----------------------------- | -----------: |
| [a@abc.com](mailto:a@abc.com) |            2 |
| [b@abc.com](mailto:b@abc.com) |            1 |

### 3. Keep only duplicates

```sql
HAVING COUNT(email) > 1
```

We only want emails that appear more than once.

Therefore:

```text
COUNT(email) > 1
```

means the email is duplicated.

## Why use `HAVING` instead of `WHERE`?

`WHERE` filters individual rows **before** grouping.

`HAVING` filters groups **after** `GROUP BY`.

Since we need to check the count of each email group, we use:

```sql
HAVING COUNT(email) > 1
```

## Query Flow

```text
Person table
     ↓
GROUP BY email
     ↓
Count occurrences of each email
     ↓
HAVING COUNT(email) > 1
     ↓
Return duplicate emails
```

## Key Concept

> **GROUP BY + HAVING** is commonly used to find duplicate values.

The general pattern is:

```sql
SELECT column
FROM table
GROUP BY column
HAVING COUNT(column) > 1;
```

### Final Takeaway

Whenever you need to find values that occur multiple times in a table, think:

**`GROUP BY` → `COUNT()` → `HAVING COUNT() > 1`**

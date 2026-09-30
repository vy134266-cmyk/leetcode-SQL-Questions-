# LeetCode 184 — Department Highest Salary

**Difficulty:** Medium
**Topic:** SQL
**Problem:** [Department Highest Salary](https://leetcode.com/problems/department-highest-salary/)

## 📌 Problem Description

Write a solution to find the employees who have the **highest salary in each department**.

For each department, return:

* Department name
* Employee name
* Employee salary

If multiple employees have the same highest salary in a department, return all of them.

## 🧠 SQL Concepts Used

* `JOIN`
* `GROUP BY`
* Aggregate Functions
* `MAX()`
* Subqueries
* Filtering

## 💡 Approach

1. Join the `Employee` table with the `Department` table using `departmentId`.
2. Find the maximum salary for each department.
3. Match each employee's salary with the maximum salary of their department.
4. Return all employees whose salary equals the department's maximum salary.

## 💻 SQL Solution

```sql
SELECT
    d.name AS Department,
    e.name AS Employee,
    e.salary AS Salary
FROM Employee e
JOIN Department d
    ON e.departmentId = d.id
JOIN (
    SELECT
        departmentId,
        MAX(salary) AS max_salary
    FROM Employee
    GROUP BY departmentId
) m
    ON e.departmentId = m.departmentId
    AND e.salary = m.max_salary;
```

## 🔍 Explanation

The subquery calculates the highest salary for every department:

```sql
SELECT
    departmentId,
    MAX(salary) AS max_salary
FROM Employee
GROUP BY departmentId;
```

Then, we join this result back to the `Employee` table and select employees whose salary matches the maximum salary of their department.

This approach also handles **ties**, meaning if two or more employees have the same highest salary in a department, all of them are returned.

## 📚 Key Learning

This problem is useful for understanding how to combine:

* Aggregation with `MAX()`
* `GROUP BY`
* Multiple `JOIN`s
* Subqueries
* Handling duplicate maximum values

## 🎯 Interview Relevance

This is a common SQL interview pattern for **Data Analyst, Data Engineer, and BI roles**.

### Related SQL Patterns

* Highest salary by department
* Second-highest salary
* Top N employees by department
* Ranking employees within departments
* `DENSE_RANK()` and `ROW_NUMBER()`
* Window functions

---

**LeetCode:** 184
**Difficulty:** Medium
**Language:** SQL
**Practice:** LeetCode SQL 50

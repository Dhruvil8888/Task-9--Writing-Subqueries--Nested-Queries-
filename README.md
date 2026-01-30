Task 9: Writing Subqueries (Nested Queries)

## 📌 Project Overview
This task demonstrates how to write and analyze **nested SQL queries (subqueries)**.  
It shows how subqueries work in `WHERE`, `FROM`, and `SELECT` clauses, and compares them with equivalent JOIN queries.

---

## 🛠 Tools Used
- **Primary:** MySQL Workbench  
- **Alternatives:** PostgreSQL, BigQuery Sandbox  

---

## 📂 Project Files
- `task9_subqueries.sql` → SQL script with subquery examples  
- `README.md` → Documentation (this file)

---

## 🎯 Learning Objectives
- Use subqueries in WHERE, FROM, and SELECT
- Write correlated subqueries
- Compare subqueries vs JOINs
- Debug subquery errors
- Understand query execution flow

---

## 🗄 Tables Used
- **employees** (with salary & department_id)

---

## 🧪 SQL Code Examples

### 1. Employees earning more than average salary
```sql
SELECT emp_name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary) FROM employees
);
2. Subquery in FROM clause
SELECT dept, avg_salary
FROM (
    SELECT department_id AS dept,
           AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) AS dept_avg;
3. Subquery in SELECT clause
SELECT 
    emp_name,
    salary,
    (SELECT AVG(salary) FROM employees) AS company_avg_salary
FROM employees;
4. Correlated subquery
(Above department average)

SELECT e.emp_name, e.salary, e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
5. Same logic using JOIN
SELECT e.emp_name, e.salary, d.avg_salary
FROM employees e
JOIN (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) d
ON e.department_id = d.department_id
WHERE e.salary > d.avg_salary;
6. Highest paid employee
SELECT emp_name, salary
FROM employees
WHERE salary = (
    SELECT MAX(salary) FROM employees
);
🔍 Key Concepts
Concept	Meaning
Subquery	A query inside another query
Correlated subquery	Depends on outer query row
WHERE subquery	Filters rows
FROM subquery	Creates derived tables
SELECT subquery	Adds computed values
⚡ Performance Notes
JOINs are often faster than correlated subqueries

Subqueries are useful when logic is complex

Avoid subqueries returning multiple rows in scalar contexts

▶ How to Run
Open MySQL Workbench

Select intern_training_db

Open task9_subqueries.sql

Run queries step-by-step

✅ Final Outcome
By completing this task, the intern:

Understands nested SQL logic

Can write complex subqueries

Knows when to use JOIN vs subquery

Is ready for analytical SQL challenges

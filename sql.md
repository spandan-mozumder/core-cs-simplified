# 📊 SQL — Interview Questions & Answers

> Top SQL interview questions with theoretical answers and query examples.
> Source: [Intellipaat — SQL Interview Questions](https://intellipaat.com/blog/interview-question/sql-interview-questions/)

---

## Basics

### Q1. What is SQL?

**SQL** (Structured Query Language) is the standard language for managing and querying relational databases.

### Q2. DDL, DML, DCL, TCL, DQL

| Category | Commands                      | Purpose       |
| -------- | ----------------------------- | ------------- |
| **DDL**  | CREATE, ALTER, DROP, TRUNCATE | Define schema |
| **DML**  | INSERT, UPDATE, DELETE        | Modify data   |
| **DQL**  | SELECT                        | Query data    |
| **DCL**  | GRANT, REVOKE                 | Permissions   |
| **TCL**  | COMMIT, ROLLBACK, SAVEPOINT   | Transactions  |

### Q3. Primary Key vs Unique Key

| Feature   | Primary Key | Unique Key    |
| --------- | ----------- | ------------- |
| NULLs     | Not allowed | One NULL      |
| Per table | Only one    | Multiple      |
| Index     | Clustered   | Non-clustered |

---

### Q4. DROP vs DELETE vs TRUNCATE

```sql
-- DELETE: Removes specific rows, can rollback, fires triggers
DELETE FROM employees WHERE department = 'Sales';

-- TRUNCATE: Removes ALL rows, faster, cannot rollback (DDL)
TRUNCATE TABLE temp_data;

-- DROP: Removes the entire table structure + data
DROP TABLE old_records;
```

---

### Q5. WHERE vs HAVING

```sql
-- WHERE filters rows BEFORE grouping
SELECT department, COUNT(*) FROM employees
WHERE salary > 50000
GROUP BY department;

-- HAVING filters groups AFTER grouping
SELECT department, AVG(salary) as avg_sal FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

### Q6. Types of JOINs

```sql
-- INNER JOIN: Only matching rows
SELECT e.name, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;

-- LEFT JOIN: All left + matching right (NULL if no match)
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;

-- RIGHT JOIN: All right + matching left
SELECT e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.id;

-- FULL OUTER JOIN: All rows from both tables
SELECT e.name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.id;

-- CROSS JOIN: Cartesian product (every combination)
SELECT e.name, d.dept_name
FROM employees e
CROSS JOIN departments d;

-- SELF JOIN: Table joined with itself
SELECT e1.name AS employee, e2.name AS manager
FROM employees e1
INNER JOIN employees e2 ON e1.manager_id = e2.id;
```

---

### Q7. UNION vs UNION ALL

```sql
-- UNION: Combines results, removes duplicates
SELECT name FROM customers
UNION
SELECT name FROM suppliers;

-- UNION ALL: Combines results, keeps duplicates (faster)
SELECT name FROM customers
UNION ALL
SELECT name FROM suppliers;
```

---

### Q8. Aggregate Functions

```sql
SELECT
    department,
    COUNT(*) AS total_employees,
    AVG(salary) AS avg_salary,
    SUM(salary) AS total_salary,
    MAX(salary) AS highest_salary,
    MIN(salary) AS lowest_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC;
```

---

### Q9. Subqueries

```sql
-- Scalar subquery
SELECT name, salary FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);

-- Correlated subquery (references outer query)
SELECT e.name, e.salary, e.department
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary) FROM employees e2
    WHERE e2.department = e.department
);

-- EXISTS
SELECT name FROM departments d
WHERE EXISTS (
    SELECT 1 FROM employees e WHERE e.dept_id = d.id
);
```

---

### Q10. Window Functions (RANK, DENSE_RANK, ROW_NUMBER)

```sql
SELECT
    name,
    department,
    salary,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS row_num,
    RANK()       OVER (PARTITION BY department ORDER BY salary DESC) AS rank,
    DENSE_RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dense_rank
FROM employees;

-- ROW_NUMBER: 1, 2, 3, 4 (always unique)
-- RANK:       1, 2, 2, 4 (skips after tie)
-- DENSE_RANK: 1, 2, 2, 3 (no skip after tie)
```

---

### Q11. Find Nth Highest Salary

```sql
-- Method 1: Subquery
SELECT DISTINCT salary FROM employees e1
WHERE N-1 = (SELECT COUNT(DISTINCT salary) FROM employees e2 WHERE e2.salary > e1.salary);

-- Method 2: DENSE_RANK
SELECT salary FROM (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rank
    FROM employees
) ranked
WHERE rank = 3; -- 3rd highest

-- Method 3: LIMIT/OFFSET
SELECT DISTINCT salary FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 2; -- 3rd highest
```

---

### Q12. Find Duplicate Rows

```sql
-- Find duplicates
SELECT name, email, COUNT(*) AS count
FROM employees
GROUP BY name, email
HAVING COUNT(*) > 1;

-- Delete duplicates (keep one)
DELETE FROM employees
WHERE id NOT IN (
    SELECT MIN(id) FROM employees GROUP BY name, email
);
```

---

### Q13. Views & Materialized Views

```sql
-- View (virtual table — computed on every query)
CREATE VIEW high_earners AS
SELECT name, salary, department FROM employees WHERE salary > 80000;

SELECT * FROM high_earners;

-- Materialized View (stored result — refreshed periodically)
CREATE MATERIALIZED VIEW monthly_sales AS
SELECT product_id, SUM(amount) as total
FROM sales
GROUP BY product_id;

REFRESH MATERIALIZED VIEW monthly_sales;
```

---

### Q14. Indexes

```sql
-- Create index
CREATE INDEX idx_emp_name ON employees(name);

-- Composite index
CREATE INDEX idx_dept_salary ON employees(department, salary);

-- Unique index
CREATE UNIQUE INDEX idx_email ON employees(email);

-- Check existing indexes
SHOW INDEX FROM employees;

-- Drop index
DROP INDEX idx_emp_name ON employees;
```

---

### Q15. Common Table Expressions (CTE)

```sql
-- Basic CTE
WITH dept_stats AS (
    SELECT department, AVG(salary) as avg_sal, COUNT(*) as emp_count
    FROM employees
    GROUP BY department
)
SELECT * FROM dept_stats WHERE avg_sal > 60000;

-- Recursive CTE (org hierarchy)
WITH RECURSIVE org_chart AS (
    SELECT id, name, manager_id, 1 as level
    FROM employees WHERE manager_id IS NULL
    UNION ALL
    SELECT e.id, e.name, e.manager_id, oc.level + 1
    FROM employees e
    INNER JOIN org_chart oc ON e.manager_id = oc.id
)
SELECT * FROM org_chart ORDER BY level;
```

---

### Q16. Normalization

| Form    | Rule                       | Example Fix                                       |
| ------- | -------------------------- | ------------------------------------------------- |
| **1NF** | Atomic values only         | Split multi-valued columns                        |
| **2NF** | No partial dependencies    | Remove columns dependent on part of composite key |
| **3NF** | No transitive dependencies | Remove A→B→C chains                               |

---

### Q17. ACID Properties

| Property        | Description                             |
| --------------- | --------------------------------------- |
| **Atomicity**   | All or nothing                          |
| **Consistency** | Valid state before and after            |
| **Isolation**   | Concurrent transactions don't interfere |
| **Durability**  | Committed = permanent                   |

```sql
BEGIN TRANSACTION;
    UPDATE accounts SET balance = balance - 500 WHERE id = 1;
    UPDATE accounts SET balance = balance + 500 WHERE id = 2;
COMMIT; -- Both succeed or both fail
```

---

### Q18. Stored Procedures & Triggers

```sql
-- Stored Procedure
DELIMITER //
CREATE PROCEDURE GetEmployeesByDept(IN dept_name VARCHAR(50))
BEGIN
    SELECT * FROM employees WHERE department = dept_name;
END //
DELIMITER ;

CALL GetEmployeesByDept('Engineering');

-- Trigger
CREATE TRIGGER before_salary_update
BEFORE UPDATE ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary < 0 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Salary cannot be negative';
    END IF;
END;
```

---

### Q19. CASE Statement

```sql
SELECT name, salary,
    CASE
        WHEN salary >= 100000 THEN 'Senior'
        WHEN salary >= 60000 THEN 'Mid'
        WHEN salary >= 30000 THEN 'Junior'
        ELSE 'Intern'
    END AS level
FROM employees;
```

---

### Q20. Query Execution Order

```
FROM → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT
```

---

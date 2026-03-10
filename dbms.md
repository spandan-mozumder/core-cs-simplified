# 🗄️ DBMS — Interview Questions & Answers

> A comprehensive quick-reference guide covering the most frequently asked DBMS questions in product-based company interviews.

---

## 1. Introduction to DBMS

### Q1. Data, Database, and File System

| Concept         | Definition                                                 |
| --------------- | ---------------------------------------------------------- |
| **Data**        | Raw facts and figures (numbers, text, images)              |
| **Database**    | Organized collection of related data stored electronically |
| **File System** | OS-level file storage without relationships or constraints |

**Why DBMS over File System?**

- ✅ Reduces data redundancy
- ✅ Enforces data integrity & constraints
- ✅ Supports concurrent access
- ✅ Provides backup & recovery
- ✅ Supports complex queries (SQL)

---

### Q2. Types of Database

| Type                   | Description                                 | Example                   |
| ---------------------- | ------------------------------------------- | ------------------------- |
| **Relational (RDBMS)** | Tables with rows & columns; uses SQL        | MySQL, PostgreSQL, Oracle |
| **NoSQL**              | Flexible schema; handles unstructured data  | MongoDB, Cassandra, Redis |
| **Hierarchical**       | Tree-like structure (parent-child)          | IBM IMS                   |
| **Network**            | Graph structure; many-to-many relationships | IDMS                      |
| **Object-Oriented**    | Stores objects (like OOP)                   | db4o                      |
| **Graph**              | Nodes and edges; for relationships          | Neo4j                     |

---

### Q3. What is DBMS and its Applications?

A **Database Management System (DBMS)** is software that manages databases — providing interfaces for creating, reading, updating, and deleting data (CRUD).

**Applications:**

- Banking (transactions, accounts)
- Airlines (reservations, schedules)
- E-commerce (products, orders)
- Telecom (billing, call records)
- Social Media (user data, posts)

**Popular DBMS:** MySQL, PostgreSQL, Oracle, SQL Server, MongoDB

---

### Q4. Data Abstraction

**Data abstraction** hides the complexity of the database from users through **3 levels:**

| Level        | What it Shows                       | Who Uses It        |
| ------------ | ----------------------------------- | ------------------ |
| **Physical** | How data is stored on disk          | Database admin     |
| **Logical**  | What data is stored & relationships | Database designers |
| **View**     | Partial view of the database        | End users          |

---

### Q5. 3-Tier Architecture

```
[User/Client] → [Application Server] → [Database Server]
   (Tier 1)          (Tier 2)              (Tier 3)
   UI/View         Business Logic        Data Storage
```

**Benefits:** Separation of concerns, scalability, security, easier maintenance.

---

## 2. Data Models

### Q6. Data Models and Their Types

A **data model** defines how data is structured, stored, and manipulated.

| Model                   | Structure            | Example           |
| ----------------------- | -------------------- | ----------------- |
| **Relational**          | Tables (relations)   | SQL databases     |
| **Hierarchical**        | Tree structure       | File systems      |
| **Network**             | Graph structure      | CODASYL           |
| **Entity-Relationship** | ER diagrams          | Conceptual design |
| **Object-Oriented**     | Objects with methods | db4o              |

---

### Q7. ER Model — Entity, Attributes & Relationships

**Entity:** A real-world object (e.g., Student, Employee)

- **Strong Entity:** Has its own primary key
- **Weak Entity:** Depends on another entity for identification

**Attributes:**
| Type | Description | Example |
|------|-------------|---------|
| **Simple** | Atomic, indivisible | Name |
| **Composite** | Divisible into sub-parts | Address → Street, City, ZIP |
| **Derived** | Computed from other attributes | Age (from DOB) |
| **Multi-valued** | Multiple values | Phone numbers |
| **Key** | Uniquely identifies entity | Roll Number |

**Relationships:** Association between entities

- **One-to-One (1:1):** Person ↔ Passport
- **One-to-Many (1:N):** Department ↔ Employees
- **Many-to-Many (M:N):** Students ↔ Courses

---

### Q8. Entity-Relationship Diagrams (ERD)

**ERD** is a visual representation of entities, attributes, and relationships.

**Symbols:**

- **Rectangle:** Entity
- **Ellipse:** Attribute
- **Diamond:** Relationship
- **Double Rectangle:** Weak Entity
- **Double Ellipse:** Multi-valued Attribute
- **Lines:** Connect entities to attributes and relationships

**Cardinality** specifies the number of instances of one entity related to another (1:1, 1:N, M:N).

---

### Q9. Relational Model

Represents data as **tables (relations)** with rows (**tuples**) and columns (**attributes**).

**Key Terms:**
| Term | Meaning |
|------|---------|
| **Relation** | Table |
| **Tuple** | Row (a single record) |
| **Attribute** | Column (a field) |
| **Domain** | Set of allowed values for an attribute |
| **Degree** | Number of columns |
| **Cardinality** | Number of rows |
| **Schema** | Structure of the table |

---

## 3. RDBMS

### Q10. What is RDBMS?

A **Relational Database Management System** stores data in tables with predefined relationships. Based on **E.F. Codd's relational model** (1970).

**Properties:**

- Data stored in tables with rows and columns
- Tables related through foreign keys
- Uses SQL for data manipulation
- Enforces ACID properties

---

### Q11. Essential Components of a Table

| Component              | Description                              |
| ---------------------- | ---------------------------------------- |
| **Row (Tuple)**        | A single record                          |
| **Column (Attribute)** | A field/property                         |
| **Primary Key**        | Uniquely identifies each row             |
| **Foreign Key**        | References primary key of another table  |
| **Schema**             | Table structure (column names, types)    |
| **Constraints**        | Rules (NOT NULL, UNIQUE, CHECK, DEFAULT) |

---

### Q12. Intension and Extension in a Database

| Concept                  | Description                                                                                        |
| ------------------------ | -------------------------------------------------------------------------------------------------- |
| **Intension (Schema)**   | The structure/definition of the table — column names, data types, constraints. **Rarely changes.** |
| **Extension (Instance)** | The actual data/rows in the table at any point in time. **Changes frequently.**                    |

---

### Q13. Keys

| Key               | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| **Primary Key**   | Uniquely identifies each record; NOT NULL, UNIQUE            |
| **Candidate Key** | All possible columns that can be a primary key               |
| **Super Key**     | Any combination of columns that uniquely identifies a record |
| **Foreign Key**   | References the primary key of another table                  |
| **Composite Key** | Primary key made of 2+ columns                               |
| **Alternate Key** | Candidate keys not chosen as primary key                     |
| **Unique Key**    | Like primary key but allows one NULL                         |

---

### Q14. Normalization and its Types (1NF, 2NF, 3NF)

**Normalization** is the process of organizing data to **reduce redundancy and dependency**.

| Normal Form | Rule                                    | Eliminates              |
| ----------- | --------------------------------------- | ----------------------- |
| **1NF**     | Atomic values only; no repeating groups | Multi-valued attributes |
| **2NF**     | 1NF + no partial dependencies           | Partial dependency      |
| **3NF**     | 2NF + no transitive dependencies        | Transitive dependency   |
| **BCNF**    | Every determinant is a candidate key    | Remaining anomalies     |

**Dependency Types:**

- **Partial Dependency:** Non-key attribute depends on PART of the composite key
- **Transitive Dependency:** A → B → C (C depends on A through B)

---

### Q15. Denormalization

**Denormalization** is the intentional introduction of redundancy to **improve read performance**.

| Normalization      | Denormalization         |
| ------------------ | ----------------------- |
| Reduces redundancy | Adds redundancy         |
| More joins needed  | Fewer joins             |
| Slower reads       | Faster reads            |
| Better for writes  | Better for reads        |
| Used for OLTP      | Used for OLAP/analytics |

---

## 4. SQL

### Q16. SQL Commands and Types

| Category                      | Commands                      | Purpose              |
| ----------------------------- | ----------------------------- | -------------------- |
| **DDL** (Data Definition)     | CREATE, ALTER, DROP, TRUNCATE | Define/modify schema |
| **DML** (Data Manipulation)   | INSERT, UPDATE, DELETE        | Modify data          |
| **DQL** (Data Query)          | SELECT                        | Retrieve data        |
| **DCL** (Data Control)        | GRANT, REVOKE                 | Manage permissions   |
| **TCL** (Transaction Control) | COMMIT, ROLLBACK, SAVEPOINT   | Manage transactions  |

**Key Difference:** `DELETE` removes rows (can rollback) vs `TRUNCATE` removes all rows (faster, no rollback).

---

### Q17. Operators and Aggregation in SQL

**Operators:**

- **Arithmetic:** `+`, `-`, `*`, `/`
- **Comparison:** `=`, `!=`, `<`, `>`, `<=`, `>=`
- **Logical:** `AND`, `OR`, `NOT`, `IN`, `BETWEEN`, `LIKE`

**Aggregate Functions:**
| Function | Purpose |
|----------|---------|
| `COUNT()` | Number of rows |
| `SUM()` | Total of column values |
| `AVG()` | Average value |
| `MIN()` | Minimum value |
| `MAX()` | Maximum value |

Used with `GROUP BY` and filtered with `HAVING`.

---

### Q18. SQL Sub Queries

A **subquery** is a query nested inside another query.

**Types:**

- **Scalar:** Returns a single value
- **Row:** Returns a single row
- **Table:** Returns a table (used with `IN`, `EXISTS`)
- **Correlated:** References the outer query (runs once per row)

```sql
-- Find employees earning more than average
SELECT name FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

---

## 5. Transactions and Concurrency Control

### Q19. Schedule (Serial, Parallel)

| Type         | Description                            | Performance | Consistency       |
| ------------ | -------------------------------------- | ----------- | ----------------- |
| **Serial**   | Transactions execute one after another | Slow        | Always consistent |
| **Parallel** | Transactions execute concurrently      | Fast        | May cause issues  |

**ACID Properties of Transactions:**

- **Atomicity:** All or nothing
- **Consistency:** DB remains valid before and after
- **Isolation:** Transactions don't interfere with each other
- **Durability:** Committed changes are permanent

---

### Q20. Isolation Levels and Types

| Level                | Dirty Read | Non-Repeatable Read | Phantom Read | Performance |
| -------------------- | ---------- | ------------------- | ------------ | ----------- |
| **Read Uncommitted** | ✅ Yes     | ✅ Yes              | ✅ Yes       | Fastest     |
| **Read Committed**   | ❌ No      | ✅ Yes              | ✅ Yes       | Fast        |
| **Repeatable Read**  | ❌ No      | ❌ No               | ✅ Yes       | Moderate    |
| **Serializable**     | ❌ No      | ❌ No               | ❌ No        | Slowest     |

**Problems:**

- **Dirty Read:** Reading uncommitted data from another transaction
- **Non-Repeatable Read:** Same query returns different data (row updated)
- **Phantom Read:** Same query returns different rows (rows added/deleted)

---

### Q21. Serializability and Concurrency Control

A parallel schedule is **serializable** if it produces the same result as some serial schedule.

**Types:**

- **Conflict Serializability:** Checked via precedence graph (cycle = not serializable)
- **View Serializability:** More permissive check

**Concurrency Control Techniques:**

- Lock-based protocols
- Timestamp-based protocols
- Optimistic concurrency control

---

### Q22. Locking Protocols

| Lock Type              | Description                                      |
| ---------------------- | ------------------------------------------------ |
| **Shared Lock (S)**    | Multiple transactions can read; no one can write |
| **Exclusive Lock (X)** | Only one transaction can read AND write          |

**Two-Phase Locking (2PL):**

1. **Growing Phase:** Acquire locks (no releasing)
2. **Shrinking Phase:** Release locks (no acquiring)

**Deadlock:** Two transactions waiting for each other's locks → neither can proceed.
**Solutions:** Timeout, wait-die, wound-wait, deadlock detection (wait-for graph).

---

## 6. Query Optimization

### Q23. Techniques for Optimizing SQL Queries

- Use **indexes** on frequently queried columns
- Avoid `SELECT *` — select only needed columns
- Use **JOINs** instead of subqueries when possible
- Use `EXISTS` instead of `IN` for large datasets
- Avoid functions on indexed columns in `WHERE` clause
- Use **query execution plans** (`EXPLAIN`) to analyze performance
- **Partition** large tables
- Use **connection pooling**

---

### Q24. Indexing and its Types

An **index** is a data structure that speeds up data retrieval (like a book's index).

| Type                    | Description                                              |
| ----------------------- | -------------------------------------------------------- |
| **Primary Index**       | On the primary key; ordered                              |
| **Secondary Index**     | On non-key columns                                       |
| **Clustered Index**     | Physically reorders the table (one per table)            |
| **Non-Clustered Index** | Separate structure pointing to data (multiple per table) |
| **Dense Index**         | Entry for every record                                   |
| **Sparse Index**        | Entry for every block/page                               |
| **Composite Index**     | Index on multiple columns                                |

**Trade-off:** Faster reads ↔ Slower writes (index must be updated)

---

### Q25. B and B+ Trees

| Feature       | B-Tree               | B+ Tree                        |
| ------------- | -------------------- | ------------------------------ |
| Data storage  | In all nodes         | Only in leaf nodes             |
| Leaf linkage  | Not linked           | Linked (sequential access)     |
| Search        | May end at any level | Always goes to leaf            |
| Range queries | Slower               | Faster (linked leaves)         |
| Used in       | General indexing     | Database indexes (most common) |

**B+ Tree Properties:**

- Balanced tree (all leaves at same level)
- Each node can have multiple keys
- Leaf nodes form a linked list → excellent for range queries

---

## 7. Scalability and Performance Optimization

### Q26. Vertical and Horizontal Scaling

| Feature    | Vertical Scaling (Scale Up)         | Horizontal Scaling (Scale Out) |
| ---------- | ----------------------------------- | ------------------------------ |
| How        | Add more CPU/RAM to existing server | Add more servers               |
| Limit      | Hardware limits                     | Theoretically unlimited        |
| Cost       | Expensive at scale                  | Cost-effective                 |
| Downtime   | May need restart                    | No downtime                    |
| Complexity | Simple                              | Complex (distributed systems)  |
| Example    | Upgrading server RAM                | Adding more database replicas  |

---

### Q27. Sharding

**Sharding** = splitting a database into smaller pieces (**shards**) distributed across multiple servers.

**Strategies:**

- **Range-based:** Shard by data range (e.g., users A-M, N-Z)
- **Hash-based:** Shard by hash of a key (even distribution)
- **Directory-based:** Lookup table maps data to shards

**Benefits:** Improved performance, horizontal scalability, fault isolation
**Challenges:** Complex queries across shards, rebalancing, consistency

---

## 8. Data Integrity and Security

### Q28. RBAC (Role-Based Access Control)

**RBAC** restricts access based on **roles** assigned to users.

```
User → Role → Permissions
```

| Component      | Example               |
| -------------- | --------------------- |
| **User**       | john_doe              |
| **Role**       | Admin, Editor, Viewer |
| **Permission** | READ, WRITE, DELETE   |

**Benefits:** Easier management, principle of least privilege, auditing.

```sql
GRANT SELECT, INSERT ON employees TO manager_role;
REVOKE DELETE ON employees FROM intern_role;
```

---

### Q29. Encryption

| Type                                  | Description                        | Use Case                |
| ------------------------------------- | ---------------------------------- | ----------------------- |
| **At Rest**                           | Encrypts stored data               | Database files, backups |
| **In Transit**                        | Encrypts data moving over network  | SSL/TLS connections     |
| **Column-level**                      | Encrypt specific sensitive columns | Credit cards, SSNs      |
| **Transparent Data Encryption (TDE)** | Encrypts entire database files     | Enterprise databases    |

**Techniques:** AES-256, RSA, hashing (bcrypt for passwords)

---

> 📖 **Source:** [TakeUForward — Most Asked DBMS Interview Questions](https://takeuforward.org/dbms/most-asked-dbms-interview-questions)

## Week 1/2


## MS Access Objects

- Tables
- Forms
- Queries - SQL Select Stmt
- Reports
- Macros - VB Programming (not focused on in course)


# Week 2: MS SQL SERVER
---

## MS SQL Server - Overview & Features

- Relational Database Management System (RDBMS) by Microsoft
- Handles **large-scale enterprise databases.**
- Provides **Security features:** clustering, replication, backups.
- Integrates with **BI tools:** SSRS, SSIS, SSAS.
- Supports **on-premises and cloud (Azure SQL Database)** deployments.


## SQL Server Management Studio (SSMS)

- **Free Microsoft tool** for managing SQL Server databases.
- Offers **Graphical User Interface (GUI)** and **Query Editor.**
- Allows creation of **databases, tables, views, and stored procedures.**
- Enables **backups, restores, and security management.**
- Object Explorer helps navigate **tables, views, procedures, and users.**
- Ideal for students to **practice queries and database management.**


## ANSI SQL vs T-SQL

**ANSI SQL**
- Standardized across RDBMS: Oracle, MySQL, PostgreSQL, SQL Server.
- Basic wuery operations: SELECT, INSERT, UPDATE, DELETE, JOIN.
- Ensures **portability** across database systems.


**T-SQL (Transact-SQL)**
- Microsoft's **extension of ANSI SQL.**
- Adds **procedural programming, system functions, error handling.**
- Used exlusively in **MS SQL Server.**


## Short Summary
<img width="483" height="388" alt="2025-09-16_15h39_11" src="https://github.com/user-attachments/assets/5f4308aa-4641-4036-8e18-764be0f26c00" />


## Security Features

## MS SQL Server - Security Features
- SQL Server security is authentication + authorization
- Authentication -> verifies who can connect (logins).
- Authorization -> controls what actions they can perform (users, roles, permissions).


### Security Features - LOGINS
- A login is required to connect to SQL Server (server-level security).
- Types of logins:
  - Windows logins (integrated with Active Directory).
  - SQL Server logins (username + password).
- Defines server-wide access but not directly to databases.


### Security Features - DATABASE USERS
- A user is created inside a database and mapped to a login
- Allows login to access specific databases
- One login can be mapped to multiple users accross different databases.
- Example Using SQL's Datab Control Langauge (DCL):
  - `CREATE USER JohnUser FOR LOGIN JohnLogin;`


### Security Features - PERMISSIONS
- Define what actions users/roles can perform.
- Levels:
  - Server-level -> CREATE DATABASE, ALTER ANY LOGIN.
  - Database-level -> SELECT, INSERT, UPDATE, DELETE, EXECUTE.
  - Object-level -> permissions on specific tables, views, or stored procedures.
- Example (SQL's DCL):
  - `GRANT SELECT, INSERT ON Employees TO JohnUser;`


### Security Features - DATABASE ROLES
- Roles group permissions for easier management.
- Types:
  - Server Roles -> control server-wide tasks (e.g., sysadmin, securityadmin).
  - Database Roles -> control database-specific tasks (e.g., db_owner, db_datareader, db_datawriter).
- Custom roles can also be created for flexibility.


### Default Login & DB User
- When you use Windows Authentication, your Windows account (e.g., DOMAIN\Username) becomes the LOGIN at the SQL Server instance level.
- This login already exists if your Windows account as Admin
- When you create a new database, SQL Server automatically creates a database user in that database mapped to your login.


### Checking Current LOGIN & DB USER
<img width="724" height="339" alt="2025-09-16_16h39_40" src="https://github.com/user-attachments/assets/45cb5466-7d8d-4f79-b11e-050950c35080" />


### Security Features - Best Practices
- Use Windows Authentication where possible (more secure).
- Follow principle of least privilege (grant minimum permissions).
- Prefer roles over individual permissions (easier to manage).
- Regularly review and audit login/user permissions.


### Security Features - Quick Summary
- Login = Who can enter the server
- User = Who can enter the database
- Roles/Permissions = What they can do inside


## Advance SQL - 1

## MS SQL Server: EXISTS Operator
- EXISTS checks whether a subquery returns any rows (TRUE/FALSE).
- Used in WHERE or IF conditions
- Evaluates row existence, not values. Returns True if rows exist
- Efficient for checking data presence
<img width="684" height="157" alt="2025-09-16_18h16_54" src="https://github.com/user-attachments/assets/a9cc6590-acec-4527-9736-25ff9a940d5d" />


## MS SQL Server: IIF Function
- Introduced in SQL Server 20212
- Simplified inline conditional expression (like IF...ELSE in one line)
- Returns one value if condition is TRUE, another if FALSE
- Syntax: IIF(condition, true_value, flase_value)
- Example:
  - `SELECT Name, IIF(Salary > 50000, 'High', 'Low') AS SalaryCategory FROM Employees;`


## MS SQL Server: CASE Statement
- More flexible than IIF - can handle multiple conditions.
- Works in SELECT, WHERE, ORDER BY clauses
- Two forms: Simple CASE and Searched CASE
- CASE is ANSI standard SQL, more portable | IIF is T-SQL specific.
**CASE**
  WHEN condition1 THEN result1
  WHEN condition2 THEN result2
  ELSE default_result
**END**


## ROLLUP
- An extension of GROUP BY that creates subtotals and a grand total.
- Automatically rolls up data to higher-level summaries
- Example:
  - `SELECT Department, SUM(Salary)
   FROM Employees
   GROUP BY ROLLUP(Department);`


## CUBE
- Like ROLLUP but generates all possible combinations of groupings.
- Useful for multi-dimensional analysis (e.g., sales by region, product, year)
- Example:
  - `SELECT REGION, Product, SUM(Sales)
   FROM Orders
   GROUP BY CUBE (Region, Product);`


## Single Row Sub-Query
- Subquery that returns only one row
- Can be used with operators like =, <, >
- Example:
  - `SELECT *
    FROM Employees
    WHERE Salary > (SELECT AVG(Salary) FROM Employees);`


## Multi-Row Sub Query
- Subquery that returns multiple rows
- Used with operators like IN, ANY, ALL
- Example:
  - `SELECT *
    FROM Employees
    WHERE DepartmentID IN (SELECT DepartmentID FROM Departments WHERE Location = 'Ottawa');`


## Co-Related Sub Query
- Subquery that depends on values from the outer query
- Executed once for each row of the outer query
- Example:
  - `SELECT Name, Salary
    FROM Employees e
    WHERE Salary > (SELECT AVG(Salary) FROM Employees
    WHERE DepartmentID = e.DepartmentID);`


## Quick Summary - Advance SQL - 1
- **EXISTS** -> Presence check
- **IIF** -> Quick yes/no
- **CASE** -> Multiple outcomes
- **ROLLUP** -> totals by hierarchy
- **CUBE** -> totals by all combinations
- **Single-row subquery** -> returns a set of values
- **Correlated subquery** -> inner query depends on outer query row


# Week 3: MS SQL SERVER
---

## **MS SQL Server: Indexes**

## Indexes in MS SQL Server
- An index is an on-disk structure associated with a table or view that speeds retrieval of rows from the table or view
- An index contains keys built from one or more columns in the table or view
- These keys are stored in a structure (B-tree) that enables SQL Server to find the row or rows associated with the key values quickly and efficiently


## What is an Index?
- Index is a database object that improves query performance
- Works like a table of contents in a book
- Key Points:
  - Speeds up data retrieval
  - Reduces disk I/O
  - References table data without storing full data serparately


## Should you use an Index all the time?
- No, indexes are better for select statements, improves table scan, and join operations etc. However requires more storage, slows certain commands (INSERT, UPDATE, DELETE) Maintenance overhead if too many indexes are declared.


## Types of Indexes in SQL Server:
- Clustered Index: Physical order, one per table, often primary key
- Non-Clustered Index: Seperate structure, multiple per table, pointers to rows
- Unique Index: Ensures uniqueness of column values
- Full-Text Index: Optimized for text search


## Clustered vs Non-Clustered Indexes
- A **clustered** index determines the physical order of the data in the table
- The table itself is stored in the order of the clustered index
- Often, the clustered index is created on the primary key, but it doesn't have to be.
- A **non-clustered** index is stored separately from the actual table data
- It contains: The indexed column(s) * A pointer (row locator) to the actual data row in the table.
- Think of it as: A separate lookup table that points to the main table, like an index in the back of a book.


## Index Creation
- SQL Server __automatically__ creates indexes when PRIMARY KEY and UNIQUE constraints are defined on table columns
  - PRIMARY KEY -> CLUSTERED UNIQUE INDEX
  - UNIQUE KEY -> NON-CLUSTERED UNIQUE INDEX
- Indexes can also be created manually by using the 'CREATE INDEX' statement.

**Clustered:** `SQL> CREATE CLUSTERED INDEX IDX_EmpID ON Employee(EmpID);`
- Note: Only 1 clustered index per table allowed.

**Non-Clustered:** `SQL> CREATE NONCLUSTERED INDEX IDX_Job ON Employee(Job);`

**Drop Index:** `SQL> DROP INDEX IDX_Job ON Employee;`


## Advantages & Disadvantages of Indexes

**Advantages:**
- Faster SELECT queries
- Reduces table scans
- Improves JOIN operations
- Helps ORDER BY and GROUP BY clauses

**Disadvantages:**
- Requires storage space
- Slows INSERT, UPDATE, DELETE
- Maintenance overhead if too many indexes
- Balance read vs write performance


## Viewing Indexes
- Using system views / Meta Data: `SQL> SELECT name, type_desc FROM sys.indexes WHERE object_id = OBJECT_ID('emp')`
`OR object_id = OBJECT_ID('dept');`
- SSMS Object Explorer: Expand table -> Indexes


## Index Maintenance
- Rebuild Index: Recreates the index, updates statistics
- Reorganize Index: Defragments leaf level, online operation

- Example:
`ALTER INDEX IDX_DeptID ON Employee REBUILD;`
`ALTER INDEX IDX_DeptID ON Employee REORGANIZE;`
- Regular maintenance improves performance on large tables


## Indexes Best Pratices
- Index primary and foreign keys
- Avoid too many indexes on write-heavy tables
- Create Index on column only if its frequently used in WHERE clause
- Monitor index usage and fragmentation
- Balance query performance and storage overhead


## **MS SQL Server: Query Optimizer & Execution Plans**

## Query Optimizer
- SQL Server component that determines the most effcient way to execute a query
- Considers: Available indexes, statistics, join methods, and query structure
- Generates multiple execution strategies and selects the lowest-cost plan.


**NOTE: Anything good for DML slows down select statement, same is true vice versa.**


## What is an Execution Plan?
- An Execution Plan is a detailed roadmap showing how a query will be executed, including the sequence of operations, data access methods, and cost estimates.
- Shows the steps SQL Server will take to retrieve or modify data
- Includes operators like scans, seeks, joins, sorts, and aggregations
- Provides estimated and actual row counts
- Helps identify performance bottlenecks and opportunities for optimization.


## Types of Execution Plans
1. Estimated Execution Plan
   - Generated before query execution
   - Shows predicted operations and costs
   - SSMS Shortcut: **Ctrl + L**
2. Actual Execution Plan
   - Generated after query execution
   - Includes runtime statistics (rows processed, CPU/IO cost)
   - SSMS Shortcut: **Ctrl + M**


## Tips & Best Practices
- Prefer Index Seek over Scan for large tables
- Use filtered indexes for selective queries
- Check warnings (missing indexes, spills to tempdb)
- Compare estimated vs actual plans for real-world performance


## Class Exercise - Indexes
1. Create a new Database named "HR" & Open NEW QUERY on HR database
2. Run the SQL script provided under CONTENT -> WEEK 2 -> HR SQL Script. This script creates dept, emp tables.
3. View indexes on Dept, Emp table (slide 11 - "Viewing Indexes")
4. Analyze what type of indexes exists? How were they created?
5. Create a new index on emp's ename column (slide 9 - "Index Creation").
6. Repeat instruction of step 3. - Viewing indexes


## Advance SQL: Top N Analysis - TOP

<ins>Find the Top-5 Highest Salary in Emp's table:</ins>

`SQL> SELECT ename, job, sal FROM emp ORDER BY sal DESC;`

Now,
`SQL> SELECT TOP 5 ENAME, JOB, sal FROM emp ORDER BY sal DESC;`


## Advance SQL: Top N Analysis - RowNum()
<ins>Find the 5 Highest Salary in Emp's table:</ins>
`SQL> SELECT ename, job, sal,
  ROW_NUMBER() OVER (ORDER BY sal DESC) AS RowNum FROM Emp;`
**Now:**
`SQL> SELECT * FROM (SELECT ename, job, sal, ROW_NUMBER() OVER (ORDER BY sal DESC) AS RowNum FROM Emp ) "EmpSal"
WHERE RowNum = 5;`


## Advance SQL: Top N Analysis - RANK()
**Write a query to rank employees in each department based on their salary (highest salary = rank 1):**

`SQL> SELECT empno, ename, deptno, sal, RANK() OVER (PARTITION BY deptno ORDER BY sal DESC) AS SalaryRank
FROM Emp;`


## Class Excercise - Execution Plan
`SQL> select* from emp where deptno = 10;`
- Use CTRL + M to view the execution plan (EP). Hover the mouse pointer on execution plan to view details in the tool tip. Examine & analyze the EP

`SQL> SELECT * INTO emp2 FROM emp;`
- Now, view if there are indexes on emp2 table

`SQL> SELECT * FROM emp2 WHERE deptno = 10;`
- User CTRL + M to view the execution plan (EP). Examine & analyze the EP. Compare it to the first EP.

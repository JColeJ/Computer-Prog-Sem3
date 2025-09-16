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

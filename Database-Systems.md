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
  - CREATE USER JohnUser FOR LOGIN JohnLogin;


### Security Features - PERMISSIONS
- Define what actions users/roles can perform.
- Levels:
  - Server-level -> CREATE DATABASE, ALTER ANY LOGIN.
  - Database-level -> SELECT, INSERT, UPDATE, DELETE, EXECUTE.
  - Object-level -> permissions on specific tables, views, or stored procedures.
- Example (SQL's DCL):
  - GRANT SELECT, INSERT ON Employees TO JohnUser;


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

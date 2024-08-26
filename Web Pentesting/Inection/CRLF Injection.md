# CRLF Injection

With CRLF Injection we can able to inject `\r \n` CRLF characters. If our input reflects in response we can able to inject a new header.

Carriage Return  - Marks the end of the line

Line Feed  - Marks the Start of a new line

`\r` - carriage Return 

`\n` - new line or line feed

`%0d%0a` - encoded `\r\n`
![](Pasted%20image%2020240624110303.png)

### SSRF to CRLF:
```
example.com/ssrf.php?url=/test%0d%0aHost:%20attacker.com
```
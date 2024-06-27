# DNS Zone Transfer

dns zone transfer is used to copy a zone file from a master dns to a slave dns


Identify the DNS Servers

```
dig @8.8.8.8 ns any_domain.com
```
OR
```
host -t ns any_domain.com
```

Now copy the DNS URL which got from the above command

```
dig @<DNS_URL> axfr any_domain.com
```
OR
```
host -l any_domain.com <DNS_URL>
```

---

##### Example

```
dig @8.8.8.8 ns zonetransfer.me

got nsztm1.digi.ninja

dig @nsztm1.digi.ninja axfr zonetransfer.me
```


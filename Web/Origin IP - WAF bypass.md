# Origin IP - WAF bypass

## Tools


WAFRecon

dnsrecon

hakoriginfinder https://github.com/hakluke/hakoriginfinder

---

## Websites

shodan

censys

securitytrails 

## Methods

```
1️⃣ Discover your target's ASN and check [https://lnkd.in/gEASNWHK](https://lnkd.in/gEASNWHK)  
2️⃣ Make a note of the target's IP range.  
3️⃣ Assuming you have a WAF-protected domain called example[.]com. Use this command with the IP range Identified in step 1 and pass your target host against the -h parameter:  
  
prips [93.184.216.0/24](http://93.184.216.0/24) | hakoriginfinder -h example[.]com
```


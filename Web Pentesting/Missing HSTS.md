# Missing HSTS

HTTP Strict Transport Security 

It enforces or strict the application to use only HTTPS 

The HTTPS might be already exist but it may also work on HTTP. For that it will force to use only HTTPS.


```
curl -s -D- https://domain.com/ | grep -i Strict
```

If we get any response as **Strict** it is not vulnerable.  


we can also check in this.
https://www.ssllabs.com/ssltest/


---
This will give all the missing headers

```
hsecscan -u www.domain.com
```

---

Force to use http the website (browse with http)


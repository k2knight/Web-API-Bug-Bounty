# Shodan Dorks

| Description | Dork | Comments |
| ---- | ---- | ---- |
| Path Traversal Vulnerability in File Inclusion Check Point | title:"Check Point" ssl:"target" | aCSHELL/../../../../../../../etc/shadow<br><br>CVE-2024-24919 |
|  | http://ssl.cert.subject.CN:"*.target.com" "230 login successful" port:"21"  |  |


```
1. http://ssl.cert.subject.CN:"*.target.com" http.title:"index of/" 
 
2. http://ssl.cert.subject.CN:"*.target.com" http.title:"gitlab" 
 
3. http://ssl.cert.subject.CN:"*. http://target.com" http.title:"gitlab" 
 
4. http://ssl.cert.subject.CN:"*.target.com" "230 login successful" port:"21" 
 
5. http://ssl.cert.subject.CN:"*. http://target.com" +200 http.title:"Admin"


```
# Recon

| Recon Type | URL | Use | Other |
| ---- | ---- | ---- | ---- |
| ASN's | http://bgp.he.net/ |  |  |
| IP Enumeration | https://whois.arin.net/ui/query.do<br>https://apps.db.ripe.net/db-web-ui/#/fulltextsearch | we will get range of IP addresses |  |
| Shodan | www.shodan.io |  |  |
| Karma v2 | https://github.com/Dheerajmadhukar/karma_v2 | AUTOMATED SHODAN |  |
| Shosubgo | https://github.com/incogbyte/shosubgo | Sub domain enum with shodan |  |
|  | www.cert.sh | subdomain |  |
| BBRF |  |  |  |
| crunchbase | https://www.crunchbase.com/ | acquisitions |  |
| OCCRP | www.OCCRP.ORG | research material for investigative reporting |  |
|  | https://kaeferjaeger.gay/ | Cloud Recon |  |
|  | www.whoxy.com  (api also) | reverse whois |  |
|  | https://github.com/hakluke/hakrawler | spiders discovery |  |
|  | Trademark, Terms of Service, Copyright, & Privacy Policy Recon (using Google) |  |  |
|  | https://www.virustotal.com/gui/home/search | Subdoamin |  |
|  | https://censys.io/ | Subdoamin |  |
|  | https://www.netcraft.com/ |  |  |
| `aquatone` |  | screenshots websites |  |

`cat *.txt | grep -F ".dell.com" | awk -F'-- ' '{print $2}'| tr ' ' '\n' | tr '[' ' ‘| sed 's/ //’| sed 's/\]//’| grep -F ".dell.com“ | sort -u`



![](Pasted%20image%2020240618230537.png)
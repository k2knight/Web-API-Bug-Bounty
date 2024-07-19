# Automation

```
1. Get all urls (waymore)  
2. Extract all Parameters (paramspider)  
3. Use nuclei dast templates  
nuclei -l parameter_based_urls.txt -t nuclei-templates/dast/ -dast
```


```
katana -u vulnweb.com -d 5 -ps -pss waybackarchive,commoncrawl,alienvault -f qurl -jc -xhr -kf -fx -fs dn -ef woff,css,png,svg,jpg,woff2,jpeg,gif,svg -silent | nuclei -t ~/pvt-template/ -dast -silent -o vulns.com
```


https://github.com/Josekutty-K/nuclei-templates
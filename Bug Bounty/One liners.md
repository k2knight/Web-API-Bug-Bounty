# One liners

https://github.com/dwisiswant0/awesome-oneliner-bugbounty

/.git File Mass Hunting

```
cat alivesubs.txt | grep "SUCCESS" | gf urls | httpx-toolkit -sc -server -cl -path "/.git/" -mc 200 -location -ms "Index of" -probe
```


```
waybackurls url | grep '\.js$' | awk -F '?' '{print $1}' | sort -u | xargs -I{} python lazyegg[.]py "{}" --js_urls --domains --ips > urls && cat urls | grep '\.' | sort -u | xargs -I{} httpx -silent -u {} -sc -title -td
```

XSS 

```
Katana -list targets.txt -silent -d 6 -rl 20 -jc -f qurl -o params.txt 
```


![](Pasted%20image%2020240630225845.png)
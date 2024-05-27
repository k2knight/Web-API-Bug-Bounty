# JS Files

```
LazyEgg - Hunting JS Files  
  
waybackurls target | grep '\.js$' | awk -F '?' '{print $1}' | sort -u | xargs -I{} bash -c 'echo -e "\ntarget : {}\n" && python lazyegg[.]py "{}" --js_urls --domains --ips'
```


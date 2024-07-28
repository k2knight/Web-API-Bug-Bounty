	# Methodology

## Recon

#### Sub Domain Enum

```
assetfinder target.com -subs-only | tee -a asset.txt
```

```
crtsh -q target.com -o | tee crtsh.txt
```

```
findomain -t target.com -o | tee finddomain.txt
```

```
subfinder -d target.com | tee subfinder.txt
```

```
./lazyrecon.sh -d target.com
```

```
github-subdomains -d target.com
```

Combine all 

```
cat asset.txt crtsh.txt finddomain.txt subfinder.txt github.txt >> subdomains.txt
```

alive

```
cat subdomains.txt | httpx | tee -a alivesubs.txt
```

```
paste -sd ',' alivesubs.txt > urls_comma_separated.txt
```
#### Screenshotting

```
cat alivesubs.txt | aquatone
```

## Auto

Nuclei
```
nuclei -list alivesubs.txt | tee nuclei_result.txt
```

Nmap
```
nmap -A -iL alivesubs.txt
```

Nikto
```
while IFS= read -r url; do
  output_file=$(echo $url | sed 's/[^a-zA-Z0-9]/_/g').txt
  nikto -h "$url" -o "$output_file"
done < alivesubs.txt
```

## Wayback

```
cat alivesubs.txt | waybackurls | tee -a wayurls.txt
```

```
cat wayurls.txt | httx | tee -a wayback_alive_urls.txt
```

from here search for admin, config, ini using grep
```
cat wayback_alive_urls.txt | grep config
```

Search for parameter's and combine with XSStrike for XSS
```
grep '?.*=' wayback_alive_urls.txt > urls_with_parameters.txt
```

```
xssstrike -u url   //incomplete
```

grep all JS files from wayback urls
```
cat wayback_alive_urls.txt | grep ".js$" >> jsfiles.txt
cat wayback_alive_urls.txt | grep "$.js$" >> jsfiles.txt
cat wayback_alive_urls.txt | grep "$.js" >> jsfiles.txt
```

find interesting files from wayback
```
cat allurls.txt | grep -E "\.txt|\.log|\.cache|\.secret|\.db|\.backup|\.yml|\.json|\.gz|\.rar|\.zip|\.config"
```

SSRF from Wayback
```
cat alive.txt | gauplus -subs -b png,jpg,jpeg,woff,gif,svg,swf -o ssrfurls.txt
cat allurls | gf redirect | ssrfurls.txt
cat allurls | grep "=" | ssrfurls.txt
```

```
cat ssrfurls.txt | grep "="  | /root/go/bin/qsreplace http://www.(burp-colabrattor) | anew ssrf.txt
```

### Dorking

https://nitinyadav00.github.io/Bug-Bounty-Search-Engine/

https://mr-dorker.onrender.com/

```
login, register, upload, contact, feedback, join, signup, profile, user, comment, api,
developer, affiliate, careers, upload, mobile, upgrade, passwordreset.
```

## Testing

Subdomain takeover

```
subzy run --targets alivesubs.txt
```

Broken link hijack

```
socialhunter -f alivesubs.txt
```

```

```
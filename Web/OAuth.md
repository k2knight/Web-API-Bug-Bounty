# OAuth


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

### Forced OAuth profile linking

### OAuth account hijacking via redirect_uri

### Stealing OAuth access tokens via an open redirect

### Stealing OAuth access tokens via a proxy page

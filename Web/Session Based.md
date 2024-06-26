# Session Based

### Session Fixation

**Scenario 1** : copy cookie before login --> paste in another browser --> login in 2nd browser --> refresh the 1st browser after logging in 2nd browser --> if we logged IN in 1st browser it is session fixation 


**Scenario 2** (indented): login --> copy cookie --> import cookie in 2nd browser --> if we logged IN in 1st browser it is session fixation


**Scenario 3** : login --> copy cookie --> logout --> import copied cookie to the browser --> if we logged IN in 1st browser it is session fixation

---
#### Session Transmission


Session ID in URL Vulnerability (in GET method)

Send session ID in unencrypted (http)

changing HTTPs to HTTP

Changing session ID traversing from POST to GET 

Session not expired after logout

---

#### Forgot Password

Use same forgot password link to reset again

investigate the forgot password link to manipulate

Send multiple forgot password reset link --> reset with last one --> login --> logout --> reset password with old link

forgot password --> get the link --> login with old pass --> update email id --> logout --> use that link to reset password.

login --> change email id --> logout --> forget password --> use old email to reset password 
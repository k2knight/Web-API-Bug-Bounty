# Cookie Terminology

## Same Site 

It restricts how cookies are sent with cross-site requests

*None* : Cookie is sent with all requests, regardless of where they come from

*Lax* : Cookies are sent when 2 conditions are met. 1) The request uses the `GET` method and 2) The request resulted from a top-level navigation by the user, such as clicking on a link. (2 minute Time frame)

*Secure* : Cookie is sent visiting the site directly or from a sub domain 

## Http Only

These are cookies that cannot be accessed or modified by JavaScript.

## Secure

The `Secure` attribute for cookies ensures that the cookie is only sent over HTTPS.
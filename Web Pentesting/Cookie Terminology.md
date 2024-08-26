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

## SOP (Same-Origin Policy):

restrict how a script loaded from one origin can interact with resources from another origin.
OR
Prevents a website from accessing resources belonging to other websites

## Content security policy

Syntax- Content—Security-Policy: $directives "sources"

`default-src` - Used to allow certain domains which can share resources with us

`script-src` -  Used to allow trusted domains to load scripts
Prevents XSS Attack

`frame-ancestors` - used to allow specific domains to load our website inside the iframe
Prevents Clickjacking Attack
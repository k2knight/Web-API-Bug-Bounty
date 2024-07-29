# SQLi Methodology

Start with giving

```
' 
"
`
')
")
`)
'))
"))
`))
```

Test in HTTP headers like accept language payloads are there in [SQLi Payloads](SQLi%20Payloads.md). 

Test in API request End point `api/user/99`. Test in 99.

Give unusual encoding payload `%BF` `%ff` which have no meaning and the sever might throw some error

give Unicode's [unicode converter](https://qaz.wtf/u/convert.cgi) to throw some error

give a `[]` for a parameter input field. where it expects 1 value, but we are forcing with an array typically gives an error. `artists[]=1`


---
Use Atlas Tool to find Injections bypassing the WAF
